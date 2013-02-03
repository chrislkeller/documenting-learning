# Learning To Use:  Postgres

In setting up a couple machines now, I have found two methods of installing Postgres.

Some kind folks at Heroku have created a [one-click installer](http://postgresapp.com/) for [PostgreSQL](http://www.postgresql.org/) on a Mac. Just add to your $PATH and the database is up and running when you bootup.

There is also the [Homebrew route](https://gist.github.com/2280659), which took me a bit longer to make it work.

To help see the data and to make sure I was on the right track I installed [pgAdmin III](http://www.pgadmin.org/download/) which is a GUI to explore the databases, which is good for a noob like me.

# Installing

**Quickstart**

* Download [Postgres.App](http://postgresapp.com/) and install.
* Download [pgAdmin III](http://www.pgadmin.org/download/) and install.

**Homebrew Route with additional GIS tools**

* Install Postgres and initialize the database.

		brew install postgres
		initdb /usr/local/var/postgres

* Should a memory allocation error arise (Failed system call was shmget(key=1, size=1646592, 03600) run.

		sudo sysctl -w kern.sysv.shmmax=1073741824
		sudo sysctl -w kern.sysv.shmall=1073741824

* Add aliases to your .bashrc to start and stop postgres.

		alias postgresup='pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start'
		alias postgresdown='pg_ctl -D /usr/local/var/postgres stop -s -m fast'

* Add PostGIS and GDAL.

		brew install gdal --with-postgres
		brew install postgis

* SpatiaLite extends SQLite core to support fully Spatial SQL.

		brew install libspatialite

* Software tailored to scientific endeavors.

		brew tap homebrew/science

* Install qgis.

		brew install qgis --with-grass --with-postgis

# Basic/Beginner Commands

* **Quickstart**

		createuser

        // creates database for user owned by the user with a name using template0
		createdb -U DjangoKeller -E utf8 -O DjangoKeller madsafety_db -T template0

* **Create new user**

        createuser

* **Activate PostgreSQL**

        psql

* **List databases**

        psql \l or psql \list

* **Create a database**

        createdb **name_of_database**

* **Creates database for the user**

        // creates database for user owned by the user with a name using template0
        createdb -U **user_name** -E utf8 -O **owner_name** **name_of_database** -T template0

* **Log into database**

        psql **name_of_database**

* **Delete a database**

        dropdb mydb

* **Add PostGIS extension to a database**

        psql -U **user_name** -h localhost **name of database** -c 'CREATE EXTENSION postgis;'

* **See if table has been created**

        \dt

* **Drop table**

		DROP TABLE **name_of_table**

* **Quit psql**

		\q

# Documentation & Resources

* There is great PostgreSQL [documentation](- [Postgres Documentation](http://www.postgresql.org/docs/9.2/static/index.html) that walks through the basic use.
* I also found a good [beginner's cheat sheet](http://od-eon.com/blogs/calvin/postgresql-cheat-sheet-beginners/).
* Here's how to create a Postgres spatial database [using EXTENSIONS](http://postgis.refractions.net/documentation/manual-2.0/postgis_installation.html#create_new_db_extensions).


----

Ask my wife or close friends and surely they'll let you know how impatient I can be. And I'll own up to it everytime. I was ready for a full-time job at the age of 10 and anxious to drop out of college and start working as soon as I finished my journalism classes.
So it's not surprising that after a handful of Django successes, I thought I was ready to get PostgreSQL and PostGIS up and running on my machine before I even knew what they might be good for.

Note to self: Learn some lingo, and what it is you are really trying to accomplish. It helps.

But it also helps to just jump in, fail, try again, make it further, fail. As I heard at #NICAR12 over and over, progress can be as simple as getting to the next "right" error message.

So what follows is how I got a GIS development stack up and running on MacOS…

Now I just have to learn how to use it.

##The Process##

I started off using [this 2010 post](http://blog.apps.chicagotribune.com/2010/02/17/quick-install-pythonpostgis-geo-stack-on-snow-leopard/) from Brian Boyer and [his updated notes](https://gist.github.com/1696819). I also followed along to a [Reporter's Lab post](http://reporterslab.wikispaces.com/Setting+Up+Your+Mac) on Setting Up A Macintosh (Snow Leopard) For Development.

I already had pip, virtualenv and virtualenvwrapper installed and running properly.

**Install Homebrew**

According to [its homepage](http://mxcl.github.com/homebrew/), Homebrew is the easiest and most flexible way to install the UNIX tools Apple didn't include with OS X.

Open up the terminal and enter the following:

     sudo mkdir /usr/local
     sudo chown -R `whoami` /usr/local
     curl -L http://github.com/mxcl/homebrew/tarball/master | tar xz --strip 1 -C /usr/local

These commands will make a new directory on your machine, change the owner of the directory and install homebrew.

**Install GIS stack**

Now you're ready to install the guts.

     brew install postgres
     brew install gdal --with-postgres
     brew install postgis





Brian  (EDIT THE FORMULA FIRST, see https://github.com/mxcl/homebrew/issues/8301)

edit /etc/paths to put /usr/local/bin on top, so that lion's psql doesnt win







**Some things I ran into, and how I solved them**

**[Post](http://journal.tianhao.info/2010/12/postgresql-change-default-encoding-of-new-databases-to-utf-8-optional/): How to Change Default Encoding of New Databases To UTF-8**

**Autostart PostgreSQL**

In the PostgreSQL documentation, and on nearly all of the walkthroughs, I found reference to the following which would start the server when your mac boots up.

     mkdir -p ~/Library/LaunchAgents

     cp /usr/local/Cellar/postgresql/9.1.3/org.postgresql.postgres.plist ~/Library/LaunchAgents/

     launchctl load -w ~/Library/LaunchAgents/org.postgresql.postgres.plist

What I found however is Homebrew has a plist file that is automatically added to your User library, allowing postgresql to start when the machine boots up. I don't know if this is normal or not.

If I had read a bit further -- and admittedly I see what this means after researching the setup -- the install script from Homebrew offers you this bit of advice:

     # Start/Stop PostgreSQL

     If this is your first install, automatically load on login with:

     mkdir -p ~/Library/LaunchAgents
     cp /usr/local/Cellar/postgresql/9.1.3/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
     launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

And homebrew.mxcl.postgresql.plist is the file I found.

**[Post](http://stackoverflow.com/questions/6770649/repairing-postgresql-after-upgrading-to-osx-10-7-lion): Determine which PostgreSQL install is running**

MacOS Lion has an instance of PostgreSQL already running.

The system's install will live in usr/bin/psql.

The Homebrew install will live in usr/local/bin/psql.

To determine the path to the active postgres install, use the following command:

     which psql

If it comes back as the Homebrew install, you should be good. If it comes back as the system install, you'll need to adjust the PATH.

From the above blog post:

>It's a PATH issue. Mac OSX Lion includes Postgresql in the system now. If you run brew doctor you should get a message stating that you need to add usr/local/bin to the head of your PATH env variable. Editing your .bash_profile or .profile, or whichever shell you're using and adding: export PATH=/usr/local/bin:$PATH as the first export for the PATH then either quit you shell session or source your file with source ~/.bash_profile and it should now be OK again.

**Manually Start Postgres:**

     postgres -D /usr/local/var/postgres

or

     pg_ctl -D /usr/local/var/postgres -l logfile start

**Manually Stop Postgres:**

     pg_ctl -D /usr/local/var/postgres stop -s -m fast

**Create/Upgrade a Database**

     initdb /usr/local/var/postgres
----

**Create a PostgreSQL database**

     createdb <NAME OF DATABASE>

**Install PostGIS in the database**

     psql -d <NAME OF DATABASE> -f /usr/local/share/postgis/postgis.sql
     psql -d <NAME OF DATABASE> -f /usr/local/share/postgis/spatial_ref_sys.sql

----

**[Post](http://willbryant.net/software/mac_os_x/postgres_initdb_fatal_shared_memory_error_on_leopard): Fixing the postgresql initdb fatal shared memory error on Leopard**

When I first attempted to run

     initdb /usr/local/var/postgres

I would get the following error message:

     FATAL:  could not create shared memory segment: Cannot allocate memory
     DETAIL:  Failed system call was shmget(key=1, size=1646592, 03600).

To remedy, I ran the following:

     sudo sysctl -w kern.sysv.shmmax=1073741824
     sudo sysctl -w kern.sysv.shmall=1073741824
     pg_ctl start -D /installation_directory
     curl http://nextmarvel.net/blog/downloads/fixBrewLionPostgres.sh | sh
     createdb mydb

----

A quick workaround on Lion is to move /usr/local/bin before /usr/bin in /etc/paths, then logout and log back in.

https://github.com/mxcl/homebrew/issues/6343

----

http://www.iainlbc.com/2011/10/osx-lion-postgres-could-not-connect-to-database-postgres-after-homebrew-installation/

----

- [Setting up PostgreSQL for ruby on rails development on os x](http://blog.willj.net/2011/05/31/setting-up-postgresql-for-ruby-on-rails-development-on-os-x/)
- [OSX Lion: Postgres could not connect to database postgres (after homebrew installation)]((http://www.iainlbc.com/2011/10/osx-lion-postgres-could-not-connect-to-database-postgres-after-homebrew-installation/))
- [Install PostgreSQL 9 on OS X](http://russbrooks.com/2010/11/25/install-postgresql-9-on-os-x)
- [HowTo: Run the .sh File Shell Script In Linux / UNIX](http://www.cyberciti.biz/faq/run-execute-sh-shell-script/)
- [How to install PostgreSQL and PostGIS on Mac OS X Lion](http://lassebunk.dk/2011/09/08/installing-postgresql-and-postgis-on-mac-os-x/)
- [Setting Up A Macintosh (Snow Leopard) For Development](http://reporterslab.wikispaces.com/Setting+Up+Your+Mac)
- [Quick-install Python/PostGIS geo stack on Snow Leopard](http://blog.apps.chicagotribune.com/2010/02/17/quick-install-pythonpostgis-geo-stack-on-snow-leopard/)
- [Brian Boyer's Lion dev environment notes](https://gist.github.com/1696819)
- [Make a postgis template](https://gist.github.com/666218#file_mk_postgis_template.sh)