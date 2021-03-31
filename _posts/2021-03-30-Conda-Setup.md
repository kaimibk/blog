---
layout: post
title:  "Getting Started with Anaconda"
excerpt: >- 
    A tutorial on installing and using the Anaconda python platform
tag: 
- python
- tutorial
- anaconda
toc: True
---

## What is Anaconda?

Anaconda is a great platform for installing Python libraries and environment management. Overall, if you develope in Python, Anaconda will make your life so much easier.

When it comes to installation, you have two options:
- The full version of anaconda, which includes a bunch of useful libraries and tools for Python development. However, it is worth noting that the install is quite large&mdash;approximately 400 MB&mdash;and includes software you may never use.
- A barebones version called Miniconda, which includes the minimal installer for Conda. However, you will have to install all libraries/tools yourself&mdash;which can be a good or bad thing, depending on your experience level.

For this tutorial, I will be focusing on **miniconda**, which is the version I work with almost exclusively.

## Installing Miniconda

Depending on your operating system (MacOSX/Linux vs Windows), the process may be different. See [HERE](https://docs.conda.io/en/latest/miniconda.html) to see the different options for installation.

On Mac and Linux, I suggest the following procedure:
1. Download the installer from the [docs](https://docs.conda.io/en/latest/miniconda.html#macosx-installers). You have two choices, either a `bash` or `pkg` file&mdash;I generally prefer to use the `bash` option.
2. Open up a copy of your terminal, and execute `bash [THE PATH TO THE MINICONDA FILE]`.
3. Follow the installation instructions that appear in the terminal. If you are unsure about any setting, accept the defaults. You can change them later.
4. To make the changes take effect, close and then re-open your terminal window.
5. Test your installation. In your terminal window, or Anaconda Prompt on Windows, run the command `conda list`. A list of installed packages appears if it has been installed correctly.

## Creating Conda Environments

The key to developing good, reproducible code is to work in isolated environment. In these environments, you can control which packages are installed, their dependencies, and even the version of Python. With Anaconda, this process in really easy!

1. Open a terminal or Anaconda prompt
2. To create a new environment `conda create --name [THE NAME YOU WANT TO CALL IT] python=[THE VERSION YOU WANT TO INSTALL]`. For example, `conda create --name MyEnv python=3.6`.
3. When conda prompts you to proceed, `proceed ([y]/n)?`, type `y`.
4. Conda will then install your new python environment with the version specified.
5. Note, there are a lot of other options you can specifiy. We will go through some options in following sections.

**It is generally good practice to make a separate (new) conda environment for each project.** However, I personally have a few general environments for quick testing. For example, I have general environments for ML, visualization, web development, etc. that I can pop into for quick development.

### Specifying a Location for the Environment

Note, instead of creating a globally accessible environment, sometimes it is valuable to install the environment directly to your project folder. You can do this by defining the `--prefix` flag. For example, `conda create --prefix ./envs python=3.7` will create your environment in a folder called `envs` relative to where you executed the command.

To activate this environment, you can call it by name, `conda activate ./envs`. It should behave just like a standard conda environment.

## Using Your New Fancy Conda Environment

Once your environment is installed, you can now work on installing all the libraries you need for your project.

1. Open a terminal or Anaconda prompt
2. Execute `conda activate [YOUR ENVIRONMENT NAME]`. In our example, `conda activate MyEnv`.
3. Assuming everything is installed correctly, you will see your environment name appear beside you username in the terminal.

If you would like to install a library, you need to be aware of which *channel* the library is located in. For most popular libraries, you don't have to specify the channel, because Anaconda has included them in the default channel.

To install a library, you can execute `conda install [THE PACKAGE NAME]` in the terminal. As an example, we can execute `conda install numpy` to install the latest version of the popular Numpy library that is compatible with your evironment. Note, it is always a good idea to verify which environment you are in before installation&mdash;so you don't accidentally mess up a separate environment...and yes, I speak from experience.

If you would like more control over the installation process, you can also specify the library version. For example, `conda install scipy=0.15.0` to install a specific version of the Scipy library.


If you are ever stuck on how to install your library, if you google "conda install [this library]" you will see which channel they are located in, ie `conda-forge`.

## Share Your Conda Environment

If you would like to share your conda environment with your colaborators, or have reproducible code in general, you can export instructions for recreating your development environment.

Assuming you activated your environment, you can execute `conda env export > environment.yml`. This will export instructions for building your environment into a `environment.yml` file.

To recreate an environment from this file, all you need to do is execute `conda env create -f environment.yml`.

## More Resources

- For a quick reference guide to other conda functionality, see [HERE](https://conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf).
- For the latest guide on managing your conda environment, see [HERE](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#restoring-an-environment).