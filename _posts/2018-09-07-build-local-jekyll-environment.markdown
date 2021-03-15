---
layout: post
title: Build Local Jekyll Environment
date: 2018-09-07 20:25:00 +0800
description: Decription of how to build your local jekyll environment in a Win10 PC 
img: github-page-and-jekyll.png
tags: [Github page, Jekyll, Local environment]
---

To instantly preview github pages using jekyll templates, a local jekyll environment is required. With the officially maintained Windows Subsystem for Linux (WSL) (which shares a hard drive with the Window 10 main system) hitting the MicroSoft Store, it is now much easier to build a local jekyll environment on a Window 10 PC.

## 1. Install a WSL in Microsoft Store
Turning on the WSL feature, restarting your computer and initially setting up your Linux account are necessary to run WSL for the first time.

## 2. Install gem in WSL
Open a Linux terminal and run the following command
```
sudo apt install ruby ruby-dev
```

## 3. Change the ruby source
If the original ruby source is too slow to access, you can change it to a ruby-china mirror
```
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```

## 4. Install jekyll and bundler with gem
```
sudo gem install jekyll bundler
```

## 5. Change bundler source
```
sudo bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

## 6. Install missing gems
Go to the root directory of the github page and run the following command to install the required gem packages
```
cd [your github page directory]
sudo bundle install
```

## 7. Begin the local serve
```
sudo bundle exec jekyll serve
```