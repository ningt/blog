title: SSH config file
date: 2015-12-21 13:51:50
tags: ssh
---
Normally when ssh into a remote server, we have to type commands like this:

```
$ ssh root@192.168.92.1
$ ssh root@tangning.me
```
which is quite troublesome to remember exact ip address or to type a long domain name. The use of ssh config file can make your life much easier.

Create a new config file at path `~/.ssh/config`. An example of ssh config file is like this:

```
Host blog
	HostName tangning.me
	ForwardKey yes #forward your ssh key
	User root
```
With the new config file just created, you can ssh into the remote server using just
```
$ ssh blog
```
If have ssh key enabled, you don't even have to enter your password.