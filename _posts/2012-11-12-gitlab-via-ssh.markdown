---
title: GitLab via ssh
layout: post
---
I've been preparing a quick guide for some colleagues to use our GitLab server via ssh tunnel. The server is located on a private network with only ssh access for those not located in the building. First you need to prepare your ssh config in '~/.ssh/config':

    Host tunnel
    HostName gateway.server
    User bob
    TCPKeepAlive yes
    LocalForward 2222 gitlab.server:22
    LocalForward 8888 gitlab.server:80


I've used [LocalForward](http://linux.die.net/man/5/ssh_config) to provide the ssh service on port 2222 from the GitLab server and 8888 to provideo the http service from the GitLab server. Then its easy enough to clone a repository. First, let's have a look at what we have access to:

    $>ssh git@localhost -p 2222 -T
    hello bob_laptop_1232247186, this is gitolite vx.x-xx-vvvvvv running on git x.x.x.x
    the gitolite config gives you the following access:
    R   W	bobrepo
	R	alicerepo


To clone 'bobrepo' just do the following:

    $>git clone ssh://git@localhost:2222/bobrepo.git


Then work away as needed.
