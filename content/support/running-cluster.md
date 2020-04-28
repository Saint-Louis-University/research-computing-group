---
date: "2019-01-25"
title: "Running Jobs on the Cluster"
type: post
---

<u>**Running Applications on Apex**</u>

Most of the jobs on Apex will be run via the scheduler SLURM. The scheduler will take care of most of the logistics of where the job is run etc.

If you are new to SLURM, the [SLURM 101](http://www.brightcomputing.com/blog/bid/174099/slurm-101-basic-slurm-usage-for-linux-clusters) tutorial is a good place to start. This will show you how to write a basic job script and submit it to the scheduler. 
Partitions: 

A partition is the same thing as a job queue on Apex. Currently, we have the following partitions set up.

 1.&nbsp;&nbsp;hi_mem - compute-018-021 in this partition. These nodes have 512GB of RAM.

 2.&nbsp;&nbsp;med_mem - compute-022-025 in this partition. These nodes have 128GB of RAM.

 3.&nbsp;&nbsp;defq  - compute-026-031 in this partition. These nodes have 64GB of RAM.

 4.&nbsp;&nbsp;interactive - compute-032-033 in this partition. These nodes also have 64GB of RAM.<br> &nbsp;&nbsp; This queue is used if you want to log into a node interactively. <br>&nbsp;&nbsp;&nbsp;Note:There is a time limit on this queue of 2 days. This partition is primarily for testing an code etc.

5.&nbsp;&nbsp;matlab - compute-022-023 in this partition. These nodes are configured to run Matlab.

Useful SLURM Commands:

<html>
<head>
<style>
table, th, td{
  border: 1px solid gray;
  border-collapse:collapse;
}
td{
  padding: 2px;
  text-align: left;
  font-size: 15px;
}
th{
  text-align: center;
}
</style>
</head>
<body>
<table>
  <tr>
    <th style="width:90px;">Command</th>
    <th style="width:650px">Description</th>
  </tr>
  <tr>
    <td>sacct</td>
    <td>reports job accounting info about running or completed jobs.</td>
  </tr>
  <tr>
    <td>salloc</td>
    <td>allocates resources for a job in real time.</td>
  </tr>
  <tr>
    <td>sbatch</td>
    <td>submits a job for later execution. script may contain srun command.</td>
  <tr>
    <td>scancel</td>
    <td>cancels a pending or running job.</td>
  </tr>
  <tr>
    <td>sinfo</td>
    <td>reports the state of partitions and nodes managed by SLURM.</td>
  </tr>
  <tr>
    <td>squeuue</td>
    <td>reports state of jobs. jobs are listed in priority order followed by pending jobs in priority order.</td>
  </tr>
    <td>srun</td>
    <td>used to submit jobs for execution in real time. this can be used with the interactive partition.</td>
  </tr>
</table></body>
 
**Note:** You can get more information on specific command syntax be tryping: man command. E.g. man sacct


Basic Job Submission Script:




Command Examples:
 
 *squeue* - this will list all jobs that are currently running or pending on the cluster partitions. Example of output is listed below.

    JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
               404      defq slurm-jo kaufmann PD       0:00      1 (Resources)
               114      defq IVrunner  avicini  R 1-00:49:21      1 compute-033
               115      defq IVrunner  avicini  R 1-00:46:13      1 compute-026

              

 
 Job 114 is running on partion defq, the status is R which means the job is running. Total running time is 49 hours and 21 minutes. It's running on compute-033 only.

*scontrol  show job 114* - This would give the complete details of job 114.

*scontrol hold job 114* - This would hold job 114.

*sbatch job_script.sh* - Submits a job with the job_scipt.sh script. 

*scancel 114* - This will cancel job 114. You can only cancel your own jobs.

Interactive Jobs:

<br>

<br>

<br>

<u>**Running Applications on Kepler**</u>

Small test jobs can be run on the head node. If you are going to run a larger job, this should be run in the job scheduler. If you are still in the testing phase, we ask that you use the interactive queue or std queue. The commands for this are below. There is also a more detailed overview section below.


<u>**Interactive Queue**</u>

There are currently 2 interactive queues set up. 

 1.&nbsp;&nbsp;apprun
  
 2.&nbsp;&nbsp;apprun_mnt_xfs - **This queue is configured for nodes that have access to the infiniband storage space /mnt/xfs. More information is listed here <u>[infiniband](../infiniband/)**</u>.


    qlogin -q apprun

This qlogin command uses the interactive queue. This will allow you to run a job interactively on a node. The *-q apprun* command syntax is used to submit the request to the apprun job queue. A job queue is a group of node on the cluster.



If you would like to run a non-interactive job, please start with the std queue. The basic syntax is listed below. **We ask that you start with the _std_ queue.** 

    qsub -q std script_name 

This command submits a job to the std job queue. The script_name is the name of the script that will be used to run the job. Basic script syntax is listed below. We will have some example scripts posted on the cluster shortly that you can modify.

<div class="alert rounded-0 alert-light">
<font size = 2px;>
#!/bin/bash <br>
#<br>
#$ -cwd - &nbsp;&nbsp;<strong>Note: This tells the job scheduler to execute the job in the current working directory.</strong><br>
#$ -j y    &nbsp;&nbsp;<strong>Note: -j y means to merge the standard error stream into the standard output stream instead of having two separate error and output streams.</strong><br>
#$ -S /bin/bash &nbsp;&nbsp;<strong>Note: This tells the job scheduler to use the bash shell. This is the shell that is used by default on Kepler.</strong><br>
#<br>
date    &nbsp;&nbsp;<strong>  Note: This area of the script is where commands are put to run your application. This example prints the date, sleeps for 10 seconds, then</strong><br>
sleep 10     &nbsp;&nbsp; <strong>prints the date again. This is just used for an example</strong>
<br>

date
</font>
</div>

<u>**Grid Engine Overview**</u>

This is a short overview of the Sun Grid Engine (SGE), which is now run by Oracle. This is a very easy to use, robust batch scheduler that can handle large work loads across entire organizations. You can find more detailed information in the <u>[Beginner's Guide](https://www.oracle.com/technetwork/oem/host-server-mgmt/twp-gridengine-beginner-167116.pdf)</u>. The version of SGE that is installed on the Kepler is 6.2u5p2.

Submitting jobs, controlling jobs, and gathering information can be accomplished with the commands listed below. Or, you can use QMON, the graphical user interface (GUI) tool. Please see the <u>[QMON tutorial](../../qmon-tutorial)</u>.

<u>**Basic Commands**</u><br>
The SGE is very easy to use. The following sections will describe the commands you will need to submit simple jobs to the Grid Engine.<br>
qsub – submit a job to the batch scheduler.<br>
qstat – examine the job que.<br>
qdel - delete a job from the que


<u>**Submitting a job to queue with qsub**</u><br>

The command syntax is as follows:

    qsub [options] [scriptfile | -- [script args]]

The following example submits a script called sge-date.

    $ qsub sge-date

SGE will run the program, and will place two files in your current directory:

    sge-date.e#
    sge-date.0#

where # is the job number assigned by SGE. The sge-date.e# file contains the standard output from the standard error and the sge-date.o# file contains the output from the standard out.

<u>**Job Scripts**</u><br>
The most efficient way to submit a job to the SGE is to use a “job script”. The script allows all options and the program file to be placed in a single file.

<u>**Que Status: qstat**</u><br>
Que status allows for your jobs to be found by issuing a qstat command. The following is an example of using the qstat -u chemlab. This would show all jobs that the user, chemlab, is running.

To look at jobs for all users, you would issue the following command.

    qstat

<u>**Troubleshooting Jobs**</u><br>
There can be several reason a job will not run. The most common reason is due to resource requirements. It is possible that the cluster may be full and you will have to wait for available resources (processors etc.)

It is also possible that your job may have experienced an error in the run script. In this case the job status will be listed as “Eqw”. You can query the job’s status by entering the following:

    qstat -explain c -j _Job-ID_

Where \_Job-ID\_ is the Grid Engine job number.

<u>**Deleting a Job: qdel**</u><br>

Jobs may be deleted by using the qdel command as follows:

    $ qdel job-id

The job-id is the number assigned by SGE when you submit the job using qsub. You cab only delete your own jobs.
