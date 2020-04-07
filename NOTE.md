###### Current git version I am using is 2.17
###### Git 2.23 and later version introduces 2 new commands ment to replace the common use of `git checkout` to `git switch` and `git reset` to `git restore`

```
# old version
git checkout b           # switch to branch b
git checkout -- f        # copy f from the stage to the working tree
git checkout b -- g      # copy f from branch b
git checkout HEAD f      # this will alter your index, too!

# new version
git switch my-branch              # same as git checkout my-branch
git switch -c my-branch           # same as git checkout -b my-branch
git switch -c my-branch HEAD~3    # branch off HEAD~3
git switch --detach HEAD~3


git restore --source HEAD~3 main.c  # --worktree is implied

rm -f hello.c
git restore hello.c

git restore '*.c'

git restore --staged hello.c    # same as using git reset

git restore --source=HEAD --staged --worktree hello.c   # same as git checkout
```
~    
