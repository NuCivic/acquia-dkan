DKAN on Acquia
==============

[![Build Status](https://travis-ci.org/NuCivic/acquia-dkan.svg)](https://travis-ci.org/NuCivic/acquia-dkan)
7.x-1.4

## Prepare your repo

On 
Save your settings file

```bash
$ mkdir assets
$ mv docroot/sites/default/settings.php assets/
$ ln -s ../../../assets/settings.php docroot/sites/default/settings.php
```

Save your custom modules

```bash
$ mkdir projects
$ mv docroot/sites/all/* projects/
$ rm -rf docroot/sites/all
$ ln -s ../../projects docroot/sites/all
```

Add this repo as a remote and merge changes

```bash
$ git remote add dkan-updates https://github.com/NuCivic/acquia-dkan.git
```

After that your **.git/config** file should look like this:

```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	ignorecase = true
	precomposeunicode = true
[remote "origin"]
	url = git@github.com:NuCivic/acquia-dkan-test.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

```bash
$ git fetch dkan-updates
```

## Update dkan

```bash
# create a branch so you can try this safely
$ git checkout -b updating_dkan
# fetch update from dkan-updates remote
$ git fetch dkan-updates
$ git merge dkan-updates/master -X theirs
```

After the merge check if the diff looks reasonable

```bash
$ git diff master
```

If it does, update your master branch

```bash
$ git checkout master
$ git rebase updating_dkan
$ git branch -D updating_dkan
$ git push origin master
```
