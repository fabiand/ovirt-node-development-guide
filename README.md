Documentation
=============

[oVirt Node](http://www.ovirt.org/Node) is a small scale operating system acting as a hypervisor under the oVirt umbrella. The expectation on Node is closer to that of a firmware than to a general purpose operating system.

This guide is intended for developers, it describes the design and implementation of Node, to learn how to use and contribute to Node.

## Leveling expectations

Node tries to meet a couple of goals:

+ **Stable** is a main goal. We want a reliable hypervisor.
+ **Easy to use** because it provides everything needed and is easy to administrate
+ **Upgrades with Rollback** to rollback if an upgrade fails or leads to an unstable environment
+ **Online & Offline Customization** for installing debugging packages and extending the base image
+ **Testable** to support the goal of being stable

Node is not aiming for the following goals:

+ General purpose operating system
+ Flexible
+ Package based
+ Minimal (tho we try to have an eye on bloat)


# Getting started

These few steps help you to get your hands onto Node.

## Build

To get started with Node, you first need to clone the appliance and build it:

    git clone git://gerrit.ovirt.org/ovirt-appliance.git
    git submodule update --init --recursive
    
    cd node-appliance
    
    # To build the squashfs image (liveimg):
    make image-build

**Note:** The `ovirt-node-appliance.ks` is used to build the `ovirt-node-appliance-squashfs-img`

The created `ovirt-node-appliance.squashfs.img` contains the root-file-system and will be used for installation.

## Install

You need

1. a CentOS 7 boot ISO and
2. a kickstart to tell anaconda where to get the squashfs image from
 
There is a `makefile` target to simulate this locally using `qemu`:

    make image-install

This command will download the correct CentOS 7 images and pass them to `qemu` to launch an installation which will in turn install the previously created squashfs image into a VM.

After the installation you can import the container into libvirt to use it.

**Hint:** The `ovirt-node-appliance-auto-installation.ks` file is used for the auto-installation of the squashfs image.

### Create USB media

The squashfs image, a kickstart, and  `livecd-iso-to-disk` can be used to create a bootable USB media using the following steps:

1. Fetch a CentOS 7 installation ISO
2. Create a kickstart file using: `echo "liveimg --url=file://ovirt-node-appliance.squashfs.img" > liveimg-install.ks`
3. Run `livecd-iso-to-disk $CENTOS_ISO $DISK --ks liveimg-install.ks`
4. Mount the created disk, and copy the squashfs image to the same directory as the `liveimg-install.ks` file.

FIXME These steps are probably not working right now, needs testing