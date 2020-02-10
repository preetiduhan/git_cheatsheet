# git_cheatsheet

CONFIGURING

to configure git:
   git config --global user.name "FirstName LastName"
   git config --global user.email "shortname@country.ibm.com"
   git config --global core.editor vim
   git config --global gitreview.username "shortname"  (e.g. "edmondsw")

 

to make a short alias for a command:

git config --global alias.<alias_name> '<aliased command>'
e.g.
git config --global alias.tree 'log --oneline --decorate --graph --all'
...and hereafter you can just type:
git tree

 

CLONING

to clone the git repository locally:
   git clone https://git.openstack.org/openstack/<projectname>.git  (for OpenStack)

(Tip: You can get a 'git clone' command from the gerrit server via: Projects => List, find and click on your project.)

 

BRANCHES

to checkout an existing branch:
   git checkout <branch>

 

to create a new branch based on current branch and check it out:
   git checkout -b <branch>

 

to list branches (will also indicate which is current with an asterisk):

   git branch [-a]

 

to list branches that have merged:
   git branch --merged

 

to list branches that have NOT merged:
   git branch --no-merged

 

to delete a branch:
   git branch -d <branch>

 

to force delete a branch:
   git branch -D <branch>

 

to pull down the latest merges to the current branch from a specified branch in a specified repository (e.g. origin):
   git pull --ff-only <repository> <branch>

 

to pull down new branches from existing remotes:
   git remote update

 

to rebase the current branch from another:
   git rebase -i <from_branch>

 

to compare the current branch to another:
   git diff <branch2>

 

to compare 2 specific branches:
   git diff <branch1> <branch2>

 

to compare a specific file in the current branch to another:
   git diff <branch2> <file>

 

to view the status of the current branch:
   git status

 

HISTORY

to see the log message of the last commit [or a specific commit]

git log -1 <commit_hash>

 

to see a nice visual tree diagram of the commit history:

git log --oneline --decorate --graph --all

 

WORKING WITH COMMITS

to undo the previous commit but keep your changes:

    git reset --soft HEAD^

 

to remove a file's changes from a commit:
    git reset --soft HEAD^
    git reset HEAD <file>
    git commit -c ORIG_HEAD

 

to add the specified file to the current commit:
   git add <file>

 

to create a new commit and add all changed (but not new!) files to that commit:
   git commit -a

 

to update the latest commit:
   git commit --amend

 

to backport a commit:
   git checkout stable/<release_codename>
   git checkout -b <new_branch_name>
   git cherry-pick -x <commit_id>

Then resolve any merge conflicts and push the change up for review. As an alternative, there is a "Cherry Pick" button in gerrit that works when there isn't a merge conflict.

 

PATCHES

to create a patch file based on the diff of the current branch against another:

   git format-patch <branch> --stdout

 

REVIEW

to initialize git review (necessary for each project):
   git-review -s

 

to push up the current commit to gerrit for review:
   git-review (for OpenStack)
   git-review osee-master (for OSEE)

 

perform a dry run of git review, printing instead of running commands
   git-review -n (for OpenStack)
   git-review -n osee-master (for OSEE)

 

to pull down a change from gerrit:
   git-review -d <change-id>
or ???
   git fetch https://review.openstack.org/openstack/<proj> refs/changes/<id>/<id>/<patch_num> && git checkout FETCH_HEAD -b bug/<bug_num>
