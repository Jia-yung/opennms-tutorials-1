## Getting Started with GIT

You should create your own account on GitHub and use this to store your exercises. 
Checking your work into the repo will also allow your tutor to look at your work and address any issues. 

This section will teach you a little bit about git and how to fork a copy of this repository into your own github account.

You will then be able to clone your fork locally.

After this you can then proceed to doing the exercises in [session1](../main/session1/).

### Introduction to GIT
Professional developers are proficient at using version control systems.
Many version control systems (each with their own benefits and drawbacks e.g CVS, Subversion, git) have been popular over the years. 
Presently one of the most popular, git, was developed by Linus Torvalds to help with the collaborative development of the Linux Kernel.

In recent years many open source projects have migrated their code base to github (https://github.com) which supports a collaborative workflow for team development and sharing of source code using git. 

The principle advantage of git over other version control systems is that it is completely distributed. When you use git you clone a complete local copy of the repository you are cloning (usually referred to as the origin).
You can develop code or modify files and save your changes in your local repository completely off line. 
At a later stage you may wish to push your changes to the on line repository or pull changes others have made into your local copy. 

There are many on line tutorials on using git and it will be worth while spending some time on these to get proficient. e.g.
* https://try.github.io/ Resources to learn Git
* https://guides.github.com/introduction/git-handbook/ Git Handbook 
* https://learngitbranching.js.org/ provides a very useful interactive tutorial on branching and merging.
 
Many IDE's  support git natively, but it is very important to learn to use the git command line independently of the IDE so that you have more control over what is happening.

Using git successfully with a team can be complex but fortunately you only need to master a few commands to work on your own project
```
git clone  (a command to clone your local copy of the on line repository)
git status (a command to tell you what is the state of your local repository e.g are their any changes to commit and push)
git pull  (a command to pull the latest changes from the remote repository into your local copy)
git add --all (a command to stage all of the current changes ready for a commit)
git commit -m 'my commit message' (a command to commit changes to your local repository)
git push (a command to push your latest commits up to the remote repository)
```

### IMPORTANT GitHub Security
Github no longer accepts a simple username and password for accessing accounts. 
Please see the page on [Github Security](../main/githubsecurity.md) to see how to set up certificates to access your github account from your pc.

### Forking the tutorial repo
You could just clone the master repo and work on the clone locally. 
However you do not have write permissions to this repo and so you couldn't save (or push) any changes or work you have added.
Therefore, to be able to use the examples and save your own work, it will be better to create a copy (called a fork) of this repository in your own github account where you will be able to push and save your changes on line.

You should open your own personal github account and FORK this repository into your own account. 
This will give you your own copy to work with and a backup of your work on github.
PLEASE NOTE, while github is very reliable, you should also keep a local backup copy of your repo in case anything goes wrong.

To create a fork of this repository
1. sign in to your own github account
2. navigate to this repository
3. click the FORK icon

![alt text](../main/docs/images/ForkingARepo.png "Figure ForkingARepo.png")

you can understand the process by reading these documentation examples.
https://help.github.com/articles/fork-a-repo/

### checking out your own fork

Having forked the repository, go to your own github account and clone the repository into your own workspace on your machine. 
Rather than just clone the repository into a workspace on your IDE, it is good practice to create a separate folder on your local machine where you will clone your remote repositories. 
You can import separate projects from this clone into your IDE workspace as you need to work on them.

Create a git repo folder on your local drive and clone your fork of opennms-tutorials-1 into it.

DO NOT check out your repository onto a network (e.g. U:) drive or a One Drive location. 
The time latency in these drives can cause git to fail.

I usually create a git repository close the the root of the C: drive (e.g. C:/devel/gitrepos/<my repo>)

```
mkdir gitrepos
cd gitrepos
git clone https://github.com/ {your github id }/opennms-tutorials-1.git
```
Important:  if using SSH keys use
```
git clone  git@github.com:{your github id }/opennms-tutorials-1.git
```

You should now have a clone of your fork in your gitrepos directory
gitrepos/opennms-tutorials-1


### hidden files .git and .gitignore
You should set the view on your windows file explorer to show hidden files and file extensions. 
This will allow you to see git and IDE specific files which are otherwise hidden.

In particular, you will see that the top level folder of the repository contains a hidden .git folder.
This is where git stores all of the branches, tags,  versions and changes to your repository. 
The rest of the files in the folder are the currently checked out versions of your code.

You will also notice that many of the projects in this repo have a .gitignore file.
This tells git to ignore certain directories or files when committing changes.
.gitignore files inherit from .gitignore files further up the class path. This allows you to have a generic .gitignore and a more specific one in a nested folder to specify project specific files you don't want to check in in. 

It is VERY important to ensure that, in particular 'target', directories are NOT checked into git as this would fill your repository up with unnecessary class and jar files.

You should also ensure that in most cases IDE specific sub folders and files are not checked in to git as this will cause confusion if you change or upgrade your IDE. Your ide will read the maven pom.xml file and recreate these folders locally if necessary.

The example [.gitignore](../main/.gitignore)  should be suitable for most purposes and should be copied into the top level of your git repository.

### Syncing with the upstream repo
I will be adding stuff to the upstream repo each session and you should be able to pull these into your local repo using the procedure described below.

PLEASE DO NOT CHANGE ANYTHING IN YOUR LOCAL REPO EXCEPT IN myPracticeCourseWork.
 this will allow merges to go smoothly.

you can see which remote repositories are referenced in your local repo using
```
$ git remote -v
origin  https://github.com/{ your github id}/opennms-tutorials-1.git (fetch)
origin  https://github.com/{ your github id}/opennms-tutorials-1.git (push)
```
if you are using SSH keys this will be
```
$ git remote -v
origin  git@github.com:{ your github id}/opennms-tutorials-1.git (fetch)
origin  git@github.com:{ your github id}/opennms-tutorials-1.git (push)
```

To sync with the upstream repo you need to add another remote repository
```
$ git remote add upstream https://github.com/gallenc/opennms-tutorials-1.git
```
NOTE even if you are using SSH to acces your repo, use https to access the upstream repo because you do not need a password or certificates to pull a public repo.

To see the upstream repositories use
```
$ git remote -v
origin  https://github.com/{ your github id}/opennms-tutorials-1.git (fetch)
origin  https://github.com/{ your github id}/opennms-tutorials-1.git (push)
upstream        https://github.com/gallenc/opennms-tutorials-1.git (fetch)
upstream        https://github.com/gallenc/opennms-tutorials-1.git (push)
```
if you are using SSH this will be
```
$ git remote -v
origin  git@github.com:{ your github id}/opennms-tutorials-1.git (fetch)
origin  git@github.com:{ your github id}/opennms-tutorials-1.git (push)
upstream        https://github.com/gallenc/opennms-tutorials-1.git (fetch)
upstream        https://github.com/gallenc/opennms-tutorials-1.git (push)
```

Note that git calls the github repository which your repository is linked to 'origin'.
This is the respository on github where where push commands normally send the changes.
The 'upstream' repository is an alternative repository from which you pull additional content for merging with your work.

Having made these changes you can now keep your own fork of opennms-tutorials-1 synced with the class examples in the upstream repository using a few Git commands.

1. Fetch the branches and their respective commits from the upstream repository. 
Commits to master will be stored in a local branch, upstream/master.
```
git fetch upstream
From https://github.com/gallenc/opennms-tutorials-1
 * [new branch]      master     -> upstream/main
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 12 (delta 3), reused 12 (delta 3), pack-reused 0
Unpacking objects: 100% (12/12), done.
From https://github.com/gallenc/opennms-tutorials-1
   ddd9643..bd85c0d  master     -> upstream/main
```

2. Check out your fork's local main branch.
```
git checkout master
Switched to branch 'master'
```
3. Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.
```
git merge upstream/master
Updating ddd9643..bd85c0d
Fast-forward
 README.md                           |  89 +++++++++++++++++++++++++++++++++++-
 docs/images/ForkingARepo.png        | Bin 0 -> 44529 bytes
 maven-setup/README.md               |  44 ++++++++++++++++++
 week1/README.md                     |   7 +++
 week1/maven-test-exercise/README.md |  12 ++++-
 5 files changed, 149 insertions(+), 3 deletions(-)
 create mode 100644 docs/images/ForkingARepo.png
 create mode 100644 maven-setup/README.md
 create mode 100644 week1/README.md
```
Your local master branch should now contain all the changes from the upstream repository.

4. You should push these changes to your own repository on github.

```
git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean

git push
Counting objects: 12, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (10/10), done.
Writing objects: 100% (12/12), 44.69 KiB | 0 bytes/s, done.
Total 12 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To https://github.com/gallenc-test/opennms-tutorials-1.git
   ddd9643..bd85c0d  master -> master

git status
On branch master
Your branch is up-to-date with 'origin/main'.
nothing to commit, working directory clean

```

## Summary
To synchronise your repository with the upstream use the following commands

If you have not set up the upstream repo
```
git remote add upstream https://github.com/gallenc/opennms-tutorials-1.git
```
Once the upstream is set use

```
git fetch upstream
git checkout main
git merge upstream/main
git push

```


## further reading

you should get familiar with the process for syncing a fork which means pulling down changes or updates from my master repository into your own fork.

https://help.github.com/articles/syncing-a-fork/

https://help.github.com/articles/configuring-a-remote-for-a-fork/

