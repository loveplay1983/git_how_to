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
   
# checking status before commmit
4. git status           -> check the status of files
   git diff file_name   -> making sure the difference of files
   git add file_name 
   git status
   git commit -m "now we are good to go"

# 
5.   
   

   

   

   

