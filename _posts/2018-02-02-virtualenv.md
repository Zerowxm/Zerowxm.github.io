---
layout: post
title: Use virtual environment for python projects.
key: 20180202
tags: python virtualenv
---

# What is virtualenv?
[virtualenv](https://virtualenv.pypa.io) is a tool used to create an isolated workspace for a Python application which allows you to work on a specific project without worry of affecting other projects. <br />It has various advantages such as the ability to install modules locally, export a working environment, and execute a Python program in that environment.

# Installation
just run
`pip install virtualenv` in your cmd. <br />Then type `virtualenv --version`, if showed number like 15.1.0, it's installed successfully.

# Use virtualenv
First, create a folder to store your projects, like `mkdir ~/virtualenvironment`, then type `virtualenv ~/virtualenvironment/project`.<br /> To begin with, you have to cd into project directory.<br />
In Linux or MacOS, you can activate virtualenv by typing `source bin/activate`. <br />For Windows, type `.\Scripts\activate`. <br />
Lastly, if you want to exit virtualenv, type `deactivate`.

# Package installation
Packages installed here will not affect the global Python installation. Virtualenv does not create every file needed to get a whole new python environment.<br />
It uses links to global environment files instead in order to save disk space end
speed up your virtualenv. <br />
Therefore, there must already have an active python environment installed on your
system.<br />

To install package in your virtualenv, type like `pip istall tensorflow`.

Hope this post could help you.


