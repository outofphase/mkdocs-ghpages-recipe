# Recipe for websites hosted on GitHub Pages

## Overview

A step-by-step walkthrough to create a collaborative documentation project using **mkdocs** that has a website hosted on GitHub Pages.

Pre-requisites:

* an OS X or Linux computer with **git** and **mkdocs** installed and a web browser
* internet access and a GitHub account
* a text editor &ndash; any text editor will do but as the documentation will be created in **markdown** files it will be useful if the editor has support for markdown syntax highlighting, for example **typora**.

## Create project

Create the local project directory in a suitable location:

```bash
galibier:~ david$ cd Projects
galibier:Projects david$ mkdocs new mkdocs-ghpages-recipe
INFO    -  Creating project directory: mkdocs-ghpages-recipe 
INFO    -  Writing config file: mkdocs-ghpages-recipe/mkdocs.yml 
INFO    -  Writing initial docs: mkdocs-ghpages-recipe/docs/index.md 
```

Replace the `index.md` file in the `docs` directory with the site content, written as markdown text. Edit the `mkdocs.yml` file to set the project name.

Buld the site by running `mkdocs build` in the project directory and then test the site by running `mkdocs serve` and accessing http://127.0.0.1:8000/ in web browser. Make further changes to the files as needed and use Ctrl-C to stop the web server when finished.

## Create local git repository of the files

Create a local git repository of the project files:

```bash
galibier:~ david$ cd Projects
galibier:Projects david$ git init mkdocs-ghpages-recipe/
Initialized empty Git repository in /Users/david/Projects/mkdocs-ghpages-recipe/.git/
```

Add a README file and a LICENSE file for your project:

```bash
galibier:Projects david$ cd mkdocs-ghpages-recipe/
galibier:mkdocs-ghpages-recipe david$ echo "A step-by-step walkthrough to ..." >> README.md
galibier:mkdocs-ghpages-recipe david$ echo "This project is in the PUBLIC DOMAIN" >> LICENSE.md
```

Add a `.gitignore` file in the project directory so that generated files are not added to the repository:

```bash
galibier:mkdocs-ghpages-recipe david$ echo "site/" >> .gitignore
```

Create a local git repository and add the project files to it:

```bash
galibier:Projects david$ git init mkdocs-ghpages-recipe/
Reinitialized existing Git repository in /Users/david/Projects/mkdocs-ghpages-recipe/.git/
galibier:Projects david$ cd mkdocs-ghpages-recipe/
galibier:mkdocs-ghpages-recipe david$ git add .
galibier:mkdocs-ghpages-recipe david$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitignore
	new file:   LICENSE.md
	new file:   README.md
	new file:   docs/index.md
	new file:   mkdocs.yml

galibier:mkdocs-ghpages-recipe david$ git commit -m 'initial commit'
[master (root-commit) 32b167d] initial commit
 5 files changed, 75 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 LICENSE.md
 create mode 100644 README.md
 create mode 100644 docs/index.md
 create mode 100644 mkdocs.yml
```

## Push to GitHub

Create a new repository on GitHub but do _not_ initialize the new repository with any files. Copy the remote respository URL.

On the local computer:

* use the URL to add this as a remote repository
* push the local repository to GitHub

```bash
galibier:mkdocs-ghpages-recipe david$ git remote add origin https://github.com/outofphase/mkdocs-ghpages-recipe.git
galibier:mkdocs-ghpages-recipe david$ git remote -v
origin	https://github.com/outofphase/mkdocs-ghpages-recipe.git (fetch)
origin	https://github.com/outofphase/mkdocs-ghpages-recipe.git (push)
galibier:mkdocs-ghpages-recipe david$ git push -u origin master
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (8/8), 1.44 KiB | 1.44 MiB/s, done.
Total 8 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/outofphase/mkdocs-ghpages-recipe.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'. 
```
> For more information see https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/


## Create GitHub Pages site

Use `mkdocs` to create a branch for the generated site files and to push it to GitHub. These will be available from the GitHub Pages website.

```bash
galibier:mkdocs-ghpages-recipe david$ mkdocs gh-deploy
INFO    -  Cleaning site directory 
INFO    -  Building documentation to directory: /Users/david/Projects/mkdocs-ghpages-recipe/site 
WARNING -  Version check skipped: No version specificed in previous deployment. 
INFO    -  Copying '/Users/david/Projects/mkdocs-ghpages-recipe/site' to 'gh-pages' branch and pushing to GitHub. 
INFO    -  Your documentation should shortly be available at: https://outofphase.github.io/mkdocs-ghpages-recipe/ 
```

