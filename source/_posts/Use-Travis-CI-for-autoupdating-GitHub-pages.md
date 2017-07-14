---
title: Use Travis CI for autoupdating GitHub pages
tags:
  - Travis CI
  - github
categories:
  - memo
date: 2017-07-13 15:02:38
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

## Travis CI settings

Good thing is, Travis CI is [well-documented](https://docs.travis-ci.com/user/getting-started "Getting started"). To get started, you may want to sign in and synchronize your special repositories from GitHub first simply by clicking on the slide-bar of your projects.

{% asset_img synbar.png %}

Next, click on that gear to set for the project. 

{% asset_img settings.png %}

You have to add environment variables `GH_REf` and `GH_TOKEN` and use them in your `.travis.yml` for Travis-CI to push the build result to your project. 

`GH_REF` is something like github.com/username/repo.git.
And `GH_TOKEN` can be generated in your own [github settings](https://github.com/settings/tokens). 

{% asset_img token.png %}

## `.travis.yml`

Then, add a `.travis.yml` file to your repository to tell Travis CI what needs to done for building. I'd like to post my `.travis.yml` for your reference here.

```yaml
language: node_js
node_js: stable

# Travis-CI Caching
cache:
  directories:
    - node_modules

# S: Build Lifecycle
install:
  - npm install

script:
  - hexo cl
  - hexo g

after_script:
  - cd ./public
  - git init
  - git config user.name "lijxug"
  - git config user.email "lijxug@gmail.com"
  - git add .
  - git commit -m "Update docs"
  - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
# E: Build LifeCycle
# my blog stores in `master` branch

# And my source code are in `source` branch
branches:
  only:
    - source 
```