---
title: Running a Few Unicorn apps on one Nginx install
layout: post
---

Since last year, we've been running Rack-based apps on Unicorn and using Nginx as a reverse proxy to access them. Up to now I've been in the luxurious position that I've only had to deploy one app per host. Now I've got to do more.

This post is more about Nginx configuration than Unicorn. That sits nicely in the background on a Unix socket.

From '/etc/nginx/sites-available/default'

    
