# Mender
A tool that makes updating your framework super easy!

This tiny software makes it possible to update any framework or GitHub repository that you use.

Using Mender, you can:
- download repositories from GitHub based on a specific version
- make changes to the code, update or downgrade the framework, resolve the merge conflicts just once
- keep track of the changes in the framework

What does my log look like?
```sh
*   Added feature 5 to my project
|
*   Added feature 4 to my project
|
*   Merged laravel/laravel (v10.2.8) into project
|\  
| * laravel/laravel (v10.2.8)
| |
* | Added feature 3 to my project
| |
* | Merged laravel/laravel (v10.2.4) into project
|\|
| * laravel/laravel (v10.2.4)
| |
* | Added feature 2 to my project
| |
* | Added feature 1 to my project
| |
* | Merged laravel/laravel (v9.5.2) into project
|\|
| * laravel/laravel (v9.5.2)
|
*   Initialized a new project using ronvanderheijden/mender
```

## Requirements
To use Mender, you only need [Git](https://git-scm.com/downloads) installed.

## Installation
```sh
# 1. download mender
curl --silent https://raw.githubusercontent.com/ronvanderheijden/mender/master/mend > mend

# 2. change permissions
chmod +x mend

# 3. add mender to your work tree
git add mend && git commit -m'Added ronvanderheijden/mender'

# 4. run mender
./mend <repository> <version> [destination=src]
```

## Why would I need it?
When you add custom code to a repository, or change some parts of a repository, updating the repository brings some problems. For example when you've updated a config file, but the repository adds new features to the same file. In this case, you have a merge conflict that you manually have to resolve, not once, but every time you update the repository.

Mender helps you with those problems using the advanced feature of Git called orphan branches.

## How does it work?
Mender creates an orphan branch to store the repository. Mender then merges the orphan branch to your current branch. This way you have the repository changes decoupled from your (custom) code. Every new version of the repository is merged in the orphan branch, and then merged to your current branch. Every conflict that you have resolved in the past, will be remembered in the future.

## A full example
```sh
# create new directory
mkdir mender && cd mender

# create an empty Git repository
git init

# download mender
curl --silent https://raw.githubusercontent.com/ronvanderheijden/mender/master/mend > mend

# change permissions
chmod +x mend

# add mender to your work tree
git add mend && git commit -m'A new project using ronvanderheijden/mender'

# install laravel
./mend laravel/laravel v9.5.2

# upgrade laravel
./mend laravel/laravel v10.2.4

# update laravel
./mend laravel/laravel v10.2.8
```
