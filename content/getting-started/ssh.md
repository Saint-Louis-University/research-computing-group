---
date: "2019-01-25"
title: SSH
type: pages
weight: 2
icon: ti-credit-card
description: SSH is a secure protocol that allows you to connect to a remote system
---

SSH is a secure protocol that allows you to connect to a remote system.  In order to access a HPC cluster from off-campus, you will need Billiken Secure Connect VPN account. More information can be found here <u>[BIlliken Secure Connect (VPN)](https://www.slu.edu/its/index.php)</u>.

**Note:** <br>
There is also a graphical user interface that can be used with the cluster. See the VNC section for more information.

**Common Linux Commands**<br>
Once you have logged into an HPC, you are communicating to a completely text-based Linux environment. To navigate the environment, you will need to enter specific commands. For example, cd Documents will change your current working directory to "Documents". <u>[This page](https://www.dummies.com/computers/operating-systems/linux/common-linux-commands/)</u> has a list of some common, useful Linux commands (many of which will also work on Mac and Putty).

<hr>

### <center><u>Windows</u></center>

<center><img src="../../images/windows_logo.jpg" style ="height:200px;width:300px;"></center>



<li style="PADDING-LEFT:20px">Download putty.exe <u>[(Here)](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)</u>. </li>
<li style="list-style-type:circle;PADDING-LEFT:60px">Note that this does not "install" like we are used to doing in Windows. By clicking on the downloaded executable it will start to run.</li>
 
<li style="PADDING-LEFT:20px">Download and install xming-mesa <u>[(Here)](https://sourceforge.net/projects/xming/files/)</u>.</li>
<li style="list-style-type:circle;PADDING-LEFT:60px">Be sure to get the -mesa version, as this is the version that is able to handle the 3D graphics of Gaussview.</li>

<li style="PADDING-LEFT:20px">Follow the directions listed on this site <u>[(Here)](https://sites.google.com/a/slu.edu/atg-interns-work/charlie-garavaglia/connecting-to-kepler-and-running-matlab)</u>.</li>

<hr>
### <center><u>Macintosh</u></center>

<center><img src="../../images/mac_logo.jpg" style ="height:200px;width:300px;"></center>

SSH is pre-installed on OS X and can be accessed using the Terminal application.  Terminal is located in Applications/Utilities.  After opening Terminal, type the following:

    ssh username@kepler.slu.edu
After successfully entering your password, you will see this prompt:

    [username@kepler.slu.edu ~]$
You are now logged into kepler.slu.edu.  To log out, simply type _exit_ at the prompt.

<hr>

### <center><u>Linux</u></center>

<center><img src="../../images/linux_logo.jpg" style ="height:200px;width:300px;"></center>


At the command prompt, type the following:
   
    ssh -X username@kepler.slu.edu
After successfully entering your password, you will see this prompt:
  
    [username@kepler.slu.edu ~]$
You are now logged into kepler.slu.edu.  To log out, simply type _exit_ at the prompt.

