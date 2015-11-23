
### motivation: use cases

Why use git? Because it makes collaboration a joy and gives you an audit trail of each change you make to your project while maintaining data integrity. This improves productivity and transparency.

Even when you work alone on a project you collaborate with yourself in the future. Often you collaborate with yourself on multiple devices - a home and work machine, for example. Git helps you manage this in an efficient way: easily sync your project over multiple devices.

Workflows can be complex even when working alone but the really painful issues arise when collaborating with others. What if many people edit the same files at the same time? How does one handle conflicting changes? Git allows you to track changes per person, byte-by-byte and gives you methods to resolve conflicts in a programmatic way.

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

We'll take a learning by doing approach. We will work in a repo that we create ourselves and in one we download from the web.

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
git commit -m 'first commit: adding data to newfile'
git status

# ignoring files
touch .gitignore
echo "4,5,6" >> somedata.csv
git status
echo "*.csv" >> .gitignore
git status
git add .gitignore
git commit -m 'ignore all csv files'

# inspect state/history
git log
git diff <hash>

# history with pretty formatting
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# keep changes for later
echo "another line of data" >> newfile
git stash
git stash show
git stash apply
git add newfile
git commit -m 'newfile added'

# remove files
git rm newfile
git commit -m 'removing newfile from repo'
```

```
# clone a repo
cd ..
git clone https://github.com/leondutoit/git-for-research.git
cd git-for-research
git log
git remote show origin

# now I will make some changes and push them to this remote
# then you can sync your local copy

# get new changes from a remote
# make sure that any local changes are applied on top of mine
git pull --rebase
git log

# create a branch, work on it
git branch
git branch feature
git branch
git checkout feature
git branch
echo "this is data afor nother file" >> anotherfile
git add anotherfile
git commit -m 'adding a new feature to the project'

# switch back
# show which commits are on feature branch but not master
# apply changes from another branch
git checkout master
git log -n 5
git log feature --not master
git merge feature
git log -n 5
```

```
# find out who changed what
# do this in the git-for-research repo
git blame README.md

# say you wanted to develop the course notes from a point in time in the past
# reset the HEAD to a specific point in tie
# stash away the changes
# create a new branch and work from there
git log -n 5
git reset <hash>
git status
git stash
git branch newbranch
git checkout newbranch

# in the extreme case that you want to throw away commited changes
# _and_ have not shared the commits with anyone else
# E.g. if you have only commited locally and you want to start over
# do: git reset --hard <hash>
```

### collaborative workflows

#### pushing to the same repo

We simulated a small part of this when I made changes and you pulled them with a rebase. Collaboration could be set up so that everyone can push to the same remote. It would then be the responsibility of each contributor to make sure they pull the latest changes and do a local rebase before pusing their own changes to the remote. You can enforce such workflows in the git configuration.

#### forking and pull requests

You can follow the instructions [on github](https://help.github.com/articles/using-pull-requests/).

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

#### desktop clients

We have used the command line interface to git during the course, but graphical user interfaces are also [available](https://git-scm.com/download/gui/linux).

#### remote hosting options, pros and cons

To collaborate you need to host your remote repo somewhere. If you are not going to set up your own then you need to find a hosting option. The following options are all excellent and widely used choices:
* [github](https://github.com)
* [gitlab](https://about.gitlab.com/)
* [bitbucket](https://bitbucket.org/)

#### git extensions - for special needs

* [git-annex](https://git-annex.branchable.com/walkthrough/): dealing with large files
* [libgit2](https://libgit2.github.com/) and [libgit2-backends](https://github.com/libgit2/libgit2-backends) - [how to](http://blog.deveo.com/your-git-repository-in-a-database-pluggable-backends-in-libgit2/) store your git objects in databases, for example
* using [dropbox as your remote](https://github.com/anishathalye/git-remote-dropbox) - note: this is not the same as keeping your repo in the dropbox folder
* create your own remotes using [remote-helpers](https://www.kernel.org/pub/software/scm/git/docs/gitremote-helpers.html)


### using git to gain insight

Using [gource](http://gource.io/) to visualise repo development. The repository is displayed as a tree where the root of the repository is the centre, directories are branches and files are leaves. Contributors to the source code appear and disappear as they contribute to specific files and directories. [Example](https://www.youtube.com/watch?v=P_02QGsHzEQ).

### what next?

If you want to deepen your understanding you can consider reading [git from the bottom up](http://ftp.newartisans.com/pub/git.from.bottom.up.pdf).
