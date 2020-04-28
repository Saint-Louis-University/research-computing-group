---
date: "2019-01-25"
title: APEX
type: pages
description: The name of our high performance computing cluster is Apex. 
icon: ti-package
---

Please see the <u>[Getting Started](/gettingstarted/)</u> page if you are new to the HPC. This will explain how to connect to the cluster and the applications needed for this. 

Note: Please also see the <u>[Bright Cluster Manager 7.2 Manual](http://support.brightcomputing.com/manuals/7.2/user-manual.pdf)</u> for detailed information on how to use Apex. 


We are in the process of moving resources from Kepler to Apex. Updates on apex include:

&minus;  CentOS 7.2<br>
&minus;  Infiniband connectivity on every nodes.<br>
&minus; Central user portal that shows status of nodes and running jobs.<br>
&minus; Hadoop and other Big Data tools will be available.<br>
&minus; Slurm job scheduler.

After 8-30-16 most new accounts will be created on Apex. 

apex.slu.edu

Most of the support documentation that was written for Kepler is applicable to Apex. The VPN process is different for Apex. If you need to use an application with a graphical user interface, you can do the following.

    ssh -Y username@apex.slu.edu

<u>**Moving files from Kepler to Apex**</u>

Both cluster are connected to the network attached storage volume xfs2. Files can be copied from Kepler to Apex on /xfs2. You will need to make sure file permissions are set correctly so you can access the file on Apex.

<u>**Cluster Documentation**</u>

Below is a link to the Bright Cluster Manager 7.2 user manual. Please review this document for complete information on how to use the cluster.

<u>[Bright Cluster Manager 7.2 User Manual](http://support.brightcomputing.com/manuals/7.2/user-manual.pdf)</u>

<br>

<u>**Storage**</u>

When you log into Apex, you will be in your personal /home directory. Your /home directory is shared and is available on all Apex nodes. This directory is backed up on a nightly basis.


Apex has access to 2 large network attached storage arrays.


    /mnt/xfs has 73 TB of space
    /xfs2 has 117 TB of space

Both of these volumes are available on all of the Apex nodes. The arrays can be used to store large data files that will be used for analysis or job scratch space. <u>**Files are not backed up on this space unless there is a need to do so. If you need files backed up on this space, please contact Eric Kaufmann at kaufmann@slu.edu.**</u>


<u>**Cluster Status**</u> 

**We are in the process of installing ganglia. This is installed on our older cluster <u>[Kepler](http://kepler.slu.edu/)</u>.**

<u>**Software on Apex**</u>

As on Kepler, applications are installed as module files. Please see <u>[Application](../../support/application-installation/)</u>  documentation. You can install applications in your own home directory. If others need access to the application, it will need to be installed in /cm/shares/apps. This is where most applications are installed on the cluster. Applications installed in this directory can be installed via module files.

<u>**Apex VPN**</u>

If you are need to connect to Apex off campus, you will need VPN access and the VPN cilent.
 
 <u>[VPN](../../getting-started/vpn/)</u>


<u>**GUI without VNC**</u>

If you need to use an application with graphical user interface without VNC, you can do the following.

    ssh -Y username@apex.slu.edu

When you open the application on the command line, the window will appear on your desktop.

<u>**Apex VNC Process:**</u>

**Note:**
  
  We are currently looking at a java based VNC viewer. This allows you to complete the SSH tunnel and VNC login in one process. Please download <u>[TightVNC](https://www.tightvnc.com/download.php)</u>. You will need the Java Viewer 
  Version (2.8.3). You will still need to set up a vnc password if this is your first tine using VNC. The steps for this are listed below.


VNC allows you to use a graphical user interface on the cluster. 


See the following [VNC](../../getting-started/vnc/) documentation for basic setup. There are a few additional steps that will need to be completed to set up VNC.

If you want to use VNC, you will first need to do the following.

1.&nbsp;&nbsp;First, you will need to ssh to the server with a ssh client. See the <u>[ssh documentation](../../getting-started/ssh/)</u> for more information.
 
2.&nbsp;&nbsp;At the command prompt type: vncpasswd
<li style="list-style-type:none;PADDING-LEFT:20px;font-size:15px">Note: This command will set the password you will login to for a VNC session. That password is separate form your user password.</li>

3.&nbsp;&nbsp;After you set your password, type: vncserver. That command will set up the 
    vnc session. You will see the following message:

    Starting applications specified in /home/kaufmann/.vnc/xstartu
    Log file is /home/kaufmann/.vnc/kepler:6.log
The port the session was set up in the above example is 5906.



The basic command to set the VNC session up is as follows.

    ssh -L 5906:localhost:5906 username@apex.slu.edu
You will see the following message:

    Starting applications specified in /home/kaufmann/.vnc/xstartup
    Log file is /home/kaufmann/.vnc/kepler:6.log
    
4.&nbsp;&nbsp;You will then need to change the syntax a bit in the VNC client you are using. The syntax is listed below. 

**Note**: You will need to use the specific port number that you were given when the session was set up. The port in the example aboveis 5906. You will only need to use the last number of the port. So, in this example we will use 6.

  Instead of using: vncviewer kepler.slu.edu:6
  
  You will use: vncviewer localhost:6

You can also use TightVNC Viewer which combines the 2 steps into one client. The SSH tunnel session and VNC sessions are launched from a single screen instead of having to use 2 different applications. 

After you have the VNC session set up. You can simply use the tightVNC java client. You will need to download TightVNC Java Viewer(Verison 2.8.3) <u>[TightVNC Viewer download](https://www.tightvnc.com/download.php)</u>.

Java many need to be upgraded on your machine. If you encounter problems, please contact us and we will be happy to help.

After you download and install the viewer you will see the following screen.

<img src="../../../../images/apex.png" style ="height:265px;width:451px;">


This will handle bot the ssh tunnel and the VNC session login. When you hit connect, you will be prompted for your cluster account password. Then you will be prompted for the VNC password that you set up in step 3.

<u>**Using Network Drives**</u>


1.&nbsp;&nbsp;Windows

We are currently looking into accessing a network volume on the cluster from Windows. 

2.&nbsp;&nbsp;&nbsp;&nbsp;Macintosh 

To use a network drive from the cluster as a local volume on a Mac download the following.

https://www.macissues.com/2014/10/13/how-to-mount-a-remote-system-as-a-drive-using-ssh-in-os-x/

If you need to preserve group permissions, use the following syntax.


    sshfs username@apex.slu.edu:/xfs2/waring_lab /mount -ovolname=Mount -o defer_permissions

<u>**Python**</u>

There is currently a module for Python 3.6.1. Packages can be installed in your /home directory with the following syntax. Note: this has been tested with the Python 3.6.1 module file.

    python -m pip install --user scipy

This would would install scipy in your home directory.

<u>**How to use the job scheduler**</u>

Please see our <u>[SLURM](../../slurm/slurm-commands/)</u> page for complete documentation.

<br>
There are 4 queues currently set up on the cluster. The queues are as follows.

defq - This is the default queue which most jobs will be run it.<br> 
hi-men - This is the queue that contains the nodes with the highest memory in the cluster.<br>
med_mem - This is the queue the contains the nodes that have less memory than the high memory nodes,<br>
matlab - This queue contains the nodes that have Matlab installed.<br>

Please read the Bright Cluster manager User manual Chapter 5 for more detailed SLUM information.

<u>[Bright 7.2 User Manual](http://support.brightcomputing.com/manuals/7.2/user-manual.pdf)</u>

Useful SLURM commands:

squeue – lets you see whats in the SLURM queue<br>
squeue -u <username> – as above but for a specific user<br>
scancel <jobid> – cancels a certain job id<br>
scancel -u <username> – cancels all jobs for a certain user<br>

Here is an example to submit a simple job to the SLURM job scheduler. This specific is a simple batch job. 

If you go to /cm/shared/scripts there is a folder called SLURM.

1.&nbsp;&nbsp;Copy slurm-job.sh to your home directory.

Here is a listing of the script contents:

    #!/usr/bin/env bash
    #SBATCH -o slurm.sh.out 
    #SBATCH -p defq
    
    echo "In the directory: `pwd`" 
    echo "As the user: `whoami`" 
    echo “write this is a file" > analysis.output 
    sleep 60

2.&nbsp;&nbsp;Make sure you have the SLURM module loaded by typing module list. You should see the module listed. If not you will have to add it.

3.&nbsp;&nbsp;Go to your /home folder and type the following.

    sbatch slurm-job.sh 
&minus; This command will submit the job script to to the scheduler. You will see the following message.
  
    Submitted batch job 84 
&minus;The submitted job number is 84.

4.&nbsp;&nbsp;To check the status of the job you can use the squeue command.

5.&nbsp;&nbsp;To get the job details type the following.

    scontrol show job 84 - The output of this is listed below. 
    JobId=84 JobName=slurm-job.sh 
    UserId=kaufmann(1003) GroupId=kaufmann(1003)
    Priority=4294901739 Nice=0 Account=(null) QOS=normal 
    JobState=FAILED Reason=NonZeroExitCode Dependency=(null) 
    Requeue=1 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=2:0 
    RunTime=00:00:01 TimeLimit=UNLIMITED TimeMin=N/A 
    SubmitTime=2016-11-21T11:11:32 EligibleTime=2016-11-21T11:11:32 
    StartTime=2016-11-21T11:11:33 EndTime=2016-11-21T11:11:34 
    PreemptTime=None SuspendTime=None SecsPreSuspend=0 
    Partition=defq AllocNode:Sid=apex:23995 
    ReqNodeList=(null) ExcNodeList=(null) 
    NodeList=compute-026 
    BatchHost=compute-026 
    NumNodes=1 NumCPUs=24 CPUs/Task=1 ReqB:S:C:T=0:0:*:* 
    TRES=cpu=24,node=1 
    Socks/Node=* NtasksPerN:B:S:C=0:0:*:* CoreSpec=* 
    MinCPUsNode=1 MinMemoryNode=0 MinTmpDiskNode=0 
    Features=(null) Gres=(null) Reservation=(null) 
    Shared=0 Contiguous=0 Licenses=(null) Network=(null)
    Command=/home/kaufmann/slurm_test/slurm-job.sh 
    WorkDir=/home/kaufmann/slurm_test 
    StdErr=/home/kaufmann/slurm_test/slurm.sh.out 
    StdIn=/dev/null 
    StdOut=/home/kaufmann/slurm_test/slurm.sh.out 
    Power= SICP=0
