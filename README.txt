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
   rm file_name     -> not allowed
   git rm file_name -> correct processing
   
   git checkout -- file_name  -> retrieve the file from .git(repository)

# 

   
    
