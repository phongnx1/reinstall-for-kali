- [MacOS](#macos)
  - [Useful commands](#useful-commands)
    - [1. Turn Off Dashboard](#1-turn-off-dashboard)
    - [2. Create a File Of Any Size](#2-create-a-file-of-any-size)
    - [3. Check the Uptime Of Your Mac](#3-check-the-uptime-of-your-mac)
    - [4. Enable Text Selection in Quick Look](#4-enable-text-selection-in-quick-look)
    - [5. Change Screenshot Location](#5-change-screenshot-location)
    - [6. Change Screenshot File Format](#6-change-screenshot-file-format)
    - [7. Records all terminal output (3rd party)](#7-records-all-terminal-output-3rd-party)
    - [8. Launch application from terminal: edit ```.zshrc``` and add these lines at the end](#8-launch-application-from-terminal-edit-zshrc-and-add-these-lines-at-the-end)
    - [9. Installing multiple versions of Python](#9-installing-multiple-versions-of-python)
    - [10. Run, stop Docker from terminal](#10-run-stop-docker-from-terminal)
  - [Useful key shortcuts](#useful-key-shortcuts)
    - [1. Show hidden files in Finder ```shift + command + .```](#1-show-hidden-files-in-finder-shift--command)
  - [Error](#error)
    - [1. rails:](#1-rails)
# MacOS
## Useful commands

### 1. Turn Off Dashboard

- Dashboard was once the future of quick-to-access apps such as a calculator and sticky notes. Despite being quite popular for a few years, it’s quickly faded into obscurity. It’s still around and usually opened accidentally.

- I use Mission Control extensively and have it positioned on the far left but, honestly, I prefer it gone completely. Thankfully, Dashboard can be permanently silenced:

```
defaults write com.apple.dashboard mcx-disabled -boolean TRUE
killall Dock
```

- You’ll find that Dashboard is no longer running, along with any widgets you might have had inside. Don’t worry, you can bring it back if necessary:

```
defaults write com.apple.dashboard mcx-disabled -boolean FALSE
killall Dock
```

### 2. Create a File Of Any Size

- Create an empty file of any size that we want.

```
mkfile 1g test.abc
```

- Can specify the file size in bytes (b), kilobytes (k), megabytes (m) or gigabytes (g). The above example creates a test file of 1GB called test.abc but you can name it whatever you wish and it doesn’t need to have a file extension.

### 3. Check the Uptime Of Your Mac

- To see how long our Mac has gone without a restart
```
uptime
```

### 4. Enable Text Selection in Quick Look

```
defaults write com.apple.finder QLEnableTextSelection -bool TRUE
killall Finder
```

- To revert the changes:
```
defaults write com.apple.finder QLEnableTextSelection -bool FALSE
killall Finder
```

### 5. Change Screenshot Location

```
defaults write com.apple.screencapture location /drag/location/here
killall SystemUIServer
```

- To undo the changes

```
defaults write com.apple.screencapture location ~/Desktop
killall SystemUIServer
```

### 6. Change Screenshot File Format

```
defaults write com.apple.screencapture type PDF
killall SystemUIServer

defaults write com.apple.screencapture type png
killall SystemUIServer
```

### 7. Records all terminal output (3rd party)

- Install the recorder
```
brew install asciinema
```
- Start recording
```
asciinema rec
```
- This spawns a new shell instance and records all terminal output. When you're ready to finish simply exit the shell either by typing ```exit``` or hitting ```Ctrl-D```.

### 8. Launch application from terminal: edit ```.zshrc``` and add these lines at the end

```zsh
# export for mysql
export PATH="/usr/local/mysql/bin:$PATH"

# export for maven
export M2_HOME=/Applications/apache-maven-3.5.4
export PATH=$PATH:$M2_HOME/bin

# for vscode
function code {
    if [[ $# = 0 ]]
    then
        open -a "Visual Studio Code"
    else
        local argPath="$1"
        [[ $1 = /* ]] && argPath="$1" || argPath="$PWD/${1#./}"
        open -a "Visual Studio Code" "$argPath"
    fi
}
# for sublime
alias subl="/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl"

# for ngrok
alias ngrok="/Users/sanh/Downloads/ngrok/ngrok"

# for pyenv
eval "$(pyenv init -)"

# for rbenv
# eval "$(rbenv init -)"
export PATH="$HOME/.rbenv/shims:$PATH"
```

### 9. [Installing multiple versions of Python](https://github.com/pyenv/pyenv)
- tutorial [https://weknowinc.com/blog/running-multiple-python-versions-mac-osx](https://weknowinc.com/blog/running-multiple-python-versions-mac-osx)

### 10. Run, stop Docker from terminal

```sh
alias docker-service="open -a /Applications/Docker.app --hide"
alias docker-stop="ps -ax | grep "/Applications/Docker.app/Contents/MacOS/Docker" | head -1 | awk {'print $1'} | xargs kill -9"
```

## Useful key shortcuts

### 1. Show hidden files in Finder ```shift + command + .```


## Error

### 1. rails:

- bundle install error: sqlite3

```sh
bundle config build.sqlite3 --with-sqlite3-include=$HOME/include --with-sqlite3-lib=$HOME/lib --with-sqlite3-dir=$HOME/bin
bundle install
```
- bundle install error: mysql2
```
Errno::EPERM: Operation not permitted @ apply2files -
/Users/me/.rbenv/versions/2.5.1/lib/ruby/gems/2.5.0/gems/mysql2-0.4.9/CHANGELOG.md
An error occurred while installing mysql2 (0.4.9), and Bundler cannot continue.
Make sure that `gem install mysql2 -v '0.4.9' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  mysql2
```

```
sudo gem install mysql2 -v '0.4.9' -- --srcdir=/usr/local/mysql/include
```
