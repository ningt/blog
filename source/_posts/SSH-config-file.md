title: Secure Your SSH
date: 2015-12-21 13:51:50
tags: ssh
categories: Linux
---
Every time we setup a new server, we wanna secure the ssh access. Here are some common practices to improve the security of ssh.

- **Disable root login**

```
$ vim /etc/ssh/sshd_config

PermitRootLogin no
```
<!--more-->

- **Only allow specific users**

```
$ vim /etc/ssh/sshd_config

AllowUsers admin user
```
- **Only allow ssh access from certain ip address**

```
$ vim /etc/ssh/sshd_config

# must be a public ip address
ListenAddress 175.12.21.233
```
Alternatively, we can achieve this by using `iptables`.

```
iptables -A INPUT -p tcp --dport 22 -s YourIP -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
- **Use public key authentication instead of password**

```
# generate key pairs on your local computer
$ ssh-keygen -t rsa

# copy your public key to remote server
$ ssh-copy-id user@123.45.56.78

# disable password login
# uncomment PasswordAuthentication and set it to no
PasswordAuthentication no
```

##### Make it more convenient
Normally when ssh into a remote server, we have to type commands like this:

```
$ ssh root@192.168.92.1
$ ssh user@tangning.me
```
which is quite troublesome to remember exact ip address or to type a long domain name. The use of ssh config file can make your life much easier.

Create a new config file at path `~/.ssh/config`. An example of ssh config file is like this:

```
Host blog
	HostName tangning.me
	User user
	IdentityFile ~/.ssh/some.key
```
With the new config file just created, you can ssh into the remote server using just
```
$ ssh blog
```