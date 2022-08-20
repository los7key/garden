---
layout: post
title: About Passwords
description: About Passwords
date: 2022-08-14
Last Updated: 2022-08-19
---
## Introduction

After running a [honeypot](/tech/security/cowrie_honeypot/) for a few weeks and seeing the same passwords used over and over, it got me thinking.  The  “rockyou” wordlist is an industry standard in the cyber security field, how can it still be relevant all these years later?!  The answer is simple; People haven’t changed their security hygiene. 

First, let’s talk about what the rockyou wordlist is and why it is still in use.  In December 2009, a social app company named RockYou had threat actors breach their security and steal 32 million user accounts including usernames and passwords stored in plain text. Because it’s so easily attainable and comprehensive, it is still commonly used (successfully) in dictionary attacks.  The full list of passwords exposed as a result of the breach is available on the Internet and is even included in Kali Linux since it’s launch in 2013.

At the time of writing, it is 2022.  It’s been 13 years since the RockYou breach, not to mention many, many more breaches since then, and what have we learned?  We know nefarious people have access to a list of 32 million passwords that were actually in use back in 2009.  We know they use this list of passwords to attempt to break into other user’s accounts.  So why are we still using those SAME PASSWORDS?

Not only are people using easy to guess passwords, but companies that make devices people rely on like firewalls, web cams, routers, etc. STILL ship products with the same default password to consumers who are either too lazy, or don’t know that they should change the default password from “123456”.

## Breakdown

Here are the top 10 password attempts the [honeypot](/tech/security/cowrie_honeypot/) that I was running in a DO droplet:

```
nproc
123456
password
123
admin
test
root
password123
test123
P@ssw0rd
```

Why does this matter?  This shows that there is still a possibility of finding an account with an easy to guess password.  If it didn’t work, threat actors wouldn’t try it.   

## Why is it bad to have a weak password?

Obviously, using the same password for everything is a very dangerous thing to do. You're probably thinking, "I don't care if someone finds my Netflix account, nobody cares what I'm watching."

But what if Netflix was compromised? Think about the things that Netflix knows about you..

* Username
* Password
* Credit Card
* Programming choices
* Email address
* Home/billing address

Now, what could someone do with THIS data? Would any of these things be used by your other accounts like Amazon or bank account or other financial accounts? You have to think like a hacker. If your Netflix data (that is now PUBLIC) contains the name of a pet or a relative, maybe they could guess other bits of data.

For example, if my compromised Netflix password is kitty89 and maybe my Amazon account password is also the same, then they would have complete control of your Amazon account including purchase history and a LOT more personal data.

Well, my password isn't EXACTLY the same, I increment the number at the end! Even still it would only take a few guesses if it was kitty88 or kitty95. Worse yet, if it were kitty1995, it'd be easy to guess 1995 was a significant year. Could it be part of your other passwords or maybe even a security code or PIN for something else? See where this can go? All because someone at Netflix made a mistake. Right? Well..

In some cases, it's not directly the fault of the company that is supposed to be protecting your data, it could be a third party or contractor. Regardless of who is to blame, this day and age there are a lot more people that have access to your data than you realize. 

## My Solution

**Use a password manager**
   
I'm probably going to against some people's opinions and say your passwords or credit card numbers are far more secure in an encrypted storage that is also encrypted end to end than keeping it locally.  But I think at some point, you HAVE to trust someone with your important data, especially passwords.  There are alternatives, but most either require a lot of overhead, require advanced technical skills, or just aren’t much more secure anyway.

I currently have 378 passwords and secure notes in my password manager.  There is no possible way I could remember every single one unless I just used the same one everywhere.  My passwords are all randomized, and I don’t even have to see them to use them!  

It may not be perfect, no solution really is. But it's a step up from a Post-It note under the keyboard or kitty1995.