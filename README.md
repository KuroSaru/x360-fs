===============================================
Source-Project: https://code.google.com/archive/p/x360/
Cloned for Academic Usage
=======================================
PREPATCHED VERSION.

I AM NOT THE MAINTAINER OR ORIGINAL CREATOR OF THIS PROJECT
IT HAS BEEN CLONED FOR ACADEMIC PURPOSES, TO MAKE SURE IT IS
NOT LOST. ~Kuro

=================
README : ORIGINAL 
===================

x360: A set of tools for working with the Xbox 360
Copyright (C) 2009-2011 by Isaac Tepper
Licensed under the terms of the GNU GPL v3


CONTENTS
========

1. Introduction
2. Building
3. Tools
   * xpart: Xbox 360 Partition Helper
   * xfd: Xbox Filesystem Driver
4. Libraries
   * libfatx: Userspace access to a FATX filesystem


INTRODUCTION
============

x360 is a set of tools that allow linux users to interface with their
Xbox 360. Currently, it is comprised of a filesystem driver and a
matching library (and a partition helper), but it will soon have some
other tools, such as a gamesave resigner and a media manager.

The name "x360" used to refer directly to the filesystem driver, but
now it refers to the collection of tools in general.



BUILDING
========

x360 has moved over to an automake build system. To build, simply run

     ./configure
     make
     make install

in the project directory. You can type "./configure --help" for more
information.



TOOLS
=====

xpart (Xbox 360 Partition Helper)

Usage: xpart /dev/sdX

Purpose: Splits /dev/sdX into three virtual device files representing
the three (known) partitions: /dev/sdx1, /dev/sdx2, and
/dev/sdx3. sdx1 will be the cache partition, sdx2 will be the Xbox
compatability partition, and sdx3 will be the Xbox 360 content
partition.

Note: There are two versions: xpart-dm, which uses device manager,
and xpart-loop, which uses loop devices. By default, xpart will be a
symlink to xpart-dm.



xfd (Xbox Filesystem Driver)

Usage: xfd-mount [options] /dev/sdcX /mnt
       mount -t fatx [options] /dev/sdcX /mnt

Options are: -d: debug mode, fuse does not daemonize and prints
syscalls as they happen. Also useful for getting warnings from
libfatx.

Purpose: Mounts a FATX partition, allowing you to read and change it's
contents (but currently libfatx has read support only). xfd (or, more
specifically, libfatx) has support for filesystems of any size, big or
little endian, with 16 bit FAT or 32 bit FAT.

Note: You can invoke this through "mount -t fatx", but that method
requires you to be root, whereas simply using xfd-mount does not
require you to be root. Not being root is always better :)



LIBRARIES
=========

libfatx (Userspace access to a FATX filesystem)

libfatx handles the filesystem access for xfd, and will for other
utilities in the future (such as a media manager). Like everything
else, it is a work in progress, and this list of features will
describe its current state:

Implemented Features:

* Runtime detection and handling of little-endian/big-endian
  filesystems

* Runtime detection and handling of 16-bit/32-bit filesystems

* Directory listing that steps through multi-cluster directories

* File/directory offset locator that steps through multi-cluster
  directories

* Reading files

* Translating FATX timestamps to/from unix time

Features Coming Soon:

* Write files, truncate (expand and shrink) files, create files,
  delete files

libfatx is a complete re-write, which is why write support is not
implemented yet. It's been thoroughly tested (as opposed to the
previous version which appearantly froze up a lot), and everything
that is implemented should work without error.