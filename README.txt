# install git 
1. sudo apt-get install git

# configure git
2. git config --global user.email "xxx@yyy.com"
   git config --global user.name "zzz"

# working directory and your first commit
3. mkdir dir_name
   cd dir_name
   
   git init
   vim README.txt       -> edit(the file your are reading)
   
   git add README.txt
   git commit -m "README.txt created"
   
   git add file1        -> when creating multiple files 
   git add file2 
   git add . | git add file1 file2 
   git commit -m "file1 file2 added"
   
# check status before commmit
4. git status           -> check the status of files
   git diff file_name   -> make sure the difference between current files and version control  
   git add file_name 
   git status
   git commit -m "now we are good to go"

# check the different versions
5. git log    -> check the git op log
   git log --pretty=oneline
   git reset --hard HEAD^    -> the latest record
   git reset --hard HEAD^^   -> the 2nd latest record
   git reset --hard commit_id_number  -> only the beginning of few are needed   
      
   git reflog -> check the git op full log

# working directory, repository and staging   
6. what is working directory? -> the directory or the path you are working now
   
   what is repository?        -> the .git folder which is hidden within your working dir
                                 including stage(index) and thte pointer "HEAD" which points
                                 to the different branches, in our case "master"

   what is staging?           -> the temporary field where you can add file by "git add file_name"
                                 commit or push it later when all files are done
                                 the .git or the repository(version control) uses staging to track
                                 the process of files

# diff current working files and latest version
7. git diff HEAD -- file_name

# retrieve the latest modifcation
8. git checkout -- file_name   -> before git add, retrieve the mod within your working dir
   
   git status
   git reset HEAD file_name    -> after git add, HEAD for the latest version
   git checkout -- file_name   -> now retrieve the modification within your working dir 
   
# delete content and restore mistakenly deleted files
9. git add file_name
   rm file_name     -> delete from local working dir
   git rm file_name -> remove from the staging 
   
   git checkout -- file_name  -> retrieve the file from .git(repository)

# **branches management**
A. create and merge 
  1. default branch `master`, `HEAD`->`master`->`commit`
  2. new branch `new`, `HEAD`->`new`->`commit`(the same commit of master commit)
  3. new branch development, `master`->old commit point, `new`->new commit point(on-going) 
     commit____commit____commit(master)
     commit____commit____commit____commit____commit(new)
  4. merge `master` and `new` branches, move `master` commit point to the current `new` commit point
  
  a. git checkout -b new   -> create and switch to new branch
     
     git branch new        -> same as above
     git checkout new

  b. git branch            -> check current branch
     
     git add files;git commit -m 'xxx' -> add file to current branch staging and commit it
     
     git checkout master;cat file_name -> switch back to master branch and observe the change we have made for new branch
  
  c. git merge new         -> merge the current branch and master branch
     git branch -d new     -> delete new branch after merge it into master 
     
  d. git switch -c new     -> another way of creating and switching to new branch

B. handle conflict
  ```
  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 2 commits.
    (use "git push" to publish your local commits)
  
  You have unmerged paths.
    (fix conflicts and run "git commit")
    (use "git merge --abort" to abort the merge)
  
  Unmerged paths:
    (use "git add <file>..." to mark resolution)
  
  	both modified:   readme.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  ``` 
  __check file content__ 
  __when there is merge conflict, check the file content and make the modifcation decision__
  ```
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  <<<<<<< HEAD
  Creating a new branch is quick & simple.
  =======
  Creating a new branch is quick AND simple.
  >>>>>>> feature1
  ```
  
  __check the git log after merge master with dev branch, dev branch deletion__
  ```
  git log --graph --pretty=oneline --abbrev-commit
  git branch -d feature1

C. branch management strategy
  __it is not recommended to use `fast forward` in branch merge which will cause the git log loss of the branch info__
  ```
  git merge --no-ff -m "merge with no-ff" dev 

  git log --graph --pretty=oneline --abbrev-commit
  *   e1e9c68 (HEAD -> master) merge with no-ff
  |\  
  | * f52c633 (dev) add merge
  |/  
  *   cf810e4 conflict fixed
  ...
  ```
  __with --no-ff argument the git log has its branch info even after the branch deletion__

D. Bug 
  __git stash save the current working stage while fixing the bug__
  ```
  $ git status
  On branch dev
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	new file:   hello.py
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt

  git stash   # save the current working stage
  ```
   
  __check the status then fix the bug__
  ```
  $ git checkout master
  Switched to branch 'master'
  Your branch is ahead of 'origin/master' by 6 commits.
    (use "git push" to publish your local commits)
  
  $ git checkout -b issue-101
  Switched to a new branch 'issue-101'
  
  $ git add readme.txt 
  $ git commit -m "fix bug 101"
  [issue-101 4c805e2] fix bug 101
  1 file changed, 1 insertion(+), 1 deletion(-)
  
  $ git switch master
  Switched to branch 'master'
  Your branch is ahead of 'origin/master' by 6 commits.
    (use "git push" to publish your local commits)
  
  $ git merge --no-ff -m "merged bug fix 101" issue-101
  Merge made by the 'recursive' strategy.
   readme.txt | 2 +-
   1 file changed, 1 insertion(+), 1 deletion(-)
  ```

  __check the stash list, find and restore the stash data__
  ```
  $ git stash list
  stash@{0}: WIP on dev: f52c633 add merge
  $ git stash apply stash@{0}
  git stash apply   - stash data remain
  git stash drop    - delete the stash data
  

  git stash pop     - restore and delete at the same time
  ```

  __dev branch has the same bug as master branch__
  ```
  $ git branch
  * dev
    master
  $ git cherry-pick 4c805e2
  [master 1d4b803] fix bug 101
   1 file changed, 1 insertion(+), 1 deletion(-)
  ```

E. feature 
F. team work
G. rebase
