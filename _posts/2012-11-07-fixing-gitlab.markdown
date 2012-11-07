---
title: Fixing GitLab
layout: post
---
Did I mention that I really like [GitLab](http://gitlabhq.com/)? It lets me host and manage in-house git repositories for the various projects I work on before the blessed few get published to the outside world.

However, I was screwing around adding a new key for a laptop I'm using at the moment. [And then something broke](https://groups.google.com/forum/?fromgroups=#!topic/gitlabhq/kFkwNVqTYgE). GitLab had 2 keys for the laptop in question - one which was correct (and provided me with the correct access to my projects) and one which was older (and provided me with no access at all). By default, gitolite went with the older and more useless key. This was all visible in the gitolite authorized_keys. 

    ssh git@git.lab
    PTY allocation request failed on channel 0
    hello epower_duff_key, this is gitolite v2.2-11-g8c4d1aa running on git 1.7.0.4
    the gitolite config gives you the following access:
        @R_ @W_	testing

First I remove the entry from authorized_keys but this was just a temporary fix. Gitolite regenerates this file periodically from a gitolite-admin repository which has restricted access under the install with GitLab. 

So I decided to dig into the repository and remove the miscreant key. 

    sudo -u gitlab -H git clone git@localhost:gitolite-admin.git /tmp/gitolite-admin
    cd /tmp/gitolite-admin/keydir
    ls

And there I spotted the keyfile that needed to be removed.

    sudo -u gitlab -H git rm epower_duff_key.pub
    sudo -u gitlab -H git commit -m "fixing key"
    sudo -u gitlab -H git push

I couldn't find the recommended 'gitolite push' command so while [the relevant gitolite documentation](http://sitaramc.github.com/gitolite/emergencies.html#bypass) says don't use 'git push', it seemed to do the trick here. 
