---
title: Support
type: post
---

# Support

<br>

<hr>

If you are new to the cluster, check out our <u>[Getting Started](../gettingstarted/)</u> page, which provides instructions for initially logging into an HPC environment.

If you would like to know more about what resources are available, we would be more than happy to meet with you. Please contact <u><a href="mailto:kaufmann@slu.edu">Eric Kaufmann</a></u> to make an appointment.

There are some nodes that have access to a large high performance storage volume. Please see the <u>[infiniband section](../../support/infiniband/)</u> for more information.

CFD Application Help<br>
If you are using a Parks College CFD application, <u>[cfd-online](https://www.cfd-online.com/)</u> is an excellent resource.

<u>**Major Applications Installed on the Hpc**</u>

**_Note: If you are interested in using any of the listed applications, please contact_**

<u>Abaqus</u> - Parks College, Used for engineering analysis. 

 Note: This documentation is for Apex

 To run an interactive session on Apex, type the following.

    srun --pty --mem 500 -t 0-00:05 /bin/bash 

  This syntax will let you run an application on a node with 500MB of memory for 5 minutes. It would be used if you want to test an application etc.

 To run a quick abaqus job on the interactive queue type the following after you are logged into the node.

    abaqus job=job-id interactive

 To run large jobs you will have to use a script to submit the job to a SLURM. Basic script will be posted shortly.

<br>
<br>
<br>

Gaussin G09 - Chemistry, Used for computational chemistry analysis.

GCC 4.7.1 - Multiple Departments, Compiler

Matlab - Multiple Departments, High-level programming language and interactive environment used for numerical computation, visualization, and programming.

Orca 3.0.2 - Chemistry, Used for computational chemistry analysis

R 3.0, 3.1.2, and 3.2.0 - Multiple Departments, Statistical application

SAS 9.4 - Multiple Departments, Statistical application

SC/Tetra - Dr. McQuelling Parks College , Used for engineering analysis.

Virtualenv 13.1.2 - Multiple Departments, Allows the use of multiple versions of Python programming language.







