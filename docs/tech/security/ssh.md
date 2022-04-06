---
layout: post
title: SSH Tunneling
---
Every now and then I need to use local port forwarding for a CTF or on rare occasions for work.  It's not often enough to keep committed to memory and I figured this might help other people as well.  So let's look at some examples of local port forwarding and remote port forwarding as well as why we would need them.

If you are in a hurry and just need something to jog your memory:

`ssh -L local_port:remote_address:remote_port username@remote_server.com` <- Local

`ssh -R remote_port:local_address:local_port username@remote_server.com` <- Remote

### Local Port Forwarding

“Local port forwarding” allows you to access resources that aren’t exposed to the Internet (or other networks). For example, if you want to access a web server at your office from your home and for security reasons, that server is only configured to accept connections from the local office network. If you have access to an SSH server at the office, and that SSH server allows connections from outside the office network, then you can connect to that SSH server from home and access the web server as if you were sitting in the office.

To use local port forwarding, connect to the SSH server normally, but also supply the -L argument. The syntax is:

`ssh -L local_port:remote_address:remote_port username@server.com`

If you're still following along with the example, assume the following is true:
* The web server at your office is located at 192.168.1.111 on port 8080.
* You have access to the office’s SSH server at ssh.youroffice.com.
* Your user account on the SSH server is "bob".

In that case, your command would look like this:

`ssh -L 8080:192.168.1.111:8080 bob@ssh.youroffice.com`

At this point, you’d be able to access the webserver on port 8080 at localhost. You could just plug in http://localhost:8080 to your web browser and browse the web server as if you were in the office.  All traffic sent to port 8080 on your host will be tunneled to 192.168.1.111:8080 on your office network.  Pretty handy for working at home!

### Remote Port Forwarding

“Remote port forwarding” is the opposite of local forwarding, and isn’t used as often. It allows you to make a resource on your local host available to a remote host. For example, let's say you’re running a web server on the local PC you’re sitting in front of. But your host is behind a firewall that doesn’t allow incoming traffic.

To use remote forwarding, use the ssh command with the -R argument. The syntax is largely the same as with local forwarding.  Note the LOCAL address of your host is used this time:

`ssh -R remote_port:local_address:local_port username@server.com`

Now we assume the following:  
* Your web application listening on port 8080 on your local host.
* The SSH server at your office is ssh.youroffice.com.
* Your user account on the SSH server is bob.

You’d run the following command:

`ssh -R 8888:localhost:1234 bob@ssh.youroffice.com`

Someone could then connect to the SSH server at port 8080 and that connection would be tunneled to the server application running on port 8080 on the local host you established the connection from.

Hopefully, this is useful for remembering the difference between local and remote port forwarding!
