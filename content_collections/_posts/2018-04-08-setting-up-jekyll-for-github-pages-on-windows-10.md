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

## [Install the new Bash on Ubuntu](https://docs.microsoft.com/en-us/windows/wsl/install-win10) 
(Requires Anniversary update, Windows build 16215, or later): 

1. Open Powershell as administrator and run 
  ```bash
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
  ```
2. Restart computer when prompted.
2. Install “Ubuntu” Linux distribution from the Microsoft store.
2. Select “Launch”, wait for installation to finish.
2. Create new user account on Ubuntu (completely independent from the Windows user account).

## [Install dependencies on Ubuntu](https://jekyllrb.com/docs/windows/#installation):
1. (In the Ubuntu command prompt (bash)) Update repo list and packages: 
```bash
sudo apt-get update -y && sudo apt-get upgrade -y
```
2. Install optimized versions of Ruby for Ubuntu (confirm when prompted.):
```bash
sudo apt-add-repository ppa:brightbox/ruby-ng
```
```
sudo apt-get update
```
```
sudo apt-get install ruby2.3 ruby2.3-dev build-essential dh-autoreconf
```

3. Update Ruby gems:
```bash
sudo gem update
```

## Install Bundler (recommended by github):
1. Install
```bash
sudo gem install bundler
```
2. Remove packages not needed:
```bash
sudo apt autoremove
```

## (Optional) for better readability in bash: 
[change bash colors and font](https://medium.com/@jgarijogarde/make-bash-on-ubuntu-on-windows-10-look-like-the-ubuntu-terminal-f7566008c5c2)


## Install Jekyll and other dependencies: 

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

5. If nokogiri installation results in error, try ([official Nokogiri installation instructions](http://www.nokogiri.org/tutorials/installing_nokogiri.html)):
```
sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev
```
```
bundle install
```

5. Check if Jekyll installed properly:
```bash
jekyll -v
```


## (Optioinal) Install Node.Js and Gulp (required by the sleek theme, this website uses)

1. Install Node version manager (nvm) via latest install command from [the official nvm github reposirotry](https://github.com/creationix/nvm).
At the time of writing, the latest is: 
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

2. Restart bash.

3. Confirm by checking:
```bash
nvm version
```
4. Install node:
```bash
nvm install node
```
5. cd into your repository.

6. [Install gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md) (If you've previously installed gulp globally, run npm rm --global gulp before following these instructions.):
```bash
npm install --global gulp-cli
```
```
npm install --save-dev gulp@next
```

7. Inside the repository, run:
```bash
npm install
```

# Troubleshooting

## If `npm install` throws an error that it is missing python, run:
``` 
sudo apt install python
```
```
npm install
```      

## If Gulp throws an error "`check_for_activated_spec!': You have already activated <name>":

Uninstall conflicting <name> version with:
```
sudo gem uninstall <name>
```
