# Image build process

## Overview


![](imgs/build-flow.dot.png)


## Specification

As `anaconda` is used for building the image, a kickstart file is used to specify how the image should look.

> Note: The kickstart defining the oVirt Node appliance is hosted in [oVirt's ovirt-appliance repository](https://gerrit.ovirt.org/gitweb?p=ovirt-appliance.git;a=blob;f=node-appliance/ovirt-node-appliance.ks;hb=HEAD)

An example kickstart can look like:

    lang en_US.UTF-8
    keyboard us
    timezone --utc Etc/UTC
    auth --enableshadow --passalgo=sha512
    selinux --permissive
    rootpw --lock
    user --name=node --lock
    firstboot --reconfig
    clearpart --all --initlabel
    bootloader --timeout=1
    part / --size=3072 --fstype=ext4 --fsoptions=discard
    poweroff
    
    %packages
    # config generic == not-hostonly, this is needed
    # to support make a generic image (do not keep lvm informations in the image)
    dracut-config-generic
    
    # EFI support
    grub2-efi
    shim
    efibootmgr
    %end

A few notes on the kickstart above:

* `dracut-config-generic` - Needed to create initramfs'es with broad hardware support
* `grub2-efi`, `shim`, `efibootmgr` - To provide EFI support within the image (these packages will not be installed by anaconda, because they are not required at build time, but they could be required at installation time).

**FIXME** The package requirements should go to some package dependencies, i.e. `ovirt-release-node-host`.

## Build

If the kickstart defining the appliance is available, the image can be built using the tooling in the `ovirt-appliance` repository:

    make image-build


## Alternative build process: `image-tools`

Originally a bunch of scripts - `image-tools` - were used to build the appliance.

The `image-tools` [repository](https://github.com/fabiand/image-tools) contains some tooling to build the appliance images.

This is very redundant to `livemedia-creator` and `koji`.

> FIXME this tool should be obsoleted by koji and livemdia-creator

### Image Format: Liveimg

Node is installed (and updated) using a single operating system image.
Contrary to many other distributions packages are not used to install the operating system. Packages are primarily used to [build the image](build.md), and eventually to [customize the image](impl.md).

The liveimg image format is a Fedora- and CentOS-ish format used to deliver LiveCDs.
A liveimg is a file-system image wrapped into a squashfs image.
The reasoning behind this matroska mechanism is that the file-system image can be mounted easily, and the squashfs image - as it can compress - is helping to reduce the size of the image.
Because it has been around for a long time, this format has mature support in dracut and anaconda.
This effectively enables two use-cases with one image:

* anaconda can use this image as a source instead of individual rpms
* dracut can boot into a liveimg


## Deliveryformat

The appliance image is delivered in the squashfs liveimg format.

This format is understood by anaconda (for installation) and dracut (for state- and diskless boots).

The format is described in `man dracut.cmdline`:

    The filesystem structure is expected to be:

       squashfs.img          |  Squashfs downloaded via network
          !(mount)
          /LiveOS
              |- ext3fs.img  |  Filesystem image to mount read-only
                   !(mount)
                   /bin      |  Live filesystem
                   /boot     |
                   /dev      |
                   ...       |

> Note: the `ext3fs.img` is a file-system image, not a disk image.

The `ext3fs.img` can be created using a range of tools, the primary one being `livemedia-creator` (part of `lorax`).

[Eventually](https://bugzilla.redhat.com/show_bug.cgi?id=1282496) `livemedia-creator` will be capable of creating squashfs images directly.