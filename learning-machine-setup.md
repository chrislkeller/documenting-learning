# Setting up a Mac OS development machine after clean install

This guide is informed by too many tutorials and Google searches to list. But the guides I have found to be invaluable are NPR apps' [How to Setup Your Mac to Develop News Applications Like We Do](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html), Noah Veltman's [Ubuntu setup script](https://gist.github.com/veltman/7492ad89ed4c0370c41e) and Brian Boyer's [Lion dev environment notes](https://gist.github.com/brianboyer/1696819)

## Preparing for clean install

* Move all of the following directories to external hard drive
    * heroku settings
    * qgis settings and plugins
    * rvm settings and gems
    * tarbell settings
    * ssh keys
        * ```cp -r ~/.heroku ~/.qgis2 ~/.rvm ~/.ssh ~/.tarbell ~/.tilemill ~/.virtualenvs /Volumes/one_tb_hd/machine_setup/```

* Move all of the following files to external hard drive
    * .bash_profile
    * .boto
    * .gitconfig
    * .gitignore
    * .ngrok
    * .sunlight.key
    * .netrc
        * ```cp -r ~/.bash_profile ~/.boto ~/.gitconfig ~/.gitignore ~/.ngrok ~/.sunlight.key ~/.netrc /Volumes/one_tb_hd/machine_setup/```

* Check the status of homebrew and export list installed packages
    * ```brew update```
    * ```brew cleanup```
    * ```brew prune```
    * ```brew doctor```
    * ```brew list -1 > /Volumes/one_tb_hd/machine_setup/homebrew_packages.txt```

* Export ```requirements.txt``` files from virtual environments using shell script
    * ```virtual-backup```

* Export ```requirements.txt``` files from virtual environments using shell script
    * ```virtual-backup```

* **If necessary** backup local [Postgres](http://postgresguide.com/utilities/backup-restore.html) and MySql databases. Mine are based off an external hard drive backed up to local machine. I also wrote a script to export MySQL databases.

        # postgres
        # list databases
        psql -l

        # dump a database
        pg_dump -Ft database_name_here > database.tar # compressed tarball

        # create and restore a database
        pg_restore -Ft -C database.tar # restore tarball

        # mysql
        bak-mysql

* List the native applications that are installed.
    * ```cd /Applications``` then ```ls -a -1```
        * Campfire: *Fluid App*
        * Chartbeat: *Fluid App*
        * GitHubWeb: *Fluid App*
        * Gmail: *Fluid App*
        * Google Analytics: *Fluid App*
        * Google Calendar: *Fluid App*
        * KPCC Reader: *Fluid App*
        * Adobe Acrobat X Pro: *KPCC IT App*
        * Adobe Illustrator CS5.1: *KPCC IT App*
        * Adobe Photoshop CS5.1: *KPCC IT App*
        * Microsoft Excel: *KPCC IT App*
        * Microsoft Outlook: *KPCC IT App*
        * Microsoft PowerPoint: *KPCC IT App*
        * Microsoft Word: *KPCC IT App*
        * VMware Fusion: *KPCC IT App*
        * [Adium](http://adium.im/): *Must Have*
        * [Opera](http://www.opera.com/browser/next/): *Must Have*
        * AppCleaner: *Must Have*
        * Byword: *Must Have*
        * Dropbox: *Must Have*
        * Evernote: *Must Have*
        * Firefox: *Must Have*
        * Fluid: *Must Have*
        * Google Chrome: *Must Have*
        * Google Refine: *Must Have*
        * Growl: *Must Have*
        * Hiss: *Must Have*
        * iTerm2: *Must Have*
        * Memory Clean: *Must Have*
        * OpenOffice: *Must Have*
        * Patterns: *Must Have*
        * pgAdmin3: *Must Have*
        * QGIS: *Must Have*
        * R: *Must Have*
        * R Studio: *Must Have*
        * R64: *Must Have*
        * RegExr: *Must Have*
        * Sequel Pro: *Must Have*
        * Skitch: *Must Have*
        * Skype: *Must Have*
        * SQLite Database Browser 2.0 b1: *Must Have*
        * Sublime Text: *Must Have*
        * Tableau: *Must Have*
        * Tableau Public: *Must Have*
        * Tabula: *Must Have*
        * TileMill: *Must Have*
        * Trello: *Must Have*
        * TweetDeck: *Must Have*
        * Vagrant: *Must Have*
        * VirtualBox: *Must Have*
        * Adapter: *Second Tier*
        * Adobe Reader: *Second Tier*
        * AirParrot: *Second Tier*
        * Alfred 2: *Second Tier*
        * All2MP3: *Second Tier*
        * Arduino: *Second Tier*
        * Audacity: *Second Tier*
        * Audio Hijack Pro: *Second Tier*
        * AudioCapture: *Second Tier*
        * Belkin: *Second Tier*
        * BitTorrent: *Second Tier*
        * Book Proofer: *Second Tier*
        * Booknote Importer: *Second Tier*
        * Briquette: *Second Tier*
        * calibre: *Second Tier*
        * Captur: *Second Tier*
        * Carbon Copy Cloner: *Second Tier*
        * CCleaner: *Second Tier*
        * CheatSheet: *Second Tier*
        * Checkbook HD: *Second Tier*
        * Chromecast: *Second Tier*
        * Coda 2: *Second Tier*
        * Color Oracle: *Second Tier*
        * Colorblender: *Second Tier*
        * CSVEdit: *Second Tier*
        * DashExpander: *Second Tier*
        * Disk Inventory X: *Second Tier*
        * Draft: *Second Tier*
        * GitHub: *Second Tier*
        * Google Drive: *Second Tier*
        * Google Earth Pro: *Second Tier*
        * GoToMeeting (1082): *Second Tier*
        * iAd Producer: *Second Tier*
        * iAntivirus: *Second Tier*
        * iBooks Author: *Second Tier*
        * iBoostUp: *Second Tier*
        * Image Capture: *Second Tier*
        * iMeme: *Second Tier*
        * Induction: *Second Tier*
        * iTunes Producer: *Second Tier*
        * iVI: *Second Tier*
        * join.me: *Second Tier*
        * Keynote: *Second Tier*
        * Kindle: *Second Tier*
        * Kindle Previewer: *Second Tier*
        * MacX DVD Ripper Mac Free Edition: *Second Tier*
        * MagicPrefs: *Second Tier*
        * Mailbox (Beta): *Second Tier*
        * Marked: *Second Tier*
        * Microsoft Silverlight: *Second Tier*
        * MindNode Lite: *Second Tier*
        * Mint QuickView: *Second Tier*
        * Mixxx: *Second Tier*
        * Mou: *Second Tier*
        * MPEG Streamclip: *Second Tier*
        * MySQLWorkbench: *Second Tier*
        * Pocket: *Second Tier*
        * Rdio: *Second Tier*
        * Read Later: *Second Tier*
        * RecordIt: *Second Tier*
        * Sauce: *Second Tier*
        * Shuttle: *Second Tier*
        * Sigil: *Second Tier*
        * SketchBookExpress: *Second Tier*
        * Slack: *Second Tier*
        * Soulver: *Second Tier*
        * Soundflower: *Second Tier*
        * SourceTree: *Second Tier*
        * Spotify: *Second Tier*
        * StuffIt Expander: *Second Tier*
        * Twitter: *Second Tier*
        * VirtualDJ Home: *Second Tier*
        * VLC: *Second Tier*
        * Wondershare PDF to Excel: *Second Tier*
        * Wunderlist: *Second Tier*

* Open font book and export fonts

* Use [Carbon Copy Cloner](http://www.bombich.com/) to create a bootable backup of the machine
    * Attach an external HD and let CCC do its work. This is a backup to the backup

## Performing clean install

* [Create OS X Mavericks USB Installation Drive](http://lifehacker.com/how-to-create-an-os-x-mavericks-usb-installation-drive-1450280026)
    * Download OS X Mavericks from the Mac App Store
    * With a USB drive > 8GB, open Disk Utility and select the drive in the sidebar
    * Format the drive as "Mac OS Extended (Journaled)" and name it Untitled
    * The installer should be called Install OS X Mavericks.app and should be in your Applications folder
    * [Run the following from the CLI](http://forums.macrumors.com/showpost.php?p=18081307&postcount=3) and "wait about 20 minutes"

            sudo /Applications/Install\ OS\ X\ Mavericks.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ OS\ X\ Mavericks.app --nointeraction

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
    * Select your new USB drive to install a clean copy of OS X Mavericks

### After the clean install

* Setup script options
 * [SoloWizard](http://www.solowizard.com/)
 * [Laptop](https://github.com/thoughtbot/laptop/blob/master/README.md)

* Skip XCode and go for the developer tools
    * [Download Command Line Tools for XCode](https://developer.apple.com/downloads/index.action)
    * I'm going to give [this a try](http://www.bloggure.info/work/installing-homebrew-without-xcode.html) as opposed to installing the whole XCode sweet which is huge and I don't do anything with. I will miss the iOS simulators though.
        * Uninstall any existing development tools

                sudo /Developer/Library/uninstall-devtools

        * Open the Command Line Tools for XCode dmg and install

* Install [Homebrew](http://mxcl.github.com/homebrew/)

        ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"

    * ```brew update```
    * ```brew doctor```
    * Install packages from ```/Volumes/one_tb_hd/machine_setup/homebrew_packages.txt```
    * ```brew cleanup```
    * ```brew prune```
    * ```brew doctor```
    * Add Homebrew to $PATH
        * ```export PATH=/usr/local/bin:$PATH```
    * ```brew tap phinze/cask```
    * ```brew install brew-cask```
    * Using [Homebrew and Cask together](http://computers.tutsplus.com/tutorials/perfect-configurations-with-homebrew-and-cask--cms-20768)

* Install MySQL via homebrew

        brew remove mysql
        brew cleanup
        launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
        rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
        sudo rm -rf /usr/local/var/mysql
        brew install mysql

    * Link MySql data directory to external HD

        mysql -u root -p
        SHOW VARIABLES WHERE Variable_Name LIKE "%dir"; - /usr/local/var/mysql/
        mysql.server stop
        ln -s /Volumes/one_tb_hd/mysql /Volumes/Macintosh\ HD/usr/local/var/mysql
        mysql.server start

    * Getting mysql up and running

            mysql.server start
            mysql_secure_installation
            mysql -u root -p
            SHOW DATABASES;

    * These links helped with the MySQL install
        * http://net.tutsplus.com/tutorials/python-tutorials/intro-to-flask-signing-in-and-out/
        * http://pythonhosted.org/Flask-SQLAlchemy/config.html
        * http://flask-mysql.readthedocs.org/en/latest/

* Configure $PATH for Python

        cd /System/Library/Frameworks/Python.framework/Versions
        sudo rm Current
        ln -s /usr/local/Cellar/python/2.7.2/Frameworks/Python.framework/Versions/Current

        easy_install pip
        pip install --upgrade distribute
        pip install virtualenv
        pip install virtualenvwrapper

        python --version

        source /usr/local/bin/virtualenvwrapper.sh

        ######### set paths for ruby & python #########
        export PATH="/usr/local/share/python:/usr/local/bin/python:/usr/local/bin:/Users/ckeller/.rvm/bin:/usr/bin:/bin:/usr/sbin:/sbin"

        ######### virtualenvwrapper settings #########
        export WORKON_HOME=$HOME/.virtualenvs
        export PIP_VIRTUALENV_BASE=$WORKON_HOME
        export PIP_RESPECT_VIRTUALENV=true
        source /usr/local/bin/virtualenvwrapper.sh

* Install rubies

        curl https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
        rvm get head
        rvm pkg install readline # need it to work correctly with utf-8 characters in irb/pry
        rvm install 1.9.3 --with-gcc=clang
        gem install capistrano

* Install Node

        brew install node
        curl https://npmjs.org/install.sh | sh
        export NODE_PATH=/usr/local/lib/node_modules

* [Generate ssh keys for GitHub](https://help.github.com/articles/generating-ssh-keys)

* Re-install native applications

* [DavMail](http://davmail.sourceforge.net/macosxsetup.html) for email client to access web mail.

* [Ubuntu Mono font library](http://font.ubuntu.com/#charset-mono-regular).

* Add bash.mode, django.mode, markdown.mode and WordPress.mode to Coda2.

* Add [tomorrow-theme](https://github.com/chriskempson/tomorrow-theme) for Coda2.

* Install IE vms

    ```curl -s https://raw.githubusercontent.com/xdissent/ievms/master/ievms.sh | env IEVMS_VERSIONS="8 9 10 11" INSTALL_PATH="/Volumes/one_tb_hd/virtualbox_vms/ie_vms" bash```

    * You may remove all files except *.vmdk after installation and they will be re-downloaded if ievms is run again in the future:

        ```$ find ~/.ievms -type f ! -name "*.vmdk" -exec rm {} \;```

    * Copy And Paste Between [VirtualBox Host And Guest Machines](https://www.liberiangeek.net/2013/09/copy-paste-virtualbox-host-guest-machines/)

    * Access host localhost by going to [http://10.0.2.2:8880](http://10.0.2.2:8880) on the guest

* Symlink Sublime Text 3 settings and packages to external hard drive

        cd ~/Library/Application\ Support/Sublime\ Text\ 3
        rm -rf Packages
        rm -rf Installed\ Packages
        ln -s /Volumes/one_tb_hd/sublime-text-3/Packages
        ln -s /Volumes/one_tb_hd/sublime-text-3/Installed\ Packages

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