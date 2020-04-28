---
date: "2019-01-25"
title: VNC Subpage
type: post
weight: 5
---

VNC allows you to use a graphical user interface on the cluster. 

See the following VNC documentation for basic setup. There are a few additional steps that will need to be completed to set up VNC.

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

Instead of using: vncviewer kepler.slu.edu:6

You will use: vncviewer localhost:6

We are switching to a java based VNC viewer. This allows you to complete the SSH tunnel and VNC login in one process. Please download <u>[TightVNC](https://www.tightvnc.com/download.php)</u>. You will need the Java Viewer Version (2.8.3). You will still need to set up a vnc password if this is your first tine using VNC. This client will allow you to create the ssh tunnel and VNC session in one step. If you need help installing this please contact us and we will be happy to help.

<center><img src="../../../../images/vnc-sub.jpg" style ="height:300px;width:500px;"></center>

This will handle bot the ssh tunnel and the VNC session login. When you hit connect, you will be prompted for your cluster account password. Then you will be prompted for the VNC password that you set up in step 3.