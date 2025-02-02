# Git How to's

Tim Stanford

This is my ever growing list of 'how to do' commands for git. This guide is not meant to be a definitive guide on git but rather a list of commands that are occassionally used and for future reference.

## Contents
- [Git How to's](#git-how-tos)
  - [Contents](#contents)
- [Cloning a remote repository locally](#cloning-a-remote-repository-locally)
  - [Clone an existing remote repository](#clone-an-existing-remote-repository)
  - [Clone an existing remote repository into a new directory](#clone-an-existing-remote-repository-into-a-new-directory)
- [Branches](#branches)
  - [List remote Branches](#list-remote-branches)
    - [Command:](#command)
    - [Output:](#output)
  - [List local branches](#list-local-branches)
    - [Command:](#command-1)
    - [Output:](#output-1)
  - [Create new local branch from master](#create-new-local-branch-from-master)
- [Commit Management](#commit-management)
  - [Undo last commit without undoing changes](#undo-last-commit-without-undoing-changes)
  - [Undo last commit throwing away changes](#undo-last-commit-throwing-away-changes)
  - [Revert a commit](#revert-a-commit)
- [Logs and History](#logs-and-history)
  - [View the history of the current branch](#view-the-history-of-the-current-branch)
  - [Show the changes in a particular commit](#show-the-changes-in-a-particular-commit)
  - [View a list of changed files for a commit](#view-a-list-of-changed-files-for-a-commit)
- [Working with previous commits](#working-with-previous-commits)
  - [View the entire repository at a current commit id](#view-the-entire-repository-at-a-current-commit-id)
  - [Create a new branch from a historic point](#create-a-new-branch-from-a-historic-point)
  - [View the history of a particular file](#view-the-history-of-a-particular-file)
  - [Do a blame on a particular file](#do-a-blame-on-a-particular-file)
- [Git server](#git-server)
  - [Set up a git server for hosting remote repositories](#set-up-a-git-server-for-hosting-remote-repositories)
  - [List the contents of a bare repository](#list-the-contents-of-a-bare-repository)
  - [Convert a normal git repository to a bare one](#convert-a-normal-git-repository-to-a-bare-one)
  - [Create a bare repository that is mirrored to another repository](#create-a-bare-repository-that-is-mirrored-to-another-repository)
  - [Convert a bare git repository to a normal one](#convert-a-bare-git-repository-to-a-normal-one)
  - [Export a repo as a bundle](#export-a-repo-as-a-bundle)
- [Pushing](#pushing)
  - [Push multiple branch commits to remote](#push-multiple-branch-commits-to-remote)
- [Confirming what will be pushed](#confirming-what-will-be-pushed)
  - [See what needs to be pushed to remote](#see-what-needs-to-be-pushed-to-remote)
  - [Remove untracked files](#remove-untracked-files)
- [Tags](#tags)
  - [Creating a tag](#creating-a-tag)
- [Undoing work](#undoing-work)
  - [Reset a local branch to match the remote branch, throwing away changes.](#reset-a-local-branch-to-match-the-remote-branch-throwing-away-changes)
- [Squash commits](#Squash-commits)
  - [Squash local commits. local repository only has two commits and normal squash fails](#squash-local-commits-local-repository-only-has-two-commits-and-normal-squash-fails)
  - [Squash remote commits](#Squash-remote-commits.)

___

# Cloning a remote repository locally

In SVN this is known as checking out. Checkout in git means to switch a branch

## Clone an existing remote repository

This command will download the git repository into the directory ng-infx. The directory will be created

Command:

    git clone git@git.internal.standardlife.com:wbp/infrastructure/ng-infx.git

## Clone an existing remote repository into a new directory

If you wish to clone into an alternative directory specify the directory name after the git repo url. e.g.

Command:

    git clone git@git.internal.standardlife.com:wbp/infrastructure/ng-infx.git ng-infx2



# Branches

## List remote Branches

### Command:
    git branch -r

### Output:

    origin/1.0.0-hotfix
    origin/Diagnostics
    origin/HEAD -> origin/master
    origin/Java11_DI_Upgrade
    origin/RepointToSplunkProd
    origin/add_v3-ci_and_v3-qa_environments_to_rebuild
    origin/apache_conf_deployment
    origin/feature-AppServerRefreshForUAT2
    origin/master

## List local branches

### Command:
    git branch

### Output:
    * feature_WBPTECH-803_DeployBoxRefresh
    master

## Create new local branch from master

    git fetch origin
    git checkout -b mybranchname master

Create the same branch on the remote:

    git push -u origin head 




# Commit Management

## Undo last commit without undoing changes

    git reset HEAD^

## Undo last commit throwing away changes

    git reset --hard HEAD^

## Revert a commit

This is different from git reset. It creates a record that the commit was reverted. This is the preferred way to work when pushing to a remote server.

    git revert [commitid]




# Logs and History

## View the history of the current branch

    git log

Output:

    commit dd6a51f8ce9e9744904225e036826b55739eb435
    Merge: 7955909 1091860
    Author: slde99 <tim_stanford@standardlife.com>
    Date:   Thu May 30 13:59:43 2019 +0100

    Merge branch 'master' of git.internal.standardlife.com:wbp/infrastructure/ng

    commit 79559090a47d38f24f989d9d1007377d77fba22f
    Author: slde99 <tim_stanford@standardlife.com>
    Date:   Thu May 30 13:59:32 2019 +0100

    added wait after requesting new policy


To see the log of the branch with one line per commit use the --oneline argument

    git log --oneline

Output:

    dd6a51f Merge branch 'master' of git.internal.standardlife.com:wbp/infrastructur
    7955909 added wait after requesting new policy
    1091860 Update rhel-commands.md
    9a8dbf5 test script for sven to run on vccontroller
    a84d9f3 Update rhel-commands.md
    04b3309 Added some support documentation
    dcb43bf Merge branch 'WBPTECH-621-ProductionJava11Release' into 'master'
    2bc2590 WBPTECH-621 Template configuration updates for Java 11 release
    d25b0dd update the relative path for the prod ssh keys copy

## Show the changes in a particular commit

You need to get the commit id using `git log`

    git show [commit id]

Example:

    git show 9a8dbf5bc96a9e883e3151f5fcd21b504207f5e8

Output:

    commit 9a8dbf5bc96a9e883e3151f5fcd21b504207f5e8
    Author: slde99 <tim_stanford@standardlife.com>
    Date:   Wed May 29 15:16:11 2019 +0100

        test script for sven to run on vccontroller

    diff --git a/env_vars/v3-sventest.yaml b/env_vars/v3-sventest.yaml
    new file mode 100644
    index 0000000..c9a0a4b
    --- /dev/null
    +++ b/env_vars/v3-sventest.yaml
    @@ -0,0 +1,10 @@
    +vsphere_host: 10.40.40.41 # Primary
    +zone_dc: VebnetDataCenter1
    +network_netmask: 24
    +disk_gb: 50
    +machine_list:
    +
    +   - { hostname: "TimTestVM1",     vm_template: "app_rc82_1t_182",       esxi_h
    +   - { hostname: "TimTestVM2",     vm_template: "app_rc82_1t_182",       esxi_h
    +   - { hostname: "TimTestVM3",     vm_template: "app_rc82_1t_10",        esxi_h
    +   - { hostname: "TimTestVM4",     vm_template: "app_rc82_1t_10",        esxi_h
    d

## View a list of changed files for a commit

    git show --stat [commit id]

Example:

    git show --stat 9a8dbf5

Output:

    commit 9a8dbf5bc96a9e883e3151f5fcd21b504207f5e8
    Author: slde99 <tim_stanford@standardlife.com>
    Date:   Wed May 29 15:16:11 2019 +0100

        test script for sven to run on vccontroller

    env_vars/v3-sventest.yaml | 10 ++++++++++
    svens_vm_test.sh          | 44 ++++++++++++++++++++++++++++++++++++++++++++
    2 files changed, 54 insertions(+)




# Working with previous commits

## View the entire repository at a current commit id

This checks out in a detached head state, meaning that changes cant be committed without getting lost. This allows you to view the repository as it was when that commit was made. This could be to replicated a system from a historic point in time to fix a bug.

    git checkout [commit id]

## Create a new branch from a historic point

You will checkout a specific commit id and create a new branch. Commits made will be made to the new branch.

    git checkout [commit id] [new branch name]

## View the history of a particular file

    git show -p [filename]

## Do a blame on a particular file

    git blame [filename]

# Git server

## Set up a git server for hosting remote repositories

ssh to the remote server

    ssh playdeploy

Create a new user called git

    sudo -s adduser

Setup .ssh directory

    sudo -s -u git
    cd ~
    mkdir .ssh
    cd .ssh
    touch authorized_keys

Add public keys of users who wwill have access to git

    echo 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCiOlY88llVXFHW8e0+vV+tEWxhsGhbQM81H64JEUmguounf5ycAZuVVF6dXcuQbOS+1mNHBHWgND0DkOQnKyemhUD/0QXRKgHWbNZPafKfzYJ0+PaNo8cNJQ1efOJQd5iHzp8ImJGUUTlVj/7dOb1/bX60y25JfPfED8ZrzG5ezlxmJ/5OLzZnGOzzIKjD6xGblu/dRlxxI+VHPTVxRPCg7aCPw5JD2oa12NnwfCF7KiQfmPUpmWt8cal1T7ign3t4NucvmeIep83w5WMVC5MZcVyGXzeWzxH+c1QlE/QiDXRqx9v8axWFBKVFaz10Yp1ejsB5mRKFQm0QjSDomLep slde99@timsmachine' >> authorized_keys

Create a directory structure for the bare git repositories

    sudo mkdir -p /srv/git

Change ownership of the git directory

    sudo chown git:git /srv/git

Initialise a bare git repository using the following

    cd /srv/git/
    mkdir project1.git
    cd project1.git
    git init --bare

On the client side. clone the repository

    git clone git@playdeploy:/src/git/project1.git


Possible git server front ends

* Gitea    https://gitea.io
* Gogs     https://gogs.io/

## List the contents of a bare repository

    git ls-tree -r HEAD --name-only

Example output:

    test.txt
    tim1/test.txt

## Convert a normal git repository to a bare one

Move the .git directory of the normal git repository to a new directory outside of the repository.

    cd myrepository
    mv .git ../myrepository.git
    cd ..
    rm -rf myrepository
    cd myrepository.git
    git config --bool core.bare true

## Create a bare repository that is mirrored to another repository

    git clone --mirror https://primary_repo_url/primary_repo.git


## Convert a bare git repository to a normal one

You need to move all directories in the bare repository to the .git directory. Then tell git it is a normal repository. Then do a hard reset to bring back the files.

    cd myrepository.git
    mkdir .git
    mv !(.git) .git/
    git config --bool core.bare false
    git reset --hard

## Export a repo as a bundle

You can export a repository as a bundle file. The use case for this is when you've lost network connectivity and need to share your work with a coworker. The bundle file can be merged into a coworkers branch.

    git bundle create repo.bundle HEAD master

The other developer can fetch the master branch from the bundle file into their repository as a new branch called "other-master"

    git fetch ~/repo.bundle master:other-master

# Pushing

## Push multiple branch commits to remote

You may be working on multiple branches and have done several commits to different local branches. It is possible to push all changes to the remote with one command, rather that remember what branches you've commited to.

    git push --all




# Confirming what will be pushed

## See what needs to be pushed to remote

    git cherry -v

or:

    git diff --stat --cached origin/master

or:

    git push --dry-run

## Remove untracked files

See what will be remove first:

    git clean -n

Then to delete for real..

    git clean -f

# Tags

## Creating a tag

Create a tag

    git tag -a 1.1.5 -m "hotfix for live release"

create a tag from a specific commit

    git tag -a v1.2 9fceb02

Tags aren't automatically pushed with a git push. You have to explicitly push the tag

    git push origin 1.1.5

or push all local tags:

    git push origin --tags

# Undoing work

## Reset a local branch to match the remote branch, throwing away changes.

    git fetch origin
    git reset --hard origin/master

If you want to save your changes prior to doing this:

    git commit -a -m "Saving my work, just in case"
    git branch my-saved-work


## Squash commits



### Squash local commits. local repository only has two commits and normal squash fails

Lets say you have 2 commits that you want to squash locally into one commit

    git log --pretty=oneline
    
    c2d22944c28af37b8827a33764d0199d57c62cef (HEAD -> WOLF-547) x
    fd7e7c10fb728445a8646c4573b81e78768affe3 (origin/WOLF-547) WOLF-547 New tab "Requests" added to the BacsRecalls View to show Manual Requests raised today.
	

Start an interactive rebase for the 2 most recent commits.

    git rebase -i HEAD~2
    
    pick fd7e7c10 WOLF-547 New tab "Requests" added to the BacsRecalls View to show Manual Requests raised today.
    pick c2d22944 x
    
This will open vi editor. Choose one of the commits that you would like to `squash` into the other. Do this by replace `pick` with `squash` or just `s`

    pick fd7e7c10 WOLF-547 New tab "Requests" added to the BacsRecalls View to show Manual Requests raised today.
    s c2d22944 x
    
Save and exit with `:wq!`

Another vi instance will open allow you to edit the commit message for the single commit. Anything starting with # will be ignored.

Save and exit with `:wq!`

### Squash remote commits.

Do a git pull. Make sure everything is up to date and correctly merged locally.

Follow the previous section to squash local commits.

Do a forced git push

    git push --force





    

	





