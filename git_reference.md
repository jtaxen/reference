REBASING
=======

Updating changes at origin
=========================
If I have made changes from one branch point, and someone else has made another change from the 
same point and merged it into master before I have, a rebase must be done.


local:
master: A - B - C - D - E

origin/master:
A - B - C - F - G

1. First, be at master and move the changes to a new branch:

```
git branch temp_b
```

local:
master: A - B - C - D - E
                 \        
temp_b:           D - E

2. Remove the commits from master that are not present at origin/master:

```
git reset --hard HEAD~2
```

local:
master: A - B - C
                 \        
temp_b:           D - E

3. Pull the changes from origin/master:

```
git pull origin
```

local:
master: A - B - C - F - G
                 \        
temp_b:           D - E

4. Checkout the temporary branch and rebase with respect to master:

```
git checkout temp_b
git rebase master
```
local:
master: A - B - C - F - G
                         \
temp_b:                   D - E

5. Merge the branch into master, and it is done and ready to be pushed:

```
git checkout master
git merge temp_b
git push origin HEAD:refs/for/master
git branch -d temp_b
```

local:
master: A - B - C - F - G - D - E

Change older commit
==================

This explains how to make changes to a commit that is not the latest one. In this example, changes
need to be done to the commit C, with * marking commits containing this change.

local:
master: A - B - C - D - E

1. Make a rebase with respect to a commit somewhere earlier than the one that should be changed:

```
git rebase -i HEAD~4
```

This opens a text editor with a list of those commits that can be changed. 

2. Choose the commit C and change the word "pick" to "edit". Save and close the document.

3. Make changes and add them. Amend them to the commit:

```
git add <file>
git commit --amend
```

4. When done, apply the changes:

```
git rebase --continue
```

4. Resolve conflicts if needed.

Show changes and diffrences:
===========================

To compare two branches:

```
git diff <branch_1> <branch_2>
```

The diff command can also be used for comparing different commits. To see the number of 
changes/additions/removals, use the ```--stat``` flag:

```
git diff --stat HEAD~2 ab5b608
```

Merging:
=======

To find out whether a branch has been merged, use ```git branch --merged```. Without any argument
it lists the branches merged into HEAD. To see which branches have been merged into a specific
branch, for example master, do:

```
git branch --merged master
```

Other useful flags are:

# ```--no-merged``` - see which branches have not been merged.
# ```-a``` - show both local and remote branches.
# ```-r``` - show only remote branches.

Checkout old commits:
====================

Script for stepping through commits one by one:

```
for commit in $(git rev-list branch_name ^commit_hash^ --reverse)
```
