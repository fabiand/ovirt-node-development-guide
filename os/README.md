
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


Plain qemu approach
-------------------

Benefit: Has few assumptions about the host.


livemedia-creator approach
--------------------------

Benefit: Is fairly well defined way of building an appliance.

