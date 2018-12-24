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

```

```



## Push to GitHub



## Create GitHub pages site





[http://127.0.0.1:8000/]: 