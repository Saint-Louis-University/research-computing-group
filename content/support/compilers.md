---
date: "2019-01-25"
title: Compilers
type: post
---

We have several compiler environments on the cluster. Many are interdependent.

#### GCC
The preferred and default compiler on the cluster is GCC, the GNU Compiler Chain.

#### The MPI compiler chain
A wrapper around GCC for compiling programs for use in an MPI environment.

Here are some example commands:<br>
Say there’s a file in a folder named chug.c. From that folder in the command line try the command
‘make chug’<br>
This will compile your program into a binary named ‘chug’

To use the compilers directly you would invoke them based on language and use the -o flag to choose the output file’s name.

<html>
<head>
<style>
table, th {
border: 1px solid white;
border-collapse: collapse;
}
th, td{
  padding: 5px;
  text-aligh: left;
  vertical-align: top;
  font-size: 14px;
}
tr:nth-child(even){
  background-color: #f2f7ff;
}
tr:nth-child(3){
  background-color: #fff;
}
tr:nth-child(5){
  background-color: #eee;
}
th{
  background-color: #F1FAF6
}
</style>
</head>
<body>
<table>
  <tr>
    <th style="width:110px;"> </th>
    <th style="width:110px;">GCC</th>
    <th style="width:110px;">MPI</th>
    <th style="width:110px;">SUN</th>
    <th style="width:110px;"> </th>
  <tr>
    <td>C</td>
    <td>gcc mycode.c<br>-o mybinary</td>
    <td>mpicc<br>mycode.c -o<br>mybinary</td>
    <td>suncc<br>mycode.c -o<br>mybinary</td>
    <td><br></td>
  <tr>
    <td>C++</td>
    <td>g++ mycode.c<br>-o mybinary</td>
    <td>mpic++<br>mycode.c-o<br>mybinary</td>
    <td>sunCC<br>mycode.c -o<br>mybinary</td>
    <td> </td>
  <tr>
    <td>FORTRAN</td>
    <td>gfortran<br>mycode.c -o<br>mybinary></td>
    <td>mpifxx<br>mycode.c -o<br>mybinary</td>
    <td>sunf*</td>
    <td>where * is the version of fortran</td>
  <tr>
    <td>assembler</td>
    <td>as</td>
    <td> </td>
    <td>sunas</td>
    <td></td>
</table>
</body>

The Oracle Solaris IDE is available on certain nodes of the cluster upon request. Solaris Studio is an IDE that allows you to write, compile, and debug code all in one window.