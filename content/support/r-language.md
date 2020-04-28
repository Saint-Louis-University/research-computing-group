---
date: "2019-01-25"
title: "R Language"
type: post
---

We currently have modules for R 3.0.0, R 3.1.2, and R 3.2.0

<u>[Installing Modules](../application-installation/)</u>

<u>Starting command line R</u>

Just type R at the command prompt.

<u>Common Commands</u>

<html>
<body>
<table style="font-size:15px">
  <tr>
   <td width = "100">library()</td>
   <td>- This will show what libraries are currently installed on kepler</td>
  </tr>
  <tr>
    <td>.libPaths()</td>
    <td>- This shows you the paths to the installed libraries</td>
  </tr>
  <tr>
    <td>q()</td>
    <td>- Quits the current R sesison.</td>
  </tr>
</table>
</body>
</html>


<u>Parallel R</u>

We are currently working on expanding our parallel support.


<u>Visualizing Data</u>

<u>[R Data Visualization Tutorial](https://www.computerworld.com/article/2497304/business-intelligence/business-intelligence-beginner-s-guide-to-r-painless-data-visualization.html)</u>

<u>[Tips on speeding up R code](https://www.r-bloggers.com/faster-higher-stonger-a-guide-to-speeding-up-r-code-for-busy-people/)</u>

<u>Installing R Packages</u>

Finding Packages:

Navigate to the cran library to see the list of packages
<br>
http://cran.us.r-project.org/
<br>
Click on the ‘Packages’ link
<br>
Click on ‘Table of available packages, sorted by name’ link

Installing Package Method 1:

    [username@kepler ~]$ R
    > install.packages('package-name',repos='http://cran.us.r-project.org')

Installing Package Method 2:
<br>
Click on ‘Table of available packages, sorted by name’ link
<br>
Click on the Package
<br>
Find the Label: ‘Package Source’
<br>
Right click on the ‘package’.tar.gz and click ‘copy link address’
<br>
Paste link address into kepler after ‘wget’

    [username@kepler ~]$ wget http://cran.r-project.org/src/contrib/’package’.tar.gz
    [username@kepler ~]$ R CMD INSTALL ‘package’.tar.gz