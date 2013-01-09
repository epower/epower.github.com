---
title: Long SSH login with Ubuntu
layout: post
---

I log into a number of ssh hosts on a regular basis. Usually its from a Mac but I've also had a netbook for some time which has Ubunut on it. I noticed a couple of years ago that one host took some time to prompt me for my password. At first I suspected it was the host but didn't give it much thought as it was just one host. Turns out it was the [default ssh config for Ubuntu](http://germanrumm.eu/fixing-ssh-login-delay-how-to-disable-gssapi-with-mic-on-ubuntu-linux/).

So adding one line to my _.ssh/config_

    ...
    GSSAPIAuthentication=no
    ...

does the job.
