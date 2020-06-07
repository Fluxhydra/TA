# Learning Summary
This section was made in order to record my learning activities so that I can traceback whenever I get stuck on a wall along the way. <br>

Processor: Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz (8 CPUs), ~2.8GHz

Memory: 8192MB RAM

Ubuntu Version: 18.04

NS2 Version: 2.35

Contents:
1. NS2 Installation
2. Introduction to NS2
3. Wired Network Design

Hope everything is going okie. Wish me luck!

## [1] NS2 Installation

Download ns-allinone-2.35.tar.gz [here](https://sourceforge.net/projects/nsnam/files/allinone/ns-allinone-2.35/ns-allinone-2.35.tar.gz/download)

Unpack files in main folder
```bash
$] tar zxvf ns-allinone-2.35.tar.gz
$] cd ns-allinone-2.35
```
Install gcc and g++
```bash
$] sudo apt install gcc-4.8 g++-4.8
```
Fix some codes before installing NS2. In file Makefile.in, look for lines containing CC and CPP then replace these values with gcc-4.8 and g++-4.8 respectively. For file ls.h at line 137, change erase to this->erase.
```bash
$] sudo apt update
$] sudo apt install build-essential autoconf automake libxmu-dev

$] cd ns-allinone-2.35/ns-2.35
$] gedit Makefile.in
$] gedit linkstate/ls.h

$] cd ..
$] ./install
```
Fix environment PATH and LD_LIBRARY_PATH by copying the values given by terminal once the NS2 installation has been finished.
```bash
$] gedit /home/hydra/.bashrc
$] source /home/hydra/.bashrc
```
![Install NS2](https://github.com/Fluxhydra/TA/blob/master/Screenshots/1051807062020%20NS2%20Installation.PNG)

## [2] Introduction to NS2

Why use Linux?
1. Support has been stopped beyond NS-2.27 in windows
2. Tedious package configuration
3. Risky and lots of difficulties in tuning cygwin and mingw (windows8x architecture)

Requirements!
1. Available distributions: Ubuntu, Fedora, Linux Mint, RHEL/CentOS etc
2. Know basic commands: ls, chmod, tar, rpm, make, gedit, vi, pwd, passwd, echo, cd etc
3. Know directory structure and shell prompt
4. Understand path variables settings, packages and dependency installations

Network Simulation
1. Event Driven: Every event provide a reference to the next event
2. NS2 is a discrete event simulator
3. NS2 provides support for TCP simulation, routing, huge number of protocols and additions of new entities (agent, packet, application etc)
4. Users of ns are requested to verify that the results are not invalidated by bugs

NS2 Architecture
1. Event driven simulator
2. Consists of C++ (internally), OTCL (user interface) and TclCL (interface between C++ and OTCL)

Try simple simulations:
```bash
$] cd ns-allinone-2.35/ns-2.35/tcl/ex
$] ns wireless-mitf.tcl
$] nam wireless_mitf.nam

$] ns simple.tcl
```

## [3] Wired Network Design
Sample Network Design. There's a wired network with 6 nodes as shown below:
![Wired Network](https://github.com/Fluxhydra/TA/blob/master/Screenshots/2092307062020%20Wired%20Network.PNG)

Nodes: 0, 1, 2, 3, 4, 5

Links: 
1. 0-1 [5,2]
2. 1-2 [10,5]
3. 1-4 [3,10]
4. 3-4 [100,2]
5. 4-5 [4,10]

<bandwidth in mbps, delay in ms>

Duplex links are used which enable data transfer from node A to B and vice versa

[S1,S2,D1,D2] => [0,2,3,5]

Data transfer:
1. From S1 to D1
2. From S2 to D2

S1 uses UDP agent with CBR (constant bit rate), D1 uses NULL agent

S2 uses TCP agent with FTP (which has unstable bit rate), D2 uses sink agent

**Credits: TS Pradeep Kumar**
