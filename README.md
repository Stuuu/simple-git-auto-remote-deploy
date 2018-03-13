# Simple git automatic remote deploy



# Steps to setup Automatic remote deploy

1. On Remote(Prod) create a new directory to house Git Repo and files for your application

    `git init — -bare`
    

2. Create hook that will listen for commit and place change in target project directory:

        cd directory_name
        cd hooks
        vi post-receive


3. In post-receive add the following lines being sure the `work-tree` points to your projects directory and the second points to the git directory created in step 1 out for your paths: 
	
        #!/bin/sh
        git --work-tree=/var/www/$project_directory/public_html --git-dir=/var/www/	$project_directory/git 	checkout -f


	Save

4. While still in /hooks make file executable with:

	`chmod +x post-receive`

3. Now on local machine

 	1. In blank directory that you want to use for local(dev) directory run the folling:

        Git init 
	2. add remote 
	
        git remote add prod ssh://$remoteuser@$remote-machine.com/var/www/$project_directory/git
	
     3. SCP down the existing project #there is probably a gitty'er way to do this part submit a PR and tell me the right way
     
       scp -r $user@your.server.example.com:/path/to/foo /home/user/Desktop/

# Adding local changes (1-3) and deploying to prod (4)

	1. Git add . 
	2. Git status 
	3. Git commit -m “message”
	4. Git push prod master
	
	
# To revert a commit on Prod(Master) run this on the remote

        git update-ref HEAD prior-hash-here

  
  
 
