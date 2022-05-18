# redata-docs
This is a repository that provides general documentation for software pertaining to ReDATA, the University of Arizona Research Data Repository. It provides links to other Re DATA software packages in Github and readthedocs.org. 


The following is how to create a copy at your own environment at your github and readthedocs.org. 

### 1. First create your desired directory and Git clone it to your local directory.
%git clone git@github.com:UAL-RE/redata-docs.git

### 2. Remove the cloned local repository from its remote association.
After you clone the git repository. Remote configuration is saved in ".git" directory. You can see "config" on ".git" for the remote and branch info. 
so you need to run "git remote rm orgin" to remove remote association. You can see the changes in "config" (remote "origin" and branch "main" are removed). You can run "git remote -v" to list all remote repositories connected to the local repository.

% git remote -v  

% git remote rm origin 

% git remote -v 



### 3. Create a new github repository and connect it with your local repository.
-- Go to your github to create a new repository. 
 
-- Connect this local repository to the new repository, and then verify its remote.

% git remote add origin git@github.com:hanmgmt/test-docs2.git

% git remote -v 
 
-- push the local repository to the new repository.

% git push branch -M main

% git push -u origin main


### 4. Read the Docs: import a repository
-- Create an account in readthedocs.org 

-- Import a Repository by click the "refresh" button. 

-- Configure and build a version

-- Wait a few minutes and see the compile message and "build completed" message. 

-- Click the "View Docs" for the latest version (HTML) with the URL. 


