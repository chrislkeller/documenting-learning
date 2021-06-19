# Setting up a Mac OS development machine after clean install

This guide is informed by too many tutorials and Google searches to list. But the guides I have found to be invaluable are NPR apps' [How to Setup Your Mac to Develop News Applications Like We Do](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html), Noah Veltman's [Ubuntu setup script](https://gist.github.com/veltman/7492ad89ed4c0370c41e), [Setting up Sublime Text for Python development](http://dbader.org/blog/setting-up-sublime-text-for-python-development) and Brian Boyer's [Lion dev environment notes](https://gist.github.com/brianboyer/1696819)

## Preparing for clean install

* Move .dotfiles and .dotdirectories to external hard drive
* Check the status of homebrew and export list installed packages
* Export ```requirements.txt``` files from virtual environments
* Backup local [Postgres](http://postgresguide.com/utilities/backup-restore.html) and MySql databases.
* Open font book and export fonts
* List the native applications that are installed.
* Use [Carbon Copy Cloner](http://www.bombich.com/) to create a bootable backup of the machine
    * Attach an external HD and let CCC do its work. This is a backup to the backup

## Performing clean install

* Create OS X Mojave USB Installation Drive
    * Download OS X Mojave from the Mac App Store
    * With a USB drive > 8GB, open Disk Utility and select the drive in the sidebar
    * Format the drive as "Mac OS Extended (Journaled)" and name it Untitled
    * The installer should be called Install macOS Mojave.app and should be in your Applications folder
    * [Run the following from the CLI](http://forums.macrumors.com/showpost.php?p=18081307&postcount=3) and "wait about 20 minutes"

            sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ macOS\ Mojave.app --nointeraction

    * You should see something like this:

            Erasing Disk: 0%... 10%... 20%... 100%...
            Copying installer files to disk...
            Copy complete.
            Making disk bootable...
            Copying boot files...
            Copy complete.
            Done.

    * When it's done, you should get a message stating the process is finished
    * Restart your computer and hold the Option key to access the boot menu
    * Select your new USB drive to install a clean copy of OS X Yosemite

### After the clean install

* Some setup script options if you wish.
    * [SoloWizard](http://www.solowizard.com/)
    * [Laptop](https://github.com/thoughtbot/laptop/blob/master/README.md)

* Otherwise download [AppCleaner](http://www.freemacsoft.net/appcleaner/) and get rid of some cruft if you want.
    * Or delete from the command line

            cd /Applications/
            sudo rm -rf Mail.app/
            sudo rm -rf FaceTime.app/
            sudo rm -rf Stickies.app/
            sudo rm -rf Chess.app/
            sudo rm -rf Photo\ Booth.app
            sudo rm -rf IMovie.app
            sudo rm -rf IPhoto.app
            sudo rm -rf Garage\ Band.app

* Uninstall any existing development tools

        sudo /Developer/Library/uninstall-devtools

* Skip XCode and go for the [Command Line Tools for XCode](https://developer.apple.com/downloads/index.action)
    * More on this path  [here](http://www.bloggure.info/work/installing-homebrew-without-xcode.html). It's much faster than installing the whole XCode suite, which is huge and I don't do anything with it. I will miss the iOS simulators though.
    * Open the Command Line Tools for XCode dmg and install

* Install [Homebrew](http://mxcl.github.com/homebrew/)

        ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
        brew update
        brew doctor
        brew cleanup
        brew prune
        brew doctor

* Add Homebrew to $PATH

        export PATH="/usr/local/bin:$PATH"

* Using [Homebrew and Cask together](http://computers.tutsplus.com/tutorials/perfect-configurations-with-homebrew-and-cask--cms-20768)

        brew tap caskroom/cask
        #cd /usr/local/Library/Taps/phinze/homebrew-cask
        #git remote set-url origin git@github.com:phinze/homebrew-cask.git
        brew install brew-cask
        brew doctor
        brew cask install iterm2

* Iinstall sublime text 3

* Configure Sublime Text 3 subl and symlink settings and packages to external hard drive

        cd ~/Library/Application\ Support/Sublime\ Text\ 3
        rm -rf Packages
        rm -rf Installed\ Packages
        ln -s /Volumes/one_tb_hd/sublime-text-3/Packages
        ln -s /Volumes/one_tb_hd/sublime-text-3/Installed\ Packages
        ln -sv "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl

* Move my ```.bash_profile``` and ```.bash_local files```

        cp -R /Volumes/one_tb_hd/machine_setup/personal_machine_bak/bak_dotfiles/.bash_profile /Users/ckeller
        cp -R /Volumes/one_tb_hd/machine_setup/personal_machine_bak/bak_dotfiles/.bashrc_local /Users/ckeller
        cd ~
        ls -a
        source ~/.bash_profile
        brew doctor
        slime ~ .

* install homebrew python

        cd /System/Library/Frameworks/Python.framework/Versions
        sudo rm Current
        brew install python
        brew doctor
        which python
        which pip
        pip install --upgrade setuptools
        pip install --upgrade distribute
        pip install virtualenv
        pip install virtualenvwrapper
        python --version
        source /usr/local/bin/virtualenvwrapper.sh
        sudo ln -s /usr/local/Cellar/python/2.7.8_2 /System/Library/Frameworks/Python.framework/Versions/Current

* Configure $PATH variables for python, virtualenv, sqlite and sublime text

        # base path and such
        export PATH="/usr/bin:/bin:/usr/sbin:/sbin"

        # sublime text
        export PATH="/usr/local/bin/subl:$PATH"

        # sqlite
        export PATH="/usr/bin/sqlite3:$PATH"

        # all my shell scripts
        export PATH="/Volumes/one_tb_hd/_programming/3scripts-dotfiles/shell-scripts:$PATH"

        # homebrew path
        export PATH="/usr/local/bin:$PATH"

        # virtualenvwrapper settings
        export WORKON_HOME=$HOME/.virtualenvs
        export PIP_VIRTUALENV_BASE=$WORKON_HOME
        export PIP_RESPECT_VIRTUALENV=true
        source /usr/local/bin/virtualenvwrapper.sh

* Install MySQL via homebrew

        brew remove mysql
        brew cleanup
        launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
        rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
        sudo rm -rf /usr/local/var/mysql
        brew install mysql
        ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents

* Getting mysql up and running

        mysql.server start
        mysql_secure_installation
        mysql -u root -p
        SHOW DATABASES;
        SET default_storage_engine=MYISAM;
        ALTER USER 'yourusername'@'localhost' IDENTIFIED WITH mysql_native_password BY 'youpassword';        

* Link MySql data directory to external HD
    * These links helped with the MySQL install
        * http://net.tutsplus.com/tutorials/python-tutorials/intro-to-flask-signing-in-and-out/
        * http://pythonhosted.org/Flask-SQLAlchemy/config.html
        * http://flask-mysql.readthedocs.org/en/latest/

    * if an error is returned, kill the processes

            ps aux | grep mysql
            kill -9 <process number>

    * else

            mysql -u root -p
            SHOW VARIABLES WHERE Variable_Name LIKE "%dir"; - /usr/local/var/mysql/
            mysql.server stop
            sudo rm -rf /usr/local/var/mysql
            ln -s /Volumes/one_tb_hd/mysql /Volumes/Macintosh\ HD/usr/local/var/mysql
            mysql.server start
            mysql -u root -p
            SHOW DATABASES;

* Install Quartz
    * Download is: https://xquartz.macosforge.org
    * Else

            brew cask install xquartz

* Install Postgres and PostGIS
    * These links helped with the Postgres install
        * [To create a spatially-enabled database](http://postgis.net/docs/manual-2.1/postgis_installation.html#create_new_db_extensions)
        * [Users of 1.5 and below will need to go the hard-upgrade path, see here](http://postgis.net/docs/manual-2.1/postgis_installation.html#upgrading)
        * PostGIS SQL scripts installed to ```/usr/local/share/postgis```
        * PostGIS plugin libraries installed to ```/usr/local/opt/postgresql/lib```
        * PostGIS extension modules installed to ```/usr/local/opt/postgresql/share/postgresql/extension```

                pip install numpy
                brew install postgresql
                initdb /usr/local/var/postgres/ -E utf-8
                ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
                alias pgdown='pg_ctl -D /usr/local/var/postgres stop -s -m fast'
                alias pgup='pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start'
                pgup
                brew install gdal --complete --with-postgresql
                brew install postgis
                brew install grass

* install qgis

        brew tap osgeo/osgeo4mac
        brew install qgis-26 --with-grass --with-postgis

* Install Node

        brew install node
        export NODE_PATH=/usr/local/lib/node_modules

* Install rubies

        \curl -sSL https://get.rvm.io | bash -s stable --ruby

        # add rvm to path for scripting
        export PATH="$HOME/.rvm/bin:$PATH"

        # load rvm into a shell session *as a function*
        [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"

        rvm get head
        rvm pkg install readline # need it to work correctly with utf-8 characters in irb/pry
        rvm install 1.9.3 --with-gcc=clang
        gem install capistrano


* Install hombrew packages from ```/Volumes/one_tb_hd/machine_setup/homebrew_packages.txt```

        brew tap beeftornado/rmtree && brew install beeftornado/rmtree/brew-rmtree
        brew tap homebrew/dupes
        brew install ack bash-completion coda-cli curl ec2-api-tools git gist heroku-toolbelt imagemagick mdbtools memcached mongodb phantomjs redis spark

        To have launchd start memcached at login:
            ln -sfv /usr/local/opt/memcached/*.plist ~/Library/LaunchAgents
        Then to load memcached now:
            launchctl load ~/Library/LaunchAgents/homebrew.mxcl.memcached.plist
        Or, if you don't want/need launchctl, you can just run:
            /usr/local/opt/memcached/bin/memcached

        To have launchd start mongodb at login:
            ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
        Then to load mongodb now:
            launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
        Or, if you don't want/need launchctl, you can just run:
            mongod --config /usr/local/etc/mongod.conf

        To have launchd start redis at login:
            ln -sfv /usr/local/opt/redis/*.plist ~/Library/LaunchAgents
        Then to load redis now:
            launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
        Or, if you don't want/need launchctl, you can just run:
            redis-server /usr/local/etc/redis.conf

* Re-install native applications
    * Reinstall the following using cask

            brew cask install color-oracle ccleaner appcleaner fluid google-chrome vlc tabula sqlite-database-browser skype sequel-pro pgadmin3 namechanger hiss adium arduino adobe-reader airparrot audacity chromecast opera firefox google-refine google-drive r tilemill microsoft-office virtualbox vagrant dropbox calibre colorpicker colorpicker-hex ngrok openoffice mou media-converter sigil rstudio sparrow spotify evernote cyberduck adapter audio-hijack-pro

        * Will need to download the others

    * User script to install native applicatons


* Install IE vms

        ```curl -s https://raw.githubusercontent.com/xdissent/ievms/master/ievms.sh | env IEVMS_VERSIONS="8 9 10 11" INSTALL_PATH="/Volumes/one_tb_hd/virtualbox_vms/ie_vms" bash```

    * You may remove all files except *.vmdk after installation and they will be re-downloaded if ievms is run again in the future:

        ```$ find ~/.ievms -type f ! -name "*.vmdk" -exec rm {} \;```

    * Copy And Paste Between [VirtualBox Host And Guest Machines](https://www.liberiangeek.net/2013/09/copy-paste-virtualbox-host-guest-machines/)

    * Access host localhost by going to [http://10.0.2.2:8880](http://10.0.2.2:8880) on the guest

* Misc
    * Add bash.mode, django.mode, markdown.mode and WordPress.mode to Coda2.
    * Add [tomorrow-theme](https://github.com/chriskempson/tomorrow-theme) for Coda2.
    * [Generate ssh keys for GitHub](https://help.github.com/articles/generating-ssh-keys)

    * Misc OS X Preferences Commands

        * Fix font smoothing
        ```defaults -currentHost write -globalDomain AppleFontSmoothing -int 0```

        * Disable window animations
        ```defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false```

        * Enable repeat on keydown
        ```defaults write -g ApplePressAndHoldEnabled -bool false```

        * Disable webkit homepage
        ```defaults write org.webkit.nightly.WebKit StartPageDisabled -bool true```

        * Use current directory as default search scope in Finder
        ```defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"```

        * Show Path bar in Finder
        ```defaults write com.apple.finder ShowPathbar -bool true```

        * Show Status bar in Finder
        ```defaults write com.apple.finder ShowStatusBar -bool true```

        * Show indicator lights for open applications in the Dock
        ```defaults write com.apple.dock show-process-indicators -bool true```

        * Enable AirDrop over Ethernet and on unsupported Macs running Lion
        ```defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true```

        * Set a blazingly fast keyboard repeat rate
        ```defaults write NSGlobalDomain KeyRepeat -int 0.02```

        * Set a shorter Delay until key repeat
        ```defaults write NSGlobalDomain InitialKeyRepeat -int 12```

        * Disable disk image verification
        ```defaults write com.apple.frameworks.diskimages skip-verify -bool true &&```
        ```defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true &&```
        ```defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true```

        * Disable Safari’s thumbnail cache for History and Top Sites
        ```defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2```

        * Enable Safari’s debug menu
        ```defaults write com.apple.Safari IncludeInternalDebugMenu -bool true```

        * Disable the Ping sidebar in iTunes
        ```defaults write com.apple.iTunes disablePingSidebar -bool true```

        * Add a context menu item for showing the Web Inspector in web views
        ```defaults write NSGlobalDomain WebKitDeveloperExtras -bool true```

        * Show the ~/Library folder
        ```chflags nohidden ~/Library```

        * Disable ping dropdowns
        ```defaults write com.apple.iTunes hide-ping-dropdown true```
