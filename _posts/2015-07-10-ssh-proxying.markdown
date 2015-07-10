---
title: SSH Proxy
layout: post
---

Sometimes you need to access a host on a private network and the only access you have to that network is via an SSH server at the edge. For me, I've got a bunch of servers in a VPC and one machine at the edge with an Elastic IP. I built some SSH config options so I can quickly access these resources without having to re-invent the wheel each time.

I use ssh (comes with OSX and Linux generally) and nc (netcat), installed via [HomeBrew](http://brew.sh).

In '~/.ssh/config':
    
    Host tunnel
      HostName elastic-ip-of-edge-server
      User my-user-account
      ServerAliveInterval 30
      DynamicForward localhost:1080

This creates an alias called tunnel that I can use to proxy traffic over. 

Also in '~/.ssh/config':

    Host private-server
        HostName private-ip-of-server
        User user-account-on-private-server
        ProxyCommand /usr/bin/nc -x localhost:1080 %h %p

This creates a connection to the private server by netcatting the traffic over the ssh proxy. To access it, I open the tunnel first and then connect to the private server.

    $ ssh tunnel

In a seperate terminal tab:

    $ ssh private-server

That's it.
