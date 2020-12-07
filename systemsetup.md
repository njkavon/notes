##### few privacy command-line tweaks compiled from comprehensive https://github.com/drduh/macOS-Security-and-Privacy-Guide

Disable Spotlight Suggestions in both the Spotlight preferences and Safari's Search preferences to avoid your search queries being sent to Apple. Enable Secure Keyboard Entry in Terminal.

```
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setstealthmode on
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
defaults write com.apple.finder AppleShowAllFiles -bool true
chflags nohidden ~/Library
defaults write com.apple.screensaver askForPassword -int 1
defaults write com.apple.screensaver askForPasswordDelay -int 0
defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false
sudo defaults write /Library/Preferences/com.apple.mDNSResponder.plist NoMulticastAdvertisements -bool YES
defaults write com.apple.CrashReporter DialogType none
```

```
# check for TRIM support
system_profiler -detailLevel mini SPSerialATADataType

sudo trimforce enable
```



##### brew - package management for Mac - https://brew.sh/

```
brew analytics off

# update homebrew itself and the package "lists"
brew update
# upgrade all the software homebrew installed
brew upgrade

# check package dependencies in tree view
brew deps pyenv --tree xpdf

brew list
brew cleanup

# to delete preferences with package
brew cask zap
```

```
brew install pyenv pyenv-virtualenv

brew cask install sublime-text firefox vscodium appcleaner mpv table-tool applepi-baker tiny-player calibre tomighty tor-browser imageoptim sensiblesidebuttons xact macpass mounty macdown

# quick look plugins
brew cask install qlstephen qlmarkdown quicklook-json quicklook-csv
```



##### random tweaks

```
# sync keyboard repeat rate to display refresh rate
defaults write NSGlobalDomain KeyRepeat -int 1
```

```
# open Sublime Text files/dirs right from terminal
$ sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl

# open curr dir
$ subl .
```



HTTPS Everywhere extension can redirect Youtube to Invidious, and Twitter to Nitter.
ctrl+z, a link called `Debugging Rulesets (advanced)` should magically appear..


       <ruleset name="yt2in_nojs">
          <target host="youtube.com" />
          <target host="www.youtube.com" />
    
          <rule from="^https?://(www\.)?youtube.com/watch\?"
                to="https://invidious.tube/watch?nojs=1&amp;" />
        </ruleset>
        
        <ruleset name="twit2nit">
          <target host="twitter.com" />
          <target host="www.twitter.com" />
    
          <rule from="^https?://(www\.)?twitter.com/"
                to="https://nitter.net/" />
        </ruleset>



copy path of the file in finder with `command + option + c` 

`option + backspace` deletes whole word


