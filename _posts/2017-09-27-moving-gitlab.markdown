---
title: Moving Gitlab
layout: post
published: true
---

![deploy in progress](/images/gitlab-deploy-page.png)

On the source host:

```
$ sudo gitlab-ctl deploy-page up
$ gitlab-rake gitlab:backup:create
$ scp /var/opt/gitlab/backups/most_recent_gitlab_backup.tar user@destinationhost:/path/

```

On the destination host:

```
$ sudo gitlab-ctl deploy-page up
$ sudo mv /path/most_recent_gitlab_backup.tar /var/opt/gitlab/backups/
$ chown git:git /var/opt/gitlab/backups/most_recent_gitlab_backup.tar
$ gitlab-ctl start
$ gitlab-ctl stop unicorn
$ gitlab-ctl stop sidekiq
$ gitlab-rake gitlab:backup:restore BACKUP=most_recent
$ gitlab-ctl start
$ gitlab-rake gitlab:check SANITIZE=true
$ gitlab-ctl deploy-page down

```

At this point, you can make tweaks to `/etc/gitlab/gitlab.rb` and run `gitlab-ctl reconfigure`.
