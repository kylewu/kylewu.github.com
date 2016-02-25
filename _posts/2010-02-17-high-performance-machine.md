---
layout: post
title: High performance machine
date: 2010-02-17 00:00:00.000000000 +01:00
published: true
categories:
- 编程技术
tags:
- linux
- os
- uppsala
---

This is my first time using high performance machine. Although the machine is only for student, and of course, it is not good as those pro machines, it is still a good experience for me. ssh remote machin, returns:

    ## Last login: Wed Feb 17 15:02:15 2010 from nl103-144-35.student.uu.se

    Interactive cluster at Uppmax, Uppsala Universitet
    Access node; os1

    * * *

    **Hardware:
    IBM X3455 dual Opteron 2220SE, 2.8GHz nodes. 4*10=40 cores
    8GB RAM, Infiniband and Gigabit interconnect**
    Infiniband is not available for MPI programming due to system problems\n Software:
    Scientific Linux SL release 5.2, kernel 2.6.18-92.1.18.el5
    SGE version 6.2, Grid Engine queue system
    "man sge_intro" for an overview.
    GCC version 4.3 c,c++,fortran and java
    module load gcc
    PGI version 7.2 & 8.0, 64 bit compilers (C,C++,F77,F95,HPF)
    module load pgi
    Intel version 10.1 & 11.1, 64 bit compilers (C,C++,Fortran)
    module load intel
    MPI, OpenMPI libraries, default 1.2.9, 1.3 available
    module load pgi openmpi
    module load gcc openmpi
    mpicc or mpif90 to compile
    mpirun to execute.
    qsub -pe dmp8 16, to submit a 16 slot mpi job
    openMP is available in pgi, intel and gcc
    QUEUES and PEs:
    os: 160 slots main queue (overbooked)
    -pe dmp NN, distributed on nodes, 16 slots per node (4 cores)
    -pe smp NN, shared memory, 1 single node for up to 16 threads (4 cores)
    User Limits:
    The login nodes are intended for short test runs only, max cputime is 30min
    INTERACTIVE:
    Use qsh to request a interactive job and recive a xterm.
    e.g. qsh -l h_rt=01:00:20
    **NB qlogin dont work at the moment use qsh**
    (Use qlogin to execute an interactive session without starting a xterm. )
    NB X-forwarding is working!
    (If you have logged in with "ssh -X os.uppmax.uu.se" !!!)
    Dont forget to request h_rt

    * * *

    News:
    2009-11-20   os6 restarted due to system problems
    2009-10-7/8  Service stop
    New file server "bubo" introduced for all uppmax storage.
    Your home directory is now in /bubo/home/h?/user.
    Refer to this using "$HOME" in your programs.
    To ease the transition we have defined symbolic links so that the old
    directory names are usable for a short time.
    2009-07-07   Compilers: PGI is updated to 9.0, default is kept as 8.0
    If you want the latest version use "module load pgi/9.0"
    Intel is updated to 11.1 (build 038), 11.0 (build 084) is kept as default
    If you want the latest version use "module load intel/11.1"
    2009-03-17      Infiniband removed from openmpi due to stability problems\n 2008-11-28      OS-kluster is reinstalled with SL 5.2
    R is now a module to run R please load the module first
    "module load R"
    Sun Grid Engine updated to 6.2
    I use bold font to indicate hardware.
