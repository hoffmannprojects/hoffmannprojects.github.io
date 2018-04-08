---
layout: post
title: Setting up Jekyll for Github Pages locally
summary: "This post has TL;DR character. Its purpose is to provide a quick 'how to' reference, which might be useful to others. No jokes or funny stories."
---

# Installation
## Mac
[Setting up your GitHub Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/ "Official Github documentation")

Keeping your site up to date with the GitHub Pages gem
- If you followed our setup recommendations and installed Bundler, run bundle update github-pages or simply bundle update and all your gems will update to the latest versions.
- If you don't have Bundler installed, run gem update github-pages

## Windows 10
Summary: 
- Install the Windows Subsystem for Linux (WSL) with bash on Ubuntu. 
- WSL is a separate environment (unlike git bash), intended for accessing Windows files from Linux, utilizing the new bash.exe (not the other way around!).
- Windows drives are mounted under /mnt, so the C drive can be accessed with cd /mnt/c.
- Tools installed in WSL (git for example) are independent from the Windows system.

### [Install the new Bash on Ubuntu](https://docs.microsoft.com/en-us/windows/wsl/install-win10) with the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (Anniversary update, Windows build 16215, or later): 
1. Open Powershell as administrator and run 
  ```bash
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
  ```
2. Restart computer when prompted.
  2. Install “Ubuntu” Linux distribution from the Microsoft store.
  2. Select “Launch”, wait for installation to finish.
  2. Create new user account on Ubuntu (completely independent from the Windows user account).

### [Install dependencies on Ubuntu](https://jekyllrb.com/docs/windows/#installation) (In the Ubuntu command prompt (bash)):
1. Update repo list and packages: 
```bash
sudo apt-get update -y && sudo apt-get upgrade -y
```
2. Install optimized versions of Ruby for Ubuntu:
```bash
sudo apt-add-repository ppa:brightbox/ruby-ng
```
(Confirm as prompted..)
```bash
sudo apt-get update
```
```bash
sudo apt-get install ruby2.3 ruby2.3-dev build-essential dh-autoreconf
```
(Confirm as prompted..)
3. Update Ruby gems:
```bash
sudo gem update
```
4.. Install Bundler (recommended by github instead of installing jekyll direktly via `gem install jekyll`):
```bash
sudo gem install bundler
```
6. Cleanup of packages not needed:
```bash
sudo apt autoremove
```
### (Optional for better readability: [Change bash colors and font to Ubuntu scheme](https://medium.com/@jgarijogarde/make-bash-on-ubuntu-on-windows-10-look-like-the-ubuntu-terminal-f7566008c5c2)

### Create a new repository (or in an existing Jekyll repository)
1. Check, if Gemfile is present (used by Ruby to track your site's dependencies)
```bash
ls
```

2. Make sure, these lines are present in existing or newly created Gemfile:
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

4.. Install Jekyll and other dependencies:
```bash
bundle install
```
If nokogiri installation results in error, try:
```
sudo gem update --system 2.7.4
sudo gem update
sudo gem install bundler
```

5. Check if Jekyll installed properly:
```bash
jekyll -v
```


### For Node.Js and Gulp (required by the sleek theme this website uses)
On Mac:
Open the Terminal app and type 
```bash
brew install node
```
To make sure you have Node and NPM installed, type in terminal (should print the version number):
```bash 
node -v
```
To see if NPM is installed, type in terminal (should print the version number): 
```bash
npm -v 
```

How to Update Node and NPM on Mac:
Using Homebrew, make sure Homebrew has the latest version of the Node package:
```bash
brew update
```
then to update Node:
```bash
brew upgrade node
```

Gulp.js (optional, but recommended for the sleek theme)
```bash
sudo npm install -g gulpfile
```

Up & Running
Inside the directory run 
```bash
bundle install
``` 
and 
```bash
npm install
```
If you want to use gulp.js run gulp or npm start
if you don't want to use gulp you can simply run bundle exec jekyll serve

