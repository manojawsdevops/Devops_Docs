git init
git add filename
git commit -m "message"
git branch -m main
git remote add origin REPO URL
git push -u origin main

type username
password

git log -----------it will show the all logs including last commit id and commit message
git commit --amend ----------it will help to change last commit message
git push origin main --force-----------it will apply in github

git pull --------------------it will help to pull the latest changes in remote repo
git clone -------------------it will help to fetct all the data from remote repo
git init --------------------it will initiaztion the repo in local system
git clean -------------------Removes untracked files from the working directory. This is the logical counterpart to git reset, which (typically) only operates on tracked files.

Central Version Control System (CVCS) 
​
In CVCS, the central server stores all the data. This central server enables team collaboration. It just contains a single repository, and each user gets their working copy. We need to commit, so the changes get reflected in the repository. Others can check our changes by updating their local copy. 


we have working copy:
repository
update and commit

Distributed Version Control System (DVCS) 

In DVCS, there is no need to store the entire data on our local repository. Instead, we can have a clone of the remote repository to the local. We can also have a full snapshot of the project history.  


Working copy------------------------>commit and commit-------------------> Repository------------------push and pull



What is version control? 

What is a “version control system”? 

Version control systems are a category of software tools that helps in recording changes made to files by keeping a track of modifications done to the code. 

example is Git, Helix core, Microsoft TFS,

what is repo:
A repository contains all of your project's files and each file's revision history. You can discuss and manage your project's work within the repository.

The local repository is a Git repository that is stored on your computer.

The remote repository is a Git repository that is stored on some remote computer.

                                       Local                                             Main serer 
                                       






