---
date: "2019-01-25"
title: VNC
type: pages
weight: 4
description: VNC allows you to use the cluster with a graphical user interface
icon: ti-package
---

VNC allows you to use the cluster with a graphical user interface. Detailed information can be found on <u>[Wikipedia VNC page](https://en.wikipedia.org/wiki/Virtual_Network_Computing)</u>.

Before you can use VNC you will need to set up a VNC session on the head node. All VNC sessions also require a ssh tunnel. This is for security purposes. The TightVNC Client will create the tunnel and VNC login in one step. Instructions for this are below.

If you want to use VNC, you will first need to do the following.

1.&nbsp;&nbsp;First, you will need to ssh to the server with a ssh client. See the <u>[ssh documentation](../ssh/)</u> for more information.
 
2.&nbsp;&nbsp;At the command prompt type: vncpasswd<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Note: This command will set the password you will login to for a VNC session. That password is separate form your user password.

3.&nbsp;&nbsp;After you set your password, type: vncserver. That command will set up the vnc session. You will see the following message:

    Starting applications specified in /home/kaufmann/.vnc/xstartup
    Log file is /home/kaufmann/.vnc/kepler:6.log
     
The port the session was set up in the above example is 5906.

The basic command to set the VNC session up is as follows.

    ssh -L 5906:localhost:5906 username@apex.slu.edu

You will see the following message:

    Starting applications specified in /home/kaufmann/.vnc/xstartup
    Log file is /home/kaufmann/.vnc/kepler:6.log

4.&nbsp;&nbsp;You will then need to change the syntax a bit in the VNC client you are using.

**Note:** You will need to use the specific port number that you were given when the session was set up. The port in the example above is 5906. You will only need to use the last number of the port. So, in this example we will use 6.

&nbsp;&nbsp;&nbsp;&nbsp;Instead of using: vncviewer kepler.slu.edu:6

&nbsp;&nbsp;&nbsp;&nbsp;You will use: vncviewer localhost:6

After you have the VNC session set up. You can simply use the tightVNC java client. You will need to download TightVNC Java Viewer(Verison 2.8.3) <u>[TightVNC Viewer download](https://www.tightvnc.com/download.php).</u>

Java many need to be upgraded on your machine. If you encounter problems, please contact us and we will be happy to help.

After you download and install the viewer you will see the following screen.

<center><img src="../../../../images/vnc-1.png" style ="height:300px;width:500px;"></center>

This will handle bot the ssh tunnel and the VNC session login. When you hit connect, you will be prompted for your cluster account password. Then you will be prompted for the VNC password that you set up in step 3.

<hr>

subpages(1): <u>[VNC](../vnc_subpage/)</u>
