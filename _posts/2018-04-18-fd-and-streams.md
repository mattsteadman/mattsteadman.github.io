---
layout: post
title:  "File Descriptors and Streams"
date:   2018-04-18
categories: [operating-systems]
permalink: fd-and-streams
description: "What's the difference between file descriptors and streams?"
---
Unix has two similar concepts for reading and writing file-like objects. The first, file descriptors, is used by lower-level functions like `read(2)`. The second, streams, is used by higher-level functions like `fprintf(3)`. So what are the similarities and differences between them?

- File descriptors are represented by objects of type `int`. Streams are represented by objects of type `FILE *`.

- Streams *themselves* use file descriptors to access files. Streams are a layer *on top* of file descriptors to take care of some of the details of the most common kinds of I/O.

- Both can represent connections to files, devices (e.g terminals), and pipes/sockets (for IPC).

- Why use streams? Because using streams gives you access to a more powerful set of functions. Namely, formatted I/O functions like `printf` and `scanf`. These functions have provide two main benefits:
  - They save you from having to write ad-hoc parsers for reading and writing strings dynamically
  - They save you system calls by using buffered I/O

- Why use file descriptors? They offer more control what and when you read and write:
  - They allow you to do control operations that are specific to particular devices
  - They let you use special modes of I/O, like nonblocking I/O. By contrast, the only control that streams give you is the choice of styles of buffering (unbuffered, line buffered, fully buffered).

- You can always change your mind:
  - You can request that a streams give you the underlying file descriptor for low-level operations
  - You can create a stream from an existing a file descriptor

- In general, try to use streams unless you have a reason to do otherwise

- File descriptors are a POSIX feature, whereas streams are an ISO C feature. Therefore, streams are more portable than file descriptors. Non-POSIX systems are free to implement streams using something besides file descriptors under the hood. File descriptors live in the kernel, while streams live in C standard library.

- *File position* is one of the attributes of a file. Therefore, streams and file descriptors (which both provide communication channels to files) both have file position as one of their attributes. File position on a stream can be changed with `fseek(3)`, and file position on a file descriptor can be changed using `lseek(2)`.
    - File position on a file descriptor is just an integer which is initialized to `0` and incremented with each written character.
    - Not all files support random-access (this is, the seek operation). You will receive the error `ESPIPE` ("error due to seeking on a pipe [or socket or FIFO]").
