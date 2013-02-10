#### [USING GIT](http://rogerdudler.github.com/git-guide/)

Local repository consists of three "trees" maintained by git.

The first is your Working Directory which holds the actual files. The second one is the Index which acts as a staging area and finally the HEAD which points to the last commit you've made.

**To see if git is installed**

	which git

**Create git repo n the current directory**

	git init

**Clone repo**

	git clone https://github.com/<github user name>/<project name>

**Clone project**

	git clone </path/to/my/project/>

**Create repo from command line

    curl -u 'USER:PASS' https://api.github.com/user/repos -d '{"name":"NAME OF REPO"}'
    git remote add origin git@github.com:USER/bootstrap-template.git
    git push origin master

**When using a remote server, the  command is**

	git clone username@host:/path/to/repository

**Create a new branch and switch to it**

    git checkout -b format_email

##### Add & commit
**Add files to the index. This is the first step in the basic git workflow**

	git add <filename>

**Or**

	git add *

**Use wildcards if you want to add many files of the same type**

    git add '*.txt'

**To actually commit these changes use to the HEAD**

	git commit -a -m "Initial commit of myproject"

**Changes are now in the HEAD of your local working copy. To send those changes to your remote repository, execute**

	git push origin <whatever branch you want to push your changes to>

**If you have not cloned an existing repository and want to connect your repository to a remote server, you need to add it to push your changes**

	git remote add origin <server>


##### Branches

Branches are used to develop features isolated from each other. The master branch is the "default" branch when you create a repository. Use other branches for development and merge them back to the master branch upon completion.

**To create a new branch named "feature_x" and switch to**

	git checkout -b feature_x

**To switch back to master**

	git checkout master

**Delete the branch again**

	git branch -d feature_x

**Branch not available unless you push to remote repo**

	git push origin feature_x

**Get status of branch**

    git status

**See log of commits**

    git log

**Reset project to previous commit**

    git reset --hard 1369471

**Post repo to github**

    git push https://github.com/<github user name>/<project name>

**Check for changes on GitHub and pull down any new changes**

    git pull origin master