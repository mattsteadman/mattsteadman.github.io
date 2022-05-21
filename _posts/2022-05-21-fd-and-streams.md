---
layout: post
title:  "File Descriptors and Streams"
date:   2022-05-21 13:30:00
categories: [R]
permalink: fd-and-streams
description: "What's the difference between file descriptors and streams?"
---
# File Descriptor and Stream

Unix has two similar concepts for reading and writing file-like objects. The first, file descriptors, is used by lower-level functions like `read(2)`. The second, streams, is used by higher-level functions like `fprintf(3)`. So what are the similarities and differences between them?

- File descriptors are represented by objects of type `int`. Streams are represented by objects of type `FILE *`.

- Streams *themselves* use file descriptors to access files. Streams are a layer *on top* of file descriptors to take care of some of the details of the most common kinds of I/O.

- Both can represent connections to files, devices (e.g terminals), and pipes/sockets (for IPC).

- Why use streams? Because using streams gives you access to a more powerful set of functions. Namely, formatted I/O functions like `printf` and `scanf`, and functions for character- and line-oriented I/O.

- If you want to do control operations that are specific to a particular device, then you *must* use file descriptors.

- If you need special modes of I/O (e.g. nonblocking input) then you must use file descriptors.

- The only control that streams give you is the choice of styles of buffering (unbuffered, line buffered, fully buffered).

- If you want, you can request that a streams gives you the file descriptor that it's using under the hood so that you can "get dirty" and do some low-level operations.

- You can also "upgrade" a file descriptor to a stream. That is, create a new stream with an existing file descriptor.

- In general try using a stream before deciding that you need to use a file descriptor unless you have a good reason to do otherwise.

- File descriptors are a POSIX feature, whereas streams are an ISO C feature. Therefore, streams are more portable than file descriptors. Non-POSIX systems are free to implement streams using something besides file descriptors under the hood.
  - File descriptors are implemented in kernelspace. Streams are implemented in userspace to make the most common kinds of I/O easier.

- *File position* is one of the attributes of a file. Therefore, streams and file descriptors (which both provide communication channels to files) both have file position as one of their attributes. File position on a stream can be changed with `fseek(3)`, and file position on a file descriptor can be changed using `lseek(2)`.
    - File position on a file descriptor is just an integer which is initialized to `0` and incremented with each written character.
    - Not all files support random-access (this is, the seek operation). You will receive the error `ESPIPE` ("error due to seeking on a pipe [or socket or FIFO]").
