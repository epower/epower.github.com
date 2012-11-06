---
title: Growing a Project with Git
layout: post
---
I ran into an interesting problem in work a couple of months ago. I only write about it now because I've only had time to deal with it properly now. We started a project in January 2012. Up to this point in time, my main revision control system was [Subversion](http://subversion.apache.org/). However, with this project, there was a little space to move to [Git](http://git-scm.com/). 

When managing the code base for projects in Subversion, one big repository generally does the trick. You can do partial checkouts of the repository based on directory structure. However, Git has its [limits](http://osdir.com/ml/git/2009-05/msg00051.html). This effectively means one project per repository. At this point, my project had three components and was starting to grow faster. 

### Submodules

So to allow the project to grow, I decided to use [git-submodules](http://git-scm.com/book/en/Git-Tools-Submodules). This allowed me to have my super-project directory structure as defined at the start of the project and have individual repositories for component development. I also got a couple of other benefits. 

* Jenkins CI server can now clone individual components cleanly for testing (up to that point, I'd been using a dirty hack to get around this).
* The super-project knows the what (the path in .gitmodules), the where (URL in .gitmodules) and the when (the changeset hash is monitored in the super-project git index - this works well when I'm specifying git tags).

This is convenient from a source code management point of view. The individual components are built individually and use [Ant](http://ant.apache.org/), [Ivy](http://ivy.apache.org/) or [Maven](http://maven.apache.org/) for dependency management. The components are then published to a local [Nexus](http://www.sonatype.org/nexus/) repository.
