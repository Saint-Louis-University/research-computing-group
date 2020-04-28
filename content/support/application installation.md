---
date: "2019-01-25"
title: Application Installation
type: post
---

#### Application Installation

Applications can be installed in your home directory. Your home directory is stored on a network share. So, that application is able to run on individual nodes. We can also install applications and environment modules for them. This will allow anyone on the cluster to use the application without having to install it. Documentation for using environment modules is below.

#### Environment Modules

We are using Environment Modules Package on <u>[Kepler](http://kepler.slu.edu/)</u>. This will take care of any shell configurations for you. To see what modules are available type module avail at the command line. 

**Note:** 

 **If you use module add, you will loose the module when you log out.**

 **If you use module initadd, you will have to log back in to use the module. But, then the module will be loaded from now on.**
 

You will see the following message when you login to Kepler:

    The commands listed below are for modules. This allows you to add paths to installed software to your environment. 
    
    'module avail'            - show available modules
    'module add <module>'     - adds a module to your environment for this session
    'module initadd <module>' - configure module to be loaded at every login
    'module list'             - shows the current modules you have


