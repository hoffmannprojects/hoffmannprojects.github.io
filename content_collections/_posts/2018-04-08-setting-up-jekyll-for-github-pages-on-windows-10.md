---
layout: post
title: Setting up Jekyll for Github Pages on Windows 10
summary: "This post has TL;DR character. Its purpose is to provide a quick 'how to' reference, which might be useful to others. No jokes or funny stories."
---

# Summary: 
- Install the Windows Subsystem for Linux (WSL) with bash on Ubuntu. 
- WSL is a separate environment (unlike git bash), intended for accessing Windows files from Linux, utilizing the new bash.exe (not the other way around!).
- Windows drives are mounted under /mnt, so the C drive can be accessed with `cd /mnt/c`.
- Tools installed in WSL (git for example) are independent from the Windows system.


# Installation

## [If not already installed] [Install the new Bash on Ubuntu](https://docs.microsoft.com/en-us/windows/wsl/install-win10){:target="_blank"} 
(Requires Anniversary update, Windows build 16215, or later): 

1. Open Powershell as administrator and run 
  ```bash
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
  ```
2. Restart computer when prompted.
2. Install “Ubuntu” Linux distribution from the Microsoft store.
2. Select “Launch”, wait for installation to finish.
2. Create new user account on Ubuntu (completely independent from the Windows user account).

1. [Optional] for better readability in bash: 
[change bash colors and font](https://medium.com/@jgarijogarde/make-bash-on-ubuntu-on-windows-10-look-like-the-ubuntu-terminal-f7566008c5c2){:target="_blank"}

## [Install dependencies on Ubuntu](https://jekyllrb.com/docs/windows/#installation-via-bash-on-windows-10){:target="_blank"}:
### [Install Ruby Version Manager (RVM)](https://github.com/rvm/ubuntu_rvm):

1. Add the PPA and install the package
```bash
sudo apt-add-repository -y ppa:rael-gc/rvm
sudo apt-get update
sudo apt-get install rvm

# Add user to rvm Group.
sudo usermod -a -G rvm <userName>
```

2. Restart the system and close bash.

3. Install Ruby via RVM:
```
rvm install 2.4
rvm install 2.4-dev
rvm install build-essential
sudo apt install dh-autoreconf

# Verify that Ruby was properly installed by printing the version number:
ruby -v
```

**Note: Don't run ruby-related commands as `sudo` when rvm is installed!**

### Update Gems, install jekyll and bundler:
```
# Update gems.
gem update

# Install jekyll and bundler.
gem install jekyll bundler

# Remove packages not needed.
sudo apt autoremove

# Check if Jekyll installed properly.
jekyll -v
```

## Install other dependencies: 

1. Create a new repository (or use an existing Jekyll repository) and cd into it.

2. Check, if Gemfile is present (used by Ruby to track your site's dependencies)
```bash
ls
```

3. Make sure, these lines are present in existing or newly created Gemfile:
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

4. Install Jekyll and other dependencies via bundler:
```bash
bundle install
```

*If nokogiri installation results in error, try ([official Nokogiri installation instructions](http://www.nokogiri.org/tutorials/installing_nokogiri.html){:target="_blank"}):*
```
sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev

bundle install

# Check if Jekyll installed properly:
jekyll -v
```


## [Optioinal] Install Node.Js and Gulp (required by the sleek theme, this website uses)

### Install Node version manager (nvm) via latest install command from [the official nvm github reposirotry](https://github.com/creationix/nvm){:target="_blank"}.

1. At the time of writing, the latest is: 
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

2. Restart bash.

3. Confirm by checking:
```bash
nvm --version
```

### Install node:
```bash
nvm install node
```


### [Install gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md){:target="_blank"} (If you've previously installed gulp globally, run npm rm --global gulp before following these instructions.):
```bash
# cd into your repository.
cd <repository/path>

npm install --global gulp-cli

npm install --save-dev gulp@next

# If you encounter warnings, run:
# npm audit fix

# Inside the repository, run:
npm install
```

# Troubleshooting

## If `npm install` throws an error that it is missing python:
Check my guide for installing python with a package manager or

``` 
sudo apt install python

npm install
```      

## If Gulp throws an error "`check_for_activated_spec!': You have already activated <name>":

Uninstall conflicting <name> version with:
```
sudo gem uninstall <name>
```
