title: Not expose ssh port to public
date: 2016-04-21 11:51:22
tags: ssh
categories: Linux
---

Sometimes from some secutiry reasons, we do not want to expose ssh port to public. We have a server with one public network interface `em1`, and one private network interface `em2`.

```
em1: 137.xx.xx.xx (public)
em2: 192.168.1.xx (private)
```

We want to hide ssh service from public, such that others cannot access to it directly from remote and scan result will not show the open ssh port as well.

<!--more-->

`iptables` is a tool to filter or forward your traffic, which is quite suitable for this task. You can use `man iptables` to check its detail usage and can build your own firewall. We use the following cammand to reject all ssh traffic on `em1`:

```
$ iptables -I INPUT -i em1 -p tcp --dport ssh -j REJECT
```

This command basically means that insert a new rule to chain `INPUT` to reject incoming traffic that uses protocol `tcp` with port number `ssh (22)` from interface `em1`. Since the rules of `iptables` are not persistent, which means every time you reboot the server, the rules will be lost, here we use a small tool called `iptables-persistent` to help us load the rules at system startup.

```
$ sudo apt-get install iptables-persistent
$ sudo service iptables-persistent save
$ sudo service iptables-persistent reload
```
 