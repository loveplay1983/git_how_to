* `PRIVATE SERVER`
    * On debian there is a possible issue with non-root ssh login
      https://forum.openmediavault.org/index.php?thread/2863-cannot-logon-with-other-user-than-root/
      
      
	* server side 
	  * create git user
	    ```
	    useradd -d /home/git -m git
	    ```
	  * swtich to `git` use and create private git directory
	    ```
	    su - git
	    cd ~
	    mkdir mygit
	    cd mygit
	    mkdir xuan.git
	    ```
	  * init `xuan.git`
	    ```
	    git init --bare
	    ```
	  * create `.ssh` and change permission
	    ```
	    cd ~
	    mkdir .ssh && chmod 700 .ssh
	    touch .ssh/authorized_Keys && chmod 600 .ssh/authorized_keys
	    ```
	  * copy `client side` pub key to `server side authorized_keys` list
	    ```
	    cat .ssh/id_rsa.pub | ssh user@123.45.56.78 "cat >> ~/.ssh/authorized_keys"
	    ```
	* Client side
	  * ssh-keygen
	    ```
	    cd ~
	    cd .ssh
	    mkdir mygit
	    cd mygit
	    ssh-keygen -t rsa
	    ssh-add .ssh/mygit/id_rsa
	    ```
	  * create and init
	    ```
	    git init
	    # git is the user name
	    git remote add origin ssh://git@ip_or_http_addr/yyy/zzz/your_git.git
	    ```
	  * YOUR NOW GOOD TO GO