## Maintaining the site

Since the site is generated locally and pushed to the GitHub webserver, updating the site after making local changes requires two steps so that the repository and site stay in sync:

* commit local changes and push the `master` branch to GitHub
* generate the new site files and push the `gh-pages` branch to GitHub, which is done by mkdocs.

Rather than polluting the GitHub repository with every experimental change, you can create a local branch for testing. Further branches from that can be created to work on specific changes too if you want to work on things in parallel. Then merge into the mainline when ready to publish.

``` bash
galibier:mkdocs-ghpages-recipe david$ git branch testing
galibier:mkdocs-ghpages-recipe david$ git branch
  gh-pages
* master
  testing
galibier:mkdocs-ghpages-recipe david$ git checkout testing
Switched to branch 'testing'
galibier:mkdocs-ghpages-recipe david$ git branch branching
galibier:mkdocs-ghpages-recipe david$ git branch
  branching
  gh-pages
  master
* testing
galibier:mkdocs-ghpages-recipe david$ git checkout branching
Switched to branch 'branching'
galibier:mkdocs-ghpages-recipe david$ git status
On branch branching
nothing to commit, working tree clean
```

Make the changes and test them locally:

``` bash
galibier:mkdocs-ghpages-recipe david$ mkdocs build
INFO    -  Cleaning site directory 
INFO    -  Building documentation to directory: /Users/david/Projects/mkdocs-ghpages-recipe/site 
galibier:mkdocs-ghpages-recipe david$ mkdocs serve
INFO    -  Building documentation... 
INFO    -  Cleaning site directory 
```

Commit the changes when ready and then merge completed change branch into the testing branch, generate and check the site there:

``` bash
galibier:mkdocs-ghpages-recipe david$ git status
On branch branching
nothing to commit, working tree clean
galibier:mkdocs-ghpages-recipe david$ git checkout testing
Switched to branch 'testing'
galibier:mkdocs-ghpages-recipe david$ git merge branching
Updating 7cc566d..bbdb1e4
Fast-forward
 docs/index.md | 47 +++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 47 insertions(+)
galibier:mkdocs-ghpages-recipe david$ git status
On branch testing
nothing to commit, working tree clean
galibier:mkdocs-ghpages-recipe david$ git branch
  branching
  gh-pages
  master
* testing
galibier:mkdocs-ghpages-recipe david$ git branch --delete branching
galibier:mkdocs-ghpages-recipe david$ mkdocs build
INFO    -  Cleaning site directory 
INFO    -  Building documentation to directory: /Users/david/Projects/mkdocs-ghpages-recipe/site 
galibier:mkdocs-ghpages-recipe david$ mkdocs serve
INFO    -  Building documentation... 
INFO    -  Cleaning site directory 
```

Finally update the mainline, then generate the site files and push it all to GitHub:

``` bash
galibier:mkdocs-ghpages-recipe david$ git status
On branch testing
nothing to commit, working tree clean
galibier:mkdocs-ghpages-recipe david$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
galibier:mkdocs-ghpages-recipe david$ git merge testing
Updating 4eb3319..283f7a3
Fast-forward
 docs/index.md | 80 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
 1 file changed, 79 insertions(+), 1 deletion(-)
galibier:mkdocs-ghpages-recipe david$ git status
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
galibier:mkdocs-ghpages-recipe david$ git push
Enumerating objects: 19, done.
Counting objects: 100% (19/19), done.
Delta compression using up to 4 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (16/16), 3.52 KiB | 3.52 MiB/s, done.
Total 16 (delta 7), reused 0 (delta 0)
remote: Resolving deltas: 100% (7/7), completed with 1 local object.
To https://github.com/outofphase/mkdocs-ghpages-recipe.git
   32b167d..283f7a3  master -> master
galibier:mkdocs-ghpages-recipe david$ mkdocs gh-deploy
INFO    -  Cleaning site directory 
INFO    -  Building documentation to directory: /Users/david/Projects/mkdocs-ghpages-recipe/site 
INFO    -  Copying '/Users/david/Projects/mkdocs-ghpages-recipe/site' to 'gh-pages' branch and pushing to GitHub. 
INFO    -  Your documentation should shortly be available at: https://outofphase.github.io/mkdocs-ghpages-recipe/ 
```

