
### motivation: use cases

Why use git? Because it makes collaboration a joy and gives you an audit trail of each change you make to your project while maintaining data integrity. This improves productivity and transparency.

Even when you work alone on a project you collaborate with yourself in the future. Often you collaborate with yourself on multiple devices - a home and work machine, for example. Git helps you manage this in an efficient way: easily sync your project over multiple devices.

Workflow can be complex even when working alone but the really painful issues arise when collaborating with others. What if many people edit the same files at the same time? How does one handle conflicting changes? Git allows you to track changes per person, byte-by-byte and gives you methods to resolve conflicts in a programmatic way.

Git succeeds when simple remote file system synchronisation tools like Dropbox fail.

### git and version control

Git was initially developed by Linus Torvalds for Linux kernel development in 2005. It is distributed, so each copy is a respository with full history. It does not need a connection to a central server.

Version control, in general, is the management of changes to documents.

### concepts

* `repos`: a repository is an on-disk data structure which stores metadata about files and/or directories. The main purpose is to store a set of files along with the history of changes made to those files.

* `commits`: the unit in which you record changes in a repository

* `remotes`: a respository on a different machine that is synced with one on your own machine. Given git's distributed nature there is no "central" repo, only remotes.

* `branches`: all work in a repository happens on a specific branch. A branch can be seen as a specific line of work, a series of changes that are applied to files. A branch can be used, for example, to develop new features while making sure that other work is not affected.

### practical session

We'll take a learning by doing approach...

```bash

# getting help
git --help
git <command> --help

# create a repo
mkdir test-dir
cd test-dir
git init

# create a file, make changes, add and commit them
touch newfile
echo "here are some changes" > newfile
git status
git add newfile
git status
git add newfile
git commit -m 'first commit: adding data to newfile'
git satus

# ignoring files

# inspect state/history
git log

# keep changes for later

# clone a repo

# get new changes from a remote

# push changes to a remote

# create a branch

# find out who changed what



```

### commands reference

* `commit`: the unit in which changes are recorded in a repository
* `log`: a summary of commits
* `status`: a summary of the state of files in a repository
* `diff`: shows the difference between two states of one or more files
* `add`: an operation/instruction to include changes to a file into the next commit
* `stash`: an operation/instruction to store changes for later usage
* `clone`: make a copy of a repo
* `pull`: get changes from a remote repo and apply them to a local copy
* `push`: apply changes made to a local repo to a remote copy
* `rebase`: apply changes from a remote on top of changes that only exist locally
* `branch`: a distinct line of work (a named series of commits)
* `blame`: an operation/instruction to display the author and other information of a specific change

### tools
    * desktop clients
    * remote hosting options, pros and cons
    * git extensions - for special needs

### using git to get project info - examples
    * todoer - assess code quality
