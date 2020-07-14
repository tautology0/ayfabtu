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

git-grab has been ported to Python and has a better user interface that means that you can list files and supply a glob to only download important files.

It just uses standard Python3 libraries so shouldn't need anything special installed.
```
usage: git-grab [-h] [--cache [CACHE]] [--verbose] [--outdir OUTDIR]
                --url url action [files [files ...]]

Abuse .git repos on web servers

positional arguments:
  action           Action to perform: ls, download, view, scan, discover
  files            list of file globs

optional arguments:
  -h, --help       show this help message and exit
  --cache [CACHE]  Directory to cache downloaded files
  --verbose        Be verbose
  --outdir OUTDIR  Directory to store output
  --url URL        URL of site (method option)
  --verison VERS   Retrieve version VERS of file
```
The default for the cache directory is ./.gitgrab and outdir is the domain part of the url.

Examples:
```
git-grab --url vulnerablesite.com ls
git-grab --url https://vulnerablesite.com/ download \*.php \*.conf
git-grab --url https://vulnerablesite.com/ view config.php
git-grab --url vulnerablesite.com scan
```

Commands
========
The various commands do various things with various levels of stealth:

scan
This will attempt to scan the git directory for common flaws, such as a WordPress configuration file or whether .git/config contains stuff like passwords.

ls
This will list all files, where multiple versions are provided they will be listed by index and that versions hash.

view
download
These are very similar - the only difference is that view will dump the file to standard out whilst download will download the resourse and save it outdir.

These can take a number of globs after the command, to say, download all globs.

If --version is used then only that version will be attempted to be accessed. If not all versions will be outputed.

discover
This will attempt to follow the commit path and recover all possible versions of a file that can be discovered in the archive.

This is very noisy and will cause a lot of traffic on the network.

