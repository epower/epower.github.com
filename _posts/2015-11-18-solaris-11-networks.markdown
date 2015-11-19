---
title: Solaris 11 Networks
layout: post
---

The following are some notes so I don't forget what I did with Solaris 11 on given hosts:
 - I've got a single host with a few interfaces connected to a switch
 - I've added link aggregation (but only with single interfaces) in front of the physical. This is for a later project where I'll be looking at link aggregation and LACP.
 - I'd like to run a few zones on 2 of the interfaces/aggrs.
   - the first interface is connected to a DMZ for external facing connectivity
   - the second interface is connected to an internal VLAN for local services
 - on another interface, I'd like to create an ip interface for connecting to the host for management

## Comments

Its worth noting that if you've got an aggr with an ip interface attached to it, the datalink is in use. This means that you can't move zone vnics to this aggr. In order to move vnics to this aggr, apparently [you must delete the ip interface first](https://docs.oracle.com/cd/E23824_01/html/821-1458/fpjvl.html).

```
root@solaris-test:~# dladm
LINK                CLASS     MTU    STATE    OVER
net0                phys      1500   up       --
net1                phys      1500   up       --
net2                phys      1500   up       --
extapps0            aggr      1500   up       net1
intapps0            aggr      1500   up       net2

root@solaris-test:~# ipadm
NAME              CLASS/TYPE STATE        UNDER      ADDR
lo0               loopback   ok           --         --
   lo0/v4         static     ok           --         127.0.0.1/8
   lo0/v6         static     ok           --         ::1/128
net0              ip         ok           --         --
   net0/v4        dhcp       ok           --         10.0.2.15/24
   net0/v6        addrconf   ok           --         fe80::a00:27ff:fe31:ae8c/10

```

A further complication emerges when you create a zone and boot it. The zone creates a temporary vnic object associated with the zone. Unfortunately, it appears one can't move this temporary vnic between aggrs as you can with vnics created in dladm in the global zone. 

The solution appears to be to create a vnic in dladm and set this as the physical interface in the net config of the zone. After removing the default anet. 

Then configure the network in the zone as required. 

```
root@solaris-test:~# dladm modify-vnic -l intapps0 testzonevnic0

root@solaris-test:~# zlogin testzone

root@testzone:~# ipadm delete-addr testzonevnic0/v4
root@testzone:~# ipadm create-addr -T static -a local=10.0.4.15/24 testzonevnic0
root@testzone:~# route -p add default 10.0.4.2
add net default: gateway 10.0.4.2
add persistent net default: gateway 10.0.4.2
root@testzone:~# ping 8.8.8.8
8.8.8.8 is alive

```

