# [Learning python/django](http://www.chrislkeller.com/pages/learning-pythondjango)

In a quest to learn how to use python within the django framework, the most difficult thing was the development environment, and getting to the point where I could <del>play</del> learn, practice and experiment. Here are some steps that I took to get to that point.

I’ll add to this as I can, but mostly I’m using it as a handy resource that I can access while continuing to learn.

#### NEWBIE MISTAKES

A [great roundup](https://code.djangoproject.com/wiki/NewbieMistakes) on the django docs site on mistakes that newcomers can make, and possible solutions.

#### USEFUL SNIPPETS

[DRY method](http://djangosnippets.org/snippets/1563/) of declaring django fieldsets based on model information.

#### CREATE DJANGO PROJECT IN MY MAC OS DEV ENV

Cribbed from my notes and this [blog post](http://www.jeffknupp.com/blog/2012/02/09/starting-a-django-project-the-right-way/).

- Download [Postgres.App](http://postgresapp.com/)

- Create new database in [local Postgres DB](http://od-eon.com/blogs/calvin/postgresql-cheat-sheet-beginners/)

		createuser -U KellerUser DjangoKeller -P

		createdb -U DjangoKeller -E utf8 -O DjangoKeller madsafety_db -T template0

		dropdb mydb madsafety_db

- Create new virtual environment

        mkvirtualenv (ENV_NAME)

* Activate environment

		workon (ENV_NAME)

* Install django and initial packages

		pip install django, south, yolk, fabric, mechanize, BeautifulSoup

* Create django project

		django-admin.py startproject (PROJECT_NAME)

* Add south to NSTALLED_APPS in settings.py

* Add db informaton & 'HOST': 'localhost', to your settings.py file

* Sync the database. This installs South from the beginning, meaning migrations to our own apps will use South

		python manage.py syncdb

* Create App

		python manage.py startapp (MY_APP)

* Creates migration file for future changes

		python manage.py schemamigration myapp --initial

* Migrate the changes

		python manage.py migrate myapp

* Create git repo n the current directory

		git init

* Stage all of our files to git to be committed

		git add .

* Commit the files

		git commit -a -m 'Initial commit of myproject'

* Create fabfile.py to pull changes from development master branch, run any migrations you've made, run your tests, and restart your webserver.

		from fabric.api import local
			def prepare_deployment(branch_name):
				local('python manage.py test myapp')
				local('git add -p && git commit')
				local('git checkout master && git merge ' + branchname)

			def deploy():
				with lcd('/path/to/my/prod/area/'):
					local('git pull /my/path/to/dev/area/')
					local('python manage.py migrate myapp')
					local('python manage.py test myapp')
					local('/my/command/to/restart/webserver')

* run the fab commands

		fab prepare_deployment:(MY_BRANCH_NAME_HERE)
		fab deploy

----

#### CREATING A DJANGO PROJECT ON WEBFACTION USING PYTHON 2.7, VIRTUALENV AND VIRTUALENVWRAPPER

WebFaction offers a one-click install to get a django project off the ground.

I've been using virtualenvwrapper locally to learn how to use the web
framework. I wanted the same thing with WebFaction. I like trying to figure
out things I am still learning to grasp I guess.

I was finally able to piece together how to go from zero to Congratulations on
your first Django-powered page … after about 2 ½ hours.

Here's what I did, with help from blog posts by [Jamie
Curle](http://jamiecurle.co.uk/blog/webfaction-installing-virtualenv-and-
virtualenvwrapper/), [Neil Lyons](http://neillyons.co/articles/how-to-install-
virtualenv-on-webfaction/) and "[zoe.vc](https://www.zoe.vc/about-2/)."

**Jamie Curle helps us set WebFaction's default python to version 2.7**

    # check your python version
    python -V

    # edit .bashrc
    vi $HOME/.bashrc

    # set the default python to 2.7
    alias python=python2.7

    # now :wq from vim and reload
    sourcesource .bashrc

    # make the python2.7 lib folder
    mkdir $HOME/lib/python2.7

**Neil Lyons helps us to install packages where we don't have permission to**

    #using easy_install as you can specify the python version
    easy_install-2.7  pip
    easy_install-2.7  --install-dir=~/lib/python2.7  --script-dir=~/bin  virtualenv
    easy_install-2.7  --install-dir=~/lib/python2.7  --script-dir=~/bin  virtualenvwrapper

**Neil Lyons setups Virtualenv & Virtualenv Wrapper in our .bashrc**

    # edit your bash file
    vi $HOME/.bashrc

    # set the workonhome and virtualenvwrapper_python
    export WORKON_HOME=$HOME/.virtualenvs
    export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python2.7

    # change your user name here
    source /home/<user name>/bin/virtualenvwrapper.sh
    export PIP_VIRTUALENV_BASE=$WORKON_HOME
    export PIP_RESPECT_VIRTUALENV=true

    # :wq out of vim and reload
    bash filesource .bashrc

If you do this correctly after you type the last command virtualenv will
create all of it's directory structure and files.

**Neil Lyons makes a directory for virtualenvs**

    mkdir ~/.virtualenvs
    mkvirtualenv <name-of-virtual-environment>
    workon mysite
    pip install django

**Zoe.vc creates a WebFaction application and website and configures apache and wsgi**

* Create an "mod_wsgi" application and create a website to use this application

* cd into your application folder. There should be 2 folders, "apache2" and
"htdocs"

* [Create django project](https://www.zoe.vc/2010/django-with-virtualenv-on-webfaction/)

		django-admin.py startproject (PROJECT_NAME)

*  backup the httpd.conf from /webapps//apache2/conf.

*  scan the httpd.conf for "Listen XXX". The XXX is your webapp port.

*  remove the … portion of code.

* append the file to tell Apache to use a wsgi config file.

		NameVirtualHost *:<webapp-port>
		<VirtualHost *:<webapp-port>>
		ServerName <SomeServerName>
		WSGIScriptAlias / /home/<your-username>/webapps/<your-webapp-name>/apache2/conf/django.wsgi
		</VirtualHost>

* create a django.wsgi in apache2/conf directory.


		#!/usr/bin/python
		import os
    		import sys
    		import site

	    # Add path to site-packages in our virtualenv
    		site.addsitedir("/home/<your-username>/.virtualenvs/<name-of-virtual-environment>/lib/python2.7/site-packages")

	    from django.core.handlers.wsgi import WSGIHandler

	    sys.path = ['/home/<your-username>/webapps/your-webapp-name>/<your-django-project>'] + sys.path

	    os.environ['DJANGO_SETTINGS_MODULE'] = '<your-django-project>.settings'
	    application = WSGIHandler()


----

#### [VIRTUALENV WRAPPER](http://www.doughellmann.com/docs/virtualenvwrapper/command_ref.html)

**Create an environment**

	mkvirtualenv (ENVNAME)

**List created environments**

	workon

**Open the given environment**

	workon (ENVNAME)

**Deactivates an environment**

	deactivate

**Remove a given environment**

	rmvirtualenv (ENVNAME):

**Copy a given environment**

	cpvirtualenv (ENVNAME) (TARGETENVNAME):

**Setup Steps**

	pip install virtualenv virtualenvwrapper

[Via Videntity](http://blog.videntity.com/?p=584): Adding virtualenv wrapper allows use of “workon” to switch between environments. To do this, add a couple items to the .baschrc file. These are the commands for using “nano,“ terminal-based text editor pre-installed with Ubuntu.

	cd ~
	nano .bashrc

Add the following lines to the bottom of the file.

	export WORKON_HOME=$HOME/.virtualenvs export PIP_VIRTUALENV_BASE=$WORKON_HOME
	export PIP_RESPECT_VIRTUALENV=true source /usr/local/bin/virtualenvwrapper.sh
	export VIRTUALENVWRAPPER_VIRTUALENV_ARGS='--no-site-packages'`

Save with CTL-X and Y to confirm.
Activate virtualenv wrapper by re-running .bashrc

	source .bashrc

----

#### [USING PIP](http://guide.python-distribute.org/pip.html)

**List installed packages**

	pip freeze

**Pipe installed packages to requirements.txt**

	pip freeze > requirements.txt

**Install app requirements/ dependencies from requirements.txt**

	pip install -r requirements.txt

----

#### BEGIN DJANGO PROJECT

**navigate to the django projects directory**

	cd Programming/mystack

**start new django project**

	django-admin.py startproject (PROJECT-NAME)

**start django app**

	python manage.py startapp (APP-NAME)

**sync app models to database**

	python manage.py syncdb

**open Django API**

	python manage.py shell

**run python server**

	python manage.py runserver

**navigate to instance**

	http://127.0.0.1:8000/

----

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
----

#### REG EX TIPS

- To strip leading whitespace: **^[ \t]+**

----

#### INTERACT WITH DATABASE MODELS VIA DJANGO API

**Example:**

    python manage.py shell
    from madfires.models import FireCall, FireStation
    FireCall.objects.count()
    >> 42
    FireStation.objects.count()
    >> 12
    FireCall.objects.filter(fireAlarm__contains='06').count()
    >> 1
    FireCall.objects.filter(fireAlarm__lte='2012-07-14').count()
    >> 19

----

#### DUMP AND LOAD JSON FROM APP OR MODEL DATA

**Base command**

	python manage.py dumpdata

**If no application name is provided, all installed applications will be dumped**

	python manage.py dumpdata madcrime.incident >> incidents.json

**use --indent to pretty-print output with number of indentation spaces**

	python manage.py dumpdata flatpages --indent=2 > flatpages.json

**use --exclude to prevent specific applications or models from being dumped**

	python manage.py dumpdata madcrime --exclude madcrime.incident >> incidents.json

**use loaddata to add information to the database**

	python manage.py loaddata incidents.json

----

#### USING SOUTH

**To set up initial migration:**

	python manage.py schemamigration madcrime --initial

**If already created tables in db run initial migration as fake:**

	python manage.py migrate madcrime --fake

**After initial or fake setup, once you make changes to model:**

	python manage.py schemamigration madcrime --auto

**To set migration to active:**

	python manage.py migrate madcrime

**If need to delete the migrations from db**

	python manage.py migrate madcrime --fake --delete-ghost-migrations

**Convert Existing App**

	python manage.py convert_to_south madfires

----

#### django-extensions

**[django-extensions](http://packages.python.org/django-extensions/command_extensions.html)**

	pip install django-extensions

**To Reset the database**

	python manage.py reset_db --router=default

----

#### MISC

**run python script and puts output in a file in the current directory**

	python first.py --> banks.txt

**[Data_exports to export models to csv](http://django-data-
exports.readthedocs.org/en/latest/index.html)**

  * mime: text/csv
  * file_ext: csv
  * name: Naive CSV format
  * template: data_exports/export_detail_csv.html (included as an example)

**[Fixtures](https://code.djangoproject.com/wiki/Fixtures) provide test data for an application**

	pip install fixturegenerator
	python manage.py generatefixture

**Restart Nginx on AWS linux box**

  * sudoservice nginx restart

**Testing Django with Gunicorn**

  * gunicorn_django -b 0.0.0.0:8000

**Resources & Learning**

  * [Python Code and Recipes](http://code.activestate.com/recipes/langs/python/)
  * [Regular Expressions 101](http://www.tcl.tk/man/tcl/tutorial/Tcl20.html)

**Used plenty from the following to get up and running**

  * [Local and AWS EC2 Setup](http://reporterslab.wikispaces.com/Setting+Up+Your+Mac)

  * [Installing Python on Mac OS X](http://blog.praveengollakota.com/47430655)

  * [Django Production Deployment](http://blog.videntity.com/?p=584)

  * [Notes for setting up the geo stack and dev tools on Lion from @brianboyer](https://gist.github.com/1696819)

----

####PYTHON LIBRARIES THROUGH PIP

  * pip install django

  * pip install django-extensions

  * pip install south (Add to settings.py apps)

  * pip install yolk (Inventories installed libraries)

  * pip install fabric (Used for deplyoment)

  * pip install requests (Interact with sites. [Docs](http://docs.python-requests.org/en/latest/index.html))

  * pip install lxml (Parse HTML. [Docs](http://lxml.de/lxmlhtml.html))

  * pip install mechanize

  * pip install BeautifulSoup==3.2.0

  * pip install csvimporter==0.1

  * pip install django-data-exports==0.2

  * pip install django-mass-edit==1.0

  * pip install django-tastypie==0.9.11

  * pip install fixture-generator

  * pip install django-extensions

  * pip install MySQL-python

  * pip install python-dateutil

  * pip install simplejson (interact with JSON in Python. [Docs](http://svn.red-bean.com/bob/simplejson/tags/simplejson-1.3/docs/index.html))

  * pip install [http://dist.repoze.org/PIL-1.1.6.tar.gz](http://dist.repoze.org/PIL-1.1.6.tar.gz) (Python Imaging Library)

----

#### SETTING UP WINDOWS 7 PYTHON ENVIRONMENT

The following are bullet points gathered from walkthroughs created by [Anthony
DeBarros](http://www.anthonydebarros.com/2011/10/15/setting-up-python-in-
windows-7/) and the Kenneth Reitz's [Python Guide](http://docs.python-
guide.org/en/latest/starting/install/win/) to get a Python development
environment up and running on my work machine.

I needed admin rights for only two steps:

  * Python 2.7.2 installation (Don't install 3.1)
  * Setting the Python path

Once those steps are completed, these steps will get easy_install pip,
virtualenv, django and many other packages up and running.

Download [Distribute for Windows](http://python-
distribute.org/distribute_setup.py) and save the script to your Python27
directory.

Open your command prompt by clicking Start Menu and search for cmd to find
cmd.exe. You will change into the Python27 directory and run the distribute
setup.py script. In turn, you will be able to install pip which is really the
gateway drug to adding packages and learning your way.

    cd C:\
    cd C:\Python27
    python distribute_setup.py
    easy_install pip
    pip install virtualenv

My virtual environments exist inside of C:\Python27\Scripts, so to get there,
change to that directory and create a new virtual environment.

    cd Scripts
    virtualenv --distribute <environment name>

To activate virtual environment:

    cd <environment name>
    cd Scripts
    activate.bat

From here, you can use pip to install python packages to the virtual
environment

    pip install django
    pip install csvkit
    pip install BeautifulSoup
    pip install mechanize

To deactivate a virtual environment

    deactivate