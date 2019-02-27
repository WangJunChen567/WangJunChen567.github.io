---
layout: post
title: Build Local Jekyll Environment
date: 2018-09-07 20:25:00 +0800
description: Decription of how to build your local jekyll environment in a Win10 PC 
img: github-page-and-jekyll.png
tags: [Github page, Jekyll, Local environment]
---

To preview our github page with jekyll template instantly, we need to install jeyll and bundler locally in our PC. 
Now it is quite convenient to do this in a Window 10 PC, since in Microsoft Store we can install a Linux subsystem, which shares the whole hard disk in PC with the Window 10 system.

## 1. Install Linux in Microsoft Store
I install the Ubuntu 18.04.

## 2. Install gem in Linux
Open the Linux terminal and run this command:
```
sudo apt install ruby ruby-dev
```

## 3. Change the ruby source
The original ruby source is too slow to reach in China, so I change the ruby source to ruby-china mirror:
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
CD into your github page directory and install needed gem packages:
```
cd [your github page directory]
sudo bundle install
```

## 7. Begin your local serve
```
sudo bundle exec jekyll serve
```