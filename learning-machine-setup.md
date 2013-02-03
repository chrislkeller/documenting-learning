
- Install [Homebrew](http://mxcl.github.com/homebrew/):

		ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"

- Use Homebrew to install the following:

		brew install ack
		brew install freetype
		brew install imagemagick
		brew install libpng
		brew install mongodb
		brew install readline
		brew install curl
		brew install gdbm
		brew install jpeg
		brew install libtool
		brew install pkg-config
		brew install sqlite
		brew install ec2-api-tools
		brew install git
		brew install libevent
		brew install memcached
		brew install python --framework --universal
		brew install wget
		brew install coda-cli

- Install [Adium](http://adium.im/), [Alfred](http://www.alfredapp.com/), AppCleaner, Briquette, Byword, calibre, Captur, CCleaner, CheatSheet, Coda 2, CSVEdit, DashExpander, DavMail, Dropbox, [Evernote](http://evernote.com/), Firefox, GitHub, GitX, Google Chrome, Google Drive, Google Refine, Growl, Hiss, Keynote, Kindle, MacDropAny, MAMP, MenuBarFilter, MindNode Lite, Mou, Patterns, PGAdmin, Pocket, Postbox, Read Later, [Reeder](http://madeatgloria.com/brewery/silvio/reeder), Sigil, SketchBookExpress, StuffIt Expander, TileMill, TweetDeck, [Twitter](http://itunes.apple.com/app/twitter/id333903271).

- Install XCode
- Install XCode command line tools: Preferences --> Downloads --> Command Line Tools



- Install [DavMail](http://davmail.sourceforge.net/macosxsetup.html) for email client to access web mail.

- Install [Ubuntu Mono font library](http://font.ubuntu.com/#charset-mono-regular).

- Add bash.mode, django.mode, markdown.mode and WordPress.mode to Coda2.

- Install [tomorrow-theme](https://github.com/chriskempson/tomorrow-theme) for Coda2.



######### set paths for ruby & python #########
export PATH="/usr/local/share/python:/usr/local/bin/python:/usr/local/bin:/Users/ckeller/.rvm/bin:/usr/bin:/bin:/usr/sbin:/sbin"

######### virtualenvwrapper settings #########
export WORKON_HOME=$HOME/.virtualenvs
export PIP_VIRTUALENV_BASE=$WORKON_HOME
export PIP_RESPECT_VIRTUALENV=true
source /usr/local/bin/virtualenvwrapper.sh




### BEGIN NOTES FOR BRIAN BOYER AND OTHERS I NEED TO ORGANIZE

https://gist.github.com/1696819







$ brew install readline sqlite gdbm
$ brew install python --universal --framework
$ python --version
Python 2.7

$ mkdir ~/Frameworks
$ ln -s "/usr/local/Cellar/python/2.7.2/Frameworks/Python.framework" ~/Frameworks
$ /usr/local/share/python/easy_install pip
$ /usr/local/share/python/pip install --upgrade distribute

$ pip install virtualenv
$ pip install virtualenvwrapper

----

- Setup RVM with Ruby 1.9.3

rvm install 1.9.3
gem install capistrano

generate ssh keys for github
https://help.github.com/articles/generating-ssh-keys

Apps
----
* [Webkit](http://webkit.org)
* [Chrome](http://www.chromium.org/getting-involved/dev-channel)
* [Firefox](http://www.mozilla.org/en-US/firefox/beta/)
* [Opera](http://www.opera.com/browser/next/)
* [iTerm](http://iterm2.com)
* [FileZilla](http://filezilla-project.org/download.php)
* [Sublime Text](http://www.sublimetext.com/dev)
* [LiveReload](http://livereload.com)
* [LiveReload Extensions](http://help.livereload.com/kb/general-use/browser-extensions)




Install rvm
-------------
```bash
curl https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
```

Install rubies
-------------
```bash
rvm get head
rvm pkg install readline # need it to work correctly with utf-8 characters in irb/pry
rvm install 1.9.3
```

# OS X Preferences

```bash
#Fix fonth smoothing
defaults -currentHost write -globalDomain AppleFontSmoothing -int 0

#Disable window animations
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false

#Enable repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

#Disable webkit homepage
defaults write org.webkit.nightly.WebKit StartPageDisabled -bool true

#Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

#Show Path bar in Finder
defaults write com.apple.finder ShowPathbar -bool true

#Show Status bar in Finder
defaults write com.apple.finder ShowStatusBar -bool true

#Show indicator lights for open applications in the Dock
defaults write com.apple.dock show-process-indicators -bool true

#Enable AirDrop over Ethernet and on unsupported Macs running Lion
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

#Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 0.02

#Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 12

#Disable disk image verification
defaults write com.apple.frameworks.diskimages skip-verify -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true

#Disable Safari’s thumbnail cache for History and Top Sites
defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2

#Enable Safari’s debug menu
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

#Disable the Ping sidebar in iTunes
defaults write com.apple.iTunes disablePingSidebar -bool true

#Add a context menu item for showing the Web Inspector in web views
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

#Show the ~/Library folder
chflags nohidden ~/Library

#Disable ping dropdowns
defaults write com.apple.iTunes hide-ping-dropdown true

```

Set hostname
------------
`sudo scutil --set HostName Work`




#Homebrew


```bash
ruby <(curl -fsSkL raw.github.com/mxcl/homebrew/go)
```

```bash
brew install git ack wget curl memcached libmemcached readline sqlite gdbm pkg-config
```


Install python
------------
```bash
brew install python --framework --universal
```

Add into your ~/.zshrc
```bash
export PATH=/usr/local/share/python:$PATH
```

Change system symlinks
```bash
cd /System/Library/Frameworks/Python.framework/Versions
sudo rm Current
ln -s /usr/local/Cellar/python/2.7.2/Frameworks/Python.framework/Versions/Current
```

Install pip & virtualenv
------------
```bash
easy_install pip
pip install virtualenv
pip install virtualenvwrapper
```

Source virtualenvwrapper script
```bash
source /usr/local/bin/virtualenvwrapper.sh