
Node is not created from source, but is basically a slimmed down version of

+ Fedora
+ CentOS or
+ RHEL

There are two steps to create the root filesystem and create an image:

+ Specify the packages to get installed
+ Let the image be build (with some additional post-processing)


Specifying the platform
=======================

The platform is specified using a regular kickstart.

There are no special requirements that need to be met, it only needs to be ensured that the tools required at runtime are contained within the root filesystem.

As the root filesystem is intended to be a filesystem, it needs to be ensured that the partitioning is plain and simple.


Building the image
==================

Creating the appliance image is fairly simple:

+ Prepare the kickstart
+ Feed kickstart to anaconda, run in a VM (eitehr using plain `qemu` or `livemedia-creator`)

Once anaconda finishes the target image will contain the rootfs.

Independently of what method is used, this works as follows:

+ A qcow2 target image is created, it will hold the rootfs
+ A VM is spawned, booting the kernel, initrd, append line from a
  boot ISO. The kickstart specifying the rootfs is passed as a kernel
  argument
+ anaconda get's started as part of the boot process, it retirves the
  kickstart url from the cmldine, fetches it and starts the
  installation.
  + The target disk is formated
  + A package manager (yum/dnf) is called to install the packages on disk
    like in a regular transaction

`livemedia-creator` encapsulatres most of this in a single command, the plain `qemu` approach
does all fo this in steps. Each approach has it's drawbacks and benefits.


Plain qemu approach
-------------------

Benefit: Has few assumptions about the host.


livemedia-creator approach
--------------------------

Benefit: Is fairly well defined way of building an appliance.

