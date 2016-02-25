---
layout: post
title: Implementation of matrix multiplication fox algorithm using MPI
date: 2010-05-05 00:00:00.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- mpi
- parallel
---

Software efficiency always improves a lot by parallelizing. Here is an implementation of fox algorithm, which is one of the algorithms calculating matrix multiplication, using MPI.

> [Message Passing Interface](http://en.wikipedia.org/wiki/Message_Passing_Interface "MPI") is a specification for an API that allows many computers to communicate with one another.

MPI is an parallel library to help programming. Its main idea is transferring messages between processes, which are paralleling running in different cores or even CPUs. About fox algorithm, I recommend everyone read this [pdf file](http://facultyfp.salisbury.edu/taanastasio/COSC490/Fall03/Lectures/FoxMM/example.pdf "fox algorithm").
