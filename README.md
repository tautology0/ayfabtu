ayfabtu - All Your File Are Belong To Us
========================================

Scripts to extract files from SCM directories left on web servers. 

The scripts were written due to finding web servers where the designers had used
an SCM as part of their release mechanism. Using an SCM (like SVN or git) often stores metadata in the contents of a local cache.

The contents are often a local copy of the contents of the repo. Not only does
this reveal source code, which can then be analysed for other flaws, it can
often include the configuration files (such as web.config) which can reveal
passwords.

Current scripts:
* svn-grab, will extract all files from the pristine directory of the SVN repo
* hg-grab, will extract files from a Mercurial repo
* git-grab, will extract files from a git repo.
