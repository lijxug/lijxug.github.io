---
title: Use Travis CI for autoupdating GitHub pages
date: 2017-07-13 15:02:38
tags: 
    - Travis CI
    - github
categories: 
    - memo
---

>The idea that use Travis CI to autoupdate GitHub pages is based on a post of IIssNan who also built NexT, the great theme that I am using. 
>
>Link to the original: [http://notes.iissnan.com/2016/publishing-github-pages-with-travis-ci/](http://notes.iissnan.com/2016/publishing-github-pages-with-travis-ci/)

## Introduction
Again, KevinZ recommond this autoupdating method to me. And for better understanding and future use, I decided to write the whole process down in my own way.
<!-- more -->
## Travis CI
[Travis CI](https://travis-ci.org) is a hosted, distributed continuous integration service used to build and test software projects hosted at GitHub.[wiki](https://en.wikipedia.org/wiki/Travis_CI)

## Principle
I'd like to skip the thinking part and focus on the method itself.
First of all, the whole process includes several steps:

1. `git push` changes to the remote repository on Github
2. Travis CI notice the changes and build the project
3. Travis CI export output to Github branch
4. Github build Pages
5. All done and celebrate!

According to IIssNan, the original author, it's quite easy except Step 3.
But, I am not farmiliar with Travis CI either, so that's where I am going to start.

Good thing is, Travis CI is [well-documented](https://docs.travis-ci.com/user/getting-started "Getting started"). To get started, you may want to sign in and synchronize your special repositories from GitHub first. 

Next, get a TOKEN, encrypt it with ``

Then, add a `.travis.yml` file to your repository to tell Travis CI what to build.

The principle of this method. 

{% asset_img travis-encrypt-keys.png The original schematic diagram of the "key"%}

The whole method includes three major steps. First of all, we need to acquire **GitHub Personal Access Token** for 

