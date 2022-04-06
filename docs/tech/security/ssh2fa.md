---
layout: post
title: 2FA SSH with Google Authenticator
---

Recently I set up a new VPS with DigitalOcean and it felt a bit exposed so I made a few tweaks to harden my droplet.  I'll probably make another post about some of the other steps I took later™.  For now, I wanted to do a quick walkthrough of setting up 2FA for SSH with [Google Authenticator](https://en.wikipedia.org/wiki/Google_Authenticator).  This guide was done for an Ubuntu-based host, but can be done with just about any flavor of Linux.

If you aren't using 2FA for EVERYTHING you possibly can, you are doing yourself a disservice with the number of data breaches rising, some highlighting the weakness in SMS-based 2FA.  You can find a [list of sites](https://twofactorauth.org/) that support 2FA and in many cases, how to tell other sites they should support it.  It's also a good idea to use ssh keys if you aren't already.

This post makes some assumptions; That you are familiar with how to edit files in a terminal, and you know what SSH and two-factor authentication is.  I'm also assuming you already have your favorite authenticator app.

Lastly, the usual warning about doing things at your own risk applies.  If you're not careful you can lock yourself out of your host and you will be sad.  There are only a few steps, read them all BEFORE you start, you've been warned! 

### 1. Install Packages

```
$ sudo apt install libpam-google-authenticator
```

### 2. Configure SSH Server (with sudo/root access)

- Open /etc/pam.d/sshd with your favorite text editor (vim) and add the following line:

```
auth required pam_google_authenticator.so
```

-  Edit /etc/ssh/sshd_config and set this line to `yes` to enable use of the Authenticator we added to the pam configuration.

```
# Change to yes to enable challenge-response passwords
ChallengeResponseAuthentication yes
```

NOTE: DO NOT RESTART SSHD YET!

### 3. Set up Google Authenticator

With the package we installed in step 1, we now have a binary that allows us to configure the Google Authenticator.

```
$ google-authenticator
```

Read the options presented and decide what suits your needs. Selecting yes to each question is a good option.  Make note of the backup codes somewhere safe. This will allow you to log into your ssh server if you don't have your app.

```
Do you want authentication tokens to be time-based (y/n) y

Do you want me to update your "/home/user/.google_authenticator" file? (y/n) y

Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases your
chances to notice or even preventing man-in-the-middle attacks (y/n) y

By default, a new token is generated every 30 seconds by the mobile app. In order
to compensate for possible time skew between the client and the server, we allow
an extra token before and after the current time. This allows for a time skew of 
up to 30 seconds between authentication server and client. If you experience
problems with poor time synchronization, you can increase the window from its
default size of 3 permitted codes (one previous code, the current code, the next
code) to 17 permitted codes (the 8 previous codes, the current code, and the 8 
next codes). This will permit for a time skew of up to 4 minutes between client 
and server.
Do you want to do so? (y/n) y

If the computer that you are logging into isn't hardened against brute-force login
attempts, you can enable rate-limiting for the authentication module. By default, 
this limits attackers to no more than 3 login attempts every 30s. 
Do you want to enable rate-limiting? (y/n) y
```

### 4. Add the key to your Google Authenticator App

There are many other authenticator apps aside from Google's to pick from so I'll leave it up to you to configure.  I use [Authy](https://itunes.apple.com/us/app/authy/id494168017?mt=8) for iOS and it's pretty straightforward to set it up with the QR code from above.

### 5. Restart the SSH service 

Now comes the moment of truth because restarting sshd will likely log out your current session (if you are logged in remotely with SSH).

```
$ sudo service sshd restart
```

### 6. Test your access

You should now be prompted for the code as well as the usual password. If you are using keys to access your host, you will still have access using the key and won't be prompted for the code. The 2FA code has been configured to only apply to the password-based authentication.

Fret not! If you have already configured ssh keys (as you should!) and want to test out your 2FA, it's pretty simple:

```
$ ssh -o PasswordAuthentication=yes -o PubkeyAuthentication=no user@host.com
Password:
Verification code:
```

Now you can rest easier knowing that even if your credentials are somehow compromised, your host will still require 2FA!