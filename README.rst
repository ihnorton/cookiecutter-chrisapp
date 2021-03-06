#####################
cookiecutter-chrisapp
#####################

A cookiecutter template for ChRIS plugin apps.


Abstract
========

This page describes how to get started with creating a ChRIS plugin. The first-time steps typically involve:

* Installing a python virtual environment for development.
* Creating (if not already done) github and dockerhub accounts.
* Checking out this repo and running the script and then associating the app you are creating with both github and dockerhub.

Requirements
============

* ``Python`` and ``pip`` (which is usually installed with Python)
* Latest ``Docker`` (17.04.0+) if you want to test your plugin's docker image and containers in your local machine. Visit https://docs.docker.com/install/ for installation directions



Install virtualenv and virtualenvwrapper
----------------------------------------
::

    pip install virtualenv virtualenvwrapper


Setup your virtual environments
-------------------------------

Create a directory for your virtual environments e.g::

    mkdir ~/python_envs


Open your .bashrc file::

    vim ~/.bashrc


Add these two lines to your .bashrc file::

    export WORKON_HOME=~/python_envs
    source $(which virtualenvwrapper.sh | head -n 1)


Create a new **Python3** virtual environment::

    mkvirtualenv --python=python3 chrisapp_env


To activate chrisapp_env::

    workon chrisapp_env


To deactivate chrisapp_env::

    deactivate


GitHub Account
--------------

Create a GitHub account on https://github.com/ if you don't already have one.


Docker Hub Account
------------------

Create a Docker Hub account on https://hub.docker.com/ if you don't already have one.


Quickstart
==========

The steps below show how to quickly create and setup a new ChRIS plugin app project.


1. Create a **Python3** virtual environment for your plugin apps and activate it if you haven't created it yet (follow steps in Requirements).

2. Install the latest Cookiecutter in ``chrisapp_env`` if you haven't installed it yet::

    pip install -U cookiecutter


3. Generate a ChRIS plugin app project:

    cookiecutter https://github.com/FNNDSC/cookiecutter-chrisapp.git
    
In running the above command, you will be prompted for an app project name. The app project name should be a valid python module name as described here https://www.python.org/dev/peps/pep-0008/#package-and-module-names.

The interactive script will ask you to choose between two types of ChRIS plugins.

    i.  **fs** plugin app. This doesn't have an input directory as a positional argument
        (does have an output directory though) and always creates a new feed (data container) in the ChRIS system. So **fs** plugins
        are always the single root of a pipeline or tree of plugin executions. They are a way to
        add new data to the system that will then be processed by subsequent **ds** plugins.
    
    ii. **ds** plugin app. This has both input and output directories as positional arguments.
        It never generates a new feed. **ds** plugins can only be run after a **fs** plugin or
        another **ds** plugin as they require an input directory (which is the output of the previous plugin).

    The first plugin of a pipeline would always be a **fs** plugin and the rest would be a chain of **ds**
    plugins creating files in the same single feed that was created by the root **fs** plugin. **Most of the
    time you will be creating a ds plugin when integrating your software application in ChRIS**.


4. Create a new repository on https://github.com/**your_github_username** with the same name as the app project
   directory generated by the previous cookiecutter command. Make sure that the repository is
   public. Don’t initialize the repository with a ``README``, a ``license`` or a ``.gitignore`` file.


5. Change the current working directory to the app project and initialize this local directory
   as a Git repository::

    git init


6. Add and commit the files in the local repository::

    git add .
    git commit -m "First commit"


7. Add the URL for the remote Github repository created in ``step 4`` where your local repository will be pushed::

    git remote add origin **remote_Github_repository_URL** (eg. https://github.com/FNNDSC/pl-neuproseg.git)
    git remote -v


8. Push the changes in your local repository to GitHub::

    git push origin master


9. Create a new automated build and repository on your Docker Hub account (https://hub.docker.com).
   Once you log in, click the Create button in the header and select Automated Build from the
   drop-down menu. The website will walk you through setting up the automated build. Next, when
   prompted for the GitHub repository that you’d like to use for the automated build select
   the repository that you just created.

   For more information on Automated Builds, visit https://docs.docker.com/docker-hub/builds/.

10. Modify ``requirements.txt``, ``Dockerfile`` and the Python code with the proper versions of
    Python dependencies and libraries and push your changes to Github.

    Look at https://github.com/FNNDSC/pl-simplefsapp (a simple **fs** plugin) and https://github.com/FNNDSC/pl-simpledsapp (a simple **ds** plugin)
    for guidance on getting started with your ChRIS plugin!

11. Once you've developed and properly tested your plugin app consult the wiki_ to learn how to register it to ChRIS and the ChRIS store.

.. _wiki: https://github.com/FNNDSC/cookiecutter-chrisapp/wiki




