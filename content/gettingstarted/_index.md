---
title: Getting Started
type: post
weight: 1
---

# Getting Started

<br>

<hr>

<u>**Accounts**</u>

an account to use the high performance cluster. Saint Louis University faculty and students working with faculty are eligible for accounts. To apply for a new account, please email <u><a href="mailto:kaufmann@slu.edu">Eric Kaufmann</a></u>. Your username will be the same as your SLU email address username. However, you will have a different password. The password will be given to you when your account is created.

<u>**Applications needed to access HPC.**</u>

<u>[SSH](../getting-started/ssh/)</u> - Client for accessing the HPC clusters remotely. Note: This is a command line interface.<br>
<u>[SSH and X11 Forwarding](https://sites.google.com/a/slu.edu/atg-interns-work/charlie-garavaglia/connecting-to-kepler-and-running-matlab)</u> - This will let you run graphical user interface applications via the command line.<br>
<u>[VNC](../getting-started/vnc/)</u> - Client for accessing a graphical interface.<br>
  -&nbsp;We reccomend using TightVNC for ease of access<br>
<u>[FTP](../getting-started/ftp/)</u> - Protocol for copying files over a network.<br>
<u>[VPN](../getting-started/vpn/)</u> - Client for accessing the HPC from off-campus.

\*Only SSH is required for access to the cluster, but the other applications can make usage easier 

<u>**Application Installation**</u>

Applications can be installed in your home directory. Your home directory is stored on a network share. So, that application is able to run on individual nodes. We can also install applications and environment modules for them. This will allow anyone on the cluster to use the application without having to install it. Documentation for using environment modules is below.

<u>**Environment Modules**</u>

We are using Environment Modules Package on <u>[Kepler](http://kepler.slu.edu/)</u>. This will take care of any shell configurations for you. To see what modules are available type module avail at the command line. 

**Note:** 

 **If you use module add, you will loose the module when you log out.** 

 **If you use module initadd, you will have to log back in to use the module. But, then the module will be loaded from now on.**
 

You will see the following message when you login to Kepler:

```
The commands listed below are for modules. This allows you to add paths to installed software to your environment. 

'module avail'            - show available modules
'module add <module>'     - adds a module to your environment for this session
'module initadd <module>' - configure module to be loaded at every login
'module list'             - shows the current modules you have
```

<u>**Node Assignments**</u>

When you login you will see the following message.

Here is an index of what is available.
<html>
<head>
<style>
td,th {
  padding: 1px;
  text-align: left;
  font-size: 13px;
  width: 50%
 }

</style>
</head>
<body>
<table>
<tr>
  <th>research#</th>
  <th>Purpose</th>
</tr>
<tr>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
</tr>
<tr>
  <td>001 - 002 GPU&nbsp;&nbsp;</td>
  <td>RESERVED FOR MATLAB!!!!!!</td>
</tr>
<tr>
  <td>003 - 010</td>
  <td>General Purpose</td>
</tr>
<tr>
  <td>011 - 020</td>
  <td>Dr. McQulling, Parks College</td>
</tr>
<tr>
  <td>021 - 032</td>
  <td>General Use Nodes</td>
</tr>
<tr>
  <td><br></td>
  <td><br></td>
</tr>
<tr>
  <th>c #</th>
  <th>Purpose</th>
</tr>
<tr>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
</tr>
<tr>
  <td>030 - 037</td>
  <td>Dr. Lebeau, Parks</td>
</tr>
<tr>
  <td>c50 - c70</td>
  <td>Dr. Kirkpatrick, Chemistry</td>
</tr>
<tr>
  <td>c79 - c82  </td>
  <td>Dr. Goodson, JCSB</td>
</tr>

<tr>
  <td><br></td>
  <td><br></td>
</tr>
<tr>
  <th>p #</th>
  <th>Purpose</th>
</tr>
<tr>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
  <th>&minus;&minus;&minus;&minus;&minus;&minus;&minus;</th>
</tr>
<tr>
  <td>phy001 - 008</td>
  <td>Dr. Solenov, Physics</td>
</tr>
</table>
</body>



Nodes that are listed under a particular name are owned by that faculty member. We ask that you use the job queue if you want to run applications on nodes. That information is listed in the next section. The job queue will assign a node for you.


<u>**Running Applications on the Cluster**</u>

Small test jobs can be run on the head node. If you are going to run a larger job, this should be run in the job scheduler. If you are still in the testing phase, we ask that you use the interactive queue or std queue. The commands for this are below. There is also a more detailed overview section below.


<u>**Interactive Queue**</u>

    qlogin -q apprun

This *qlogin* command uses the interactive queue. This will allow you to run a job interactively on a node. The *-q apprun* command syntax is used to submit the request to the apprun job queue. A job queue is a group of node on the cluster.



If you would like to run a non-interactive job, please start with the *std queue*. The basic syntax is listed below. **We ask that you start with the _std_ queue.** 

    qsub -q std script_name 

This command submits a job to the std job queue. The script_name is the name of the script that will be used to run the job. Basic script syntax is listed below. We will have some example scripts posted on the cluster shortly that you can modify.

```
#!/bin/bash
#
#$ -cwd -  Note: This tells the job scheduler to execute the job in the current working directory.
#$ -j y    Note: -j y means to merge the standard error stream into the standard output stream instead of having two separate error and output streams.
#$ -S /bin/bash Note: This tells the job scheduler to use the bash shell. This is the shell that is used by default on Kepler.
#
date       Note: This area of the script is where commands are put to run your application. This example prints the date, sleeps for 10 seconds, then
sleep 10         prints the date again. This is just used for an example
date
```
