---
date: "2019-01-25"
title: "SLURM Commands"
type: post
---

SLURM is the job scheduler that we are using on Apex. This allows jobs to be run on a node. How the jobs starts, runs, and completes is normally dictated by a script.<br>
More detailed information and tutorials can be found at <u>[SLURM information page.](https://slurm.schedmd.com/)</u> Please also read the F.A.Q below. before

**Note** : We have listed the most commonly used commands below. Futher

#### Useful SLURM Commands

Here is a list of the most common SLURM commands.

**General Commands**

Get SLURM documentation:

man sbatch<br>
man squeue<br>
man scancel<br>

**Get Information on Jobs**

List Jobs for current user:

    squeue -u <username>

List all running jobs for a user:
 
    squeue -u <username> -t RUNNING

List all pending jobs for a user:
 
    squeue - u <username> -t PENDING

List all current jobs in the defq partition for a user:

    squeue -u <username> -p defq

List detailed status for a job. This can be helpful for troubleshooting.

    scontrol show jobid -dd <jobid>

List statistics on completed job by jobID:

    sacct -j <jobid> --format=JobID,JobName,MaxRSS,Elapsed

To view the same information for all jobs of a user:
 
    sacct -u <username> --format=JobID,JobName,MaxRSS,Elapsed

 **Controlling Jobs**

Cancel a job:

    scancel <jobid>
To cancel a job for a user:

    scancel -u <username>

Cancel all pending jobs for a user:
 
    scancel -t Pending -u <username>

Cancel one or more jobs by name:

    scancel --name myJonName

Pause a job:

    scontrol hold <jobid>

To resume a job:

    scontrol resume <jobid>

To requeue (cancel and rerun) a particular job:

    scontrol require <jobid>



#### Getting Information

There are many commands that you can use to interact with SLURM. The sinfo command gives you an overview of the resources offered by the cluster, while  squeue shows which jobs have resources allocated to them. Examples of both command are listed below.

By default, sinfo lists the partitions that are available. A **partition** is a set of compute **compute nodes** (machines dedicated to running jobs) grouped logically. In the example below, node are grouped by machine, memory, and matlab which is a application. The **timelimit** is the maximum time that a job can run on a node. The default partition is, **defq**, is marked by an \*. Jobs are running on all the nodes on the example. They have a state of **alloc** which means that they are currently allocated.

    sinfo
    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    defq*        up   infinite     10  alloc compute-[018-021,026-031]
    hi_mem       up   infinite      4  alloc compute-[018-021]
    matlab       up   infinite      3  alloc compute-[022-024]
    med_mem      up   infinite      4  alloc compute-[022-025]



*Squeue* shows how many jobs are currently running on the cluster.


    squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             20488 hi_mem,me executeA nkullman PD       0:00      1 (Resources)
             20489 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20490 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20491 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20492 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20493 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20494 hi_mem,me executeA nkullman PD       0:00      1 (Priority)
             20495 hi_mem,me executeA nkullman PD       0:00      1 (Priority)

There are many switches you can use to filter the output by user (&minus;&minus;user), by partition (&minus;&minus;partition), by state (&minus;&minus;state), etc.

**Partitions**

A partition is a group of machines on the cluster that jobs are run in. If you don't request a particular partition, your job will ruin on the default, defq, partition.Here are the current partitions on Apex.

1.&nbsp;&nbsp;defq - This is the default queue which most jobs will be run it.<br> 
2.&nbsp;&nbsp;hi-men - This is the queue that contains the nodes with the highest memory in the cluster.<br>
3.&nbsp;&nbsp;med_mem - This is the queue the contains the nodes that have less memory than the high memory nodes,<br>
4.&nbsp;&nbsp;matlab - This queue contains the nodes that have Matlab installed. These nodes can run Matlab Distributed Computing Server.

**Modifying a submitted job**

A job can be modified after its submitted. This can be done with the scontrol command.

If you wanted to change the partition a job is running in, you could do the following.

    scontrol update jobid=$i partition=hi_mem

Note: That $i is the actual job number. The partition the job will run in will change to hi_mem. To see more command syntax simply type scontrol help.

#### Running Jobs

Normally you will use scripts to submit a job to the scheduler. We suggest that you look at the <u>[SLRUM 101](http://www.brightcomputing.com/blog/bid/174099/slurm-101-basic-slurm-usage-for-linux-clusters)</u> page to get a basic idea. There are also script examples below. You can also use SLURM to run an interactive job. That will allow you to login to a node to run an application or test code. Example syntax is listed below.

**Interactive Jobs**

    srun -p matlab --pty -t 1:00 /bin/bash 

This command will find a node in the matlab partition and will allow you to stay logged into the node for one minute. Time format in SLUM is HH:MM:SS. You can see the syntax for srun by typing man srun at the command prompt.

Here are the current partitions on Apex.

There are 4 queues currently set up on the cluster. The queues are as follows.

1.&nbsp;&nbsp;defq - This is the default queue which most jobs will be run it.<br>
2.&nbsp;&nbsp;hi-men - This is the queue that contains the nodes with the highest memory in the cluster.<br>
3.&nbsp;&nbsp;med_mem - This is the queue the contains the nodes that have less memory than the high memory nodes,<br>
4.&nbsp;&nbsp;matlab - This queue contains the nodes that have Matlab installed. These nodes can run Matlab Distributed Computing Server.

**Job Scripts**

A job script consist of two parts: **resource requests** and **job steps**. Resource requirements consist of number of CPU's, computing expected duration, amounts of RAM or disk space, etc. Job steps describe **tasks** that must be done, and/or software that needs to be run.

A **submission script** is a **shell script**, e.g BASH script whose comments are prefixed with SBATCH. These are SLURM parameters describing resource requests and other submission options. The script it's self is a job step. Other job steps are created with the **srun** command.

The example below is a script called submit.sh.

    #!/bin/bash
    #
    #SBATCH --job-name=test
    #SBATCH --output=res.text
    #
    #SBATCH --ntasks=1
    #SBATCH --time=10:00

    srun hostname
    run sleep 60

This script requests one **CPU** for 10 minutes, along with 100 MB of RAM, and it will run in the default, defq, queue. When started, the job will run the first job step srun hostname. This will launch a unix command hostname on the node that requested CPU was allocated. Then a second step will start the sleep command. After you write the script, you will need to **submit** the job with the **batch** command. When the job is finished, it will return to the **shell prompt $**. 

    $ sbatch submit.sh
    sbatch: Submitted batch job to 2133

The job then enters the queue in the *PENDING* state. Once resources become available and the job has highest priority, an **allocation** is created for it and it goes to the RUNNING state. If the job completes correctly, it goes to the *COMPLETED* state, otherwise, it is set to the *FAILED* state. 

Upon compeltion, the output file contains the result of the commands run in the script file. In the above example, you can see it with **cat res.text.**

Note that you can create an **interactive job** with the **salloc** command or by issuing a **srun** command directly.

<br>

**Parallel Jobs**

But, still, the real question is: How do you create a parallel job?

There are several ways a **parallel job**, one whose tasks are run simultaneously, can be created:

<font size = 3>
<li style="PADDING-LEFT:20px">by running a multi-process program ([SPMD](https://en.wikipedia.org/wiki/SPMD) paradigm, e.g. with [MPI](https://en.wikipedia.org/wiki/Message_Passing_Interface))</li>
<li style="PADDING-LEFT:20px">by running a multithreaded program (shared memory paradigm, e.g. with [OpenMP](https://en.wikipedia.org/wiki/OpenMP) or [pthreads](https://en.wikipedia.org/wiki/POSIX_Threads))</li>
<li style="PADDING-LEFT:20px">by running several instances of a single-threaded program (so-called *embarrassingly parallel* paradigm)</li>
<li style="PADDING-LEFT:20px">by running one master program controling several slave programs (*master/slave* paradigm)</li>
</font>

In the Slurm context, a task is to be understood as a **process**. So a multi-process program is made of several tasks. By contrast, a multithreaded program is composed of only one task, which uses several CPUs. 

Tasks are requested/created with the <span style="background-color:#ffffff;font-family:Comic Sans MS">&minus;&minus;ntasks</span> option, while CPUs, for the multithreaded programs, are requested with the <span style="background-color:#ffffff;font-family:Comic Sans MS">&minus;&minus;cpus-per-task</span> option. Tasks cannot be split across several compute nodes, so requesting several CPUs with the <span style="background-color:#ffffff;font-family:Comic Sans MS">&minus;&minus;cpus-per-task</span> option will ensure all CPUs are allocated on the same compute node. By contrast, requesting the same amount of CPUs with the <span style="background-color:#ffffff;font-family:Comic Sans MS">&minus;&minus;ntasks</span> option may lead to several CPUs being allocated on several, distinct compute nodes.
