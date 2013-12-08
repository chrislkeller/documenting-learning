# Setting up a Mac OS development machine

This guide is informed by too many tutorials and Google searches to list. But the guides I have found to be invaluable are NPR apps' [How to Setup Your Mac to Develop News Applications Like We Do](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html) and Brian Boyer's [Lion dev environment notes](https://gist.github.com/brianboyer/1696819)

### Preparing for clean install

**Backup local [Postgres](http://postgresguide.com/utilities/backup-restore.html) and MySql databases**

        # list databases
        psql -l

        # dump a database
        pg_dump -Ft database_name_here > database.tar # compressed tarball

        # create and restore a database
        pg_restore -Ft -C database.tar # restore tarball

**Backup ssh keys**

**Create a backup of the current development environment**

* Download [Carbon Copy Cloner](http://www.bombich.com/) which will create a bootable backup of the machine
* Attach an external HD and let CCC do its work

**[Create OS X Mavericks USB Installation Drive](http://lifehacker.com/how-to-create-an-os-x-mavericks-usb-installation-drive-1450280026)**

* Download OS X Mavericks from the Mac App Store
* With a USB drive > 8GB, open Disk Utility and select the drive in the sidebar
* Format the drive as "Mac OS Extended (Journaled)" and name it Untitled
* The installer should be called Install OS X Mavericks.app and should be in your Applications folder
* [Run the following from the CLI](http://forums.macrumors.com/showpost.php?p=18081307&postcount=3) and "wait about 20 minutes"

        sudo /Applications/Install\ OS\ X\ Mavericks.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ OS\ X\ Mavericks.app --nointeraction

>You should see something like this:
>
>       Erasing Disk: 0%... 10%... 20%... 100%...
>       Copying installer files to disk...
>       Copy complete.
>       Making disk bootable...
>       Copying boot files...
>       Copy complete.
>       Done.

* When it's done, you should get a message stating the process is finished
* Restart your computer and hold the Option key to access the boot menu
* Select your new USB drive to install a clean copy of OS X Mavericks

### After the clean install

**See how far [SoloWizard](http://www.solowizard.com/) will get you**

**[Install Command Line Tools for XCode](https://developer.apple.com/downloads/index.action)**

* I'm going to give [this a try](http://www.bloggure.info/work/installing-homebrew-without-xcode.html) as opposed to installing the whole XCode sweet which is huge and I don't do anything with. I will miss the iOS simulators though.

        sudo /Developer/Library/uninstall-devtools

**Install [Homebrew](http://mxcl.github.com/homebrew/)**

		ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"

* Use Homebrew to install the following

        brew install ack apple-gcc42 autoconf automake bison cmake coda-cli curl doxygen ec2-api-tools expat fftw freetype freexl gdal gdbm geos gettext giflib git glib gpp grass gsl howdoi imagemagick jbig2dec jpeg json-c libevent libffi libgeotiff libpng libspatialite libtiff libtool libxml2 little-cms2 lzlib mdbtools memcached mongodb mupdf node opencv openjpeg ossp-uuid pkg-config postgis postgresql proj pyqt python qt qwt readline redis sip spatialindex sqlite unixodbc wget wxmac xz

        brew doctor

* Add Homebrew to $PATH

        export PATH=/usr/local/bin:$PATH

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

**Install rubies**

        curl https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
        rvm get head
        rvm pkg install readline # need it to work correctly with utf-8 characters in irb/pry
        rvm install 1.9.3
        gem install capistrano

**Install Node**

        brew install node
        curl https://npmjs.org/install.sh | sh
        export NODE_PATH=/usr/local/lib/node_modules

**[Generate ssh keys for GitHub](https://help.github.com/articles/generating-ssh-keys)**

**Re-install the following native applications**

* Ableton Live 8.app
* Adapter.app
* [Adium](http://adium.im/)
* Adobe CS Applications
* Adobe Help Viewer 1.0.app
* Adobe Illustrator CS5.1
* Adobe Photoshop CS5.1
* Adobe Reader.app
* AirParrot.app
* Alfred 2.app
* All2MP3.app
* App Store.app
* AppCleaner.app
* Arduino.app
* Audacity
* Audio Hijack Pro.app
* AudioCapture.app
* Automator.app
* Belkin
* BitTorrent.app
* Book Proofer.app
* Booknote Importer.app
* Briquette.app
* Byword.app
* Calculator.app
* Calendar Plus.app
* Calendar.app
* calibre.app
* Call of Duty.app
* Campfire.app
* Captur
* Captur.app
* Carbon Copy Cloner.app
* CCleaner.app
* CheatSheet.app
* Checkbook HD.app
* Chess.app
* Chromecast.app
* Coda 2
* Coda 2.app
* Color Oracle.app
* Color Oracle.app
* Colorblender.app
* Contacts.app
* CSVEdit.app
* Dashboard.app
* DashExpander.app
* DavMail.app
* Dictionary.app
* Draft.app
* Dropbox.app
* DVD Player.app
* Evernote.app
* FaceTime.app
* Feedly.app
* Firefox Beta.app
* Firefox.app
* Fluid.app
* Font Book.app
* Game Center.app
* GamePad Companion.app
* GarageBand.app
* GCal.app
* GIMP.app
* GitHub.app
* GitHubWeb.app
* GitX
* Gmail.app
* GoFlex Home Desktop Applications
* Google Calendar.app
* Google Chrome.app
* Google Drive.app
* Google Refine.app
* GoToMeeting (1082).app
* GRASS-6.4.app
* Growl
* Growl.app
* HipChat.app
* Hiss
* Hiss.app
* iAd Producer.app
* iAntivirus.app
* iBooks Author.app
* iBoostUp.app
* iDVD.app
* Image Capture.app
* iMeme.app
* iMovie.app
* import.io.app
* Induction.app
* Instapaper.app
* Instashare.app
* iPhoto.app
* iSnap.app
* iTemplates.app
* iTerm.app
* iTunes Producer.app
* iTunes.app
* iTunification.app
* iVI.app
* JewelryBox.app
* join.me.app
* Keynote
* Keynote.app
* Keynote.app
* Kindle
* Kindle Previewer.app
* Kindle.app
* Launchpad.app
* MacDropAny.app
* Mactracker.app
* MacX DVD Ripper Mac Free Edition.app
* MagicPrefs.app
* Mail.app
* MAMP
* MAMP PRO
* Marked.app
* Media Converter.app
* MenuBarFilter.app
* Messages.app
* Microsoft Messenger.app
* Microsoft Office 2008
* Microsoft Office 2011
* Microsoft Silverlight
* MindNode Lite.app
* Mint QuickView.app
* Mission Control.app
* Mixxx.app
* Mou.app
* MPEG Streamclip.app
* Notes.app
* [Opera](http://www.opera.com/browser/next/)
* OpenOffice.app
* Parallels Desktop.app
* Patterns.app
* PdaNetMac.app
* pgAdmin3.app
* Photo Booth.app
* PivotalBooster.app
* Pocket.app
* Postbox.app
* Postgres.app
* Preview.app
* PyRegEx.app
* Python 2.7
* QGIS.app
* QuickHub.app
* QuickTime Player.app
* R.app
* R64.app
* Rdio.app
* Read Later.app
* Reeder.app
* RegExr.app
* Reminders.app
* Remote Desktop Connection.app
* Safari.app
* Sauce.app
* Sequel Pro.app
* Sequel Pro.app
* Shortcat.app
* Sigil.app
* SketchBookExpress.app
* Skitch.app
* Skype.app
* Sophos Remove.app
* Soundflower
* SourceTree.app
* Sparrow.app
* Spotify.app
* SQLite Database Browser 2.0 b1.app
* SqliteQuery.app
* Stickies.app
* StuffIt Expander
* StuffIt Expander.app
* Sublime Text 2.app
* System Preferences.app
* Tabula.app
* TextEdit.app
* TextMate.app
* TileMill.app
* Time Machine.app
* TinyUmbrella.app
* TweetDeck.app
* Twitter.app
* Utilities
* Vagrant
* VirtualBox.app
* VirtualDJ Home.app
* VLC.app
* VMware Fusion.app
* Wondershare PDF to Excel.app
* Wunderlist.app
* Xcode.app
* XtraFinder.app
* [DavMail](http://davmail.sourceforge.net/macosxsetup.html) for email client to access web mail.
* [Ubuntu Mono font library](http://font.ubuntu.com/#charset-mono-regular).
* Add bash.mode, django.mode, markdown.mode and WordPress.mode to Coda2.
* Add [tomorrow-theme](https://github.com/chriskempson/tomorrow-theme) for Coda2.

### Misc OS X Preferences Commands

        *Fix font smoothing
        defaults -currentHost write -globalDomain AppleFontSmoothing -int 0

        *Disable window animations
        defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false

        *Enable repeat on keydown
        defaults write -g ApplePressAndHoldEnabled -bool false

        *Disable webkit homepage
        defaults write org.webkit.nightly.WebKit StartPageDisabled -bool true

        *Use current directory as default search scope in Finder
        defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

        *Show Path bar in Finder
        defaults write com.apple.finder ShowPathbar -bool true

        *Show Status bar in Finder
        defaults write com.apple.finder ShowStatusBar -bool true

        *Show indicator lights for open applications in the Dock
        defaults write com.apple.dock show-process-indicators -bool true

        *Enable AirDrop over Ethernet and on unsupported Macs running Lion
        defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

        *Set a blazingly fast keyboard repeat rate
        defaults write NSGlobalDomain KeyRepeat -int 0.02

        *Set a shorter Delay until key repeat
        defaults write NSGlobalDomain InitialKeyRepeat -int 12

        *Disable disk image verification
        defaults write com.apple.frameworks.diskimages skip-verify -bool true &&
        defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true &&
        defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true

        *Disable Safari’s thumbnail cache for History and Top Sites
        defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2

        *Enable Safari’s debug menu
        defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

        *Disable the Ping sidebar in iTunes
        defaults write com.apple.iTunes disablePingSidebar -bool true

        *Add a context menu item for showing the Web Inspector in web views
        defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

        *Show the ~/Library folder
        chflags nohidden ~/Library

        *Disable ping dropdowns
        defaults write com.apple.iTunes hide-ping-dropdown true