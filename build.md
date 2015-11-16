# Image build process

The appliance image is delivered in the squashfs liveimg format.
This format is understood by anaconda and dracut.

## Deliveryformat

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


## Specification

As `anaconda` is used for building the image, a kickstart file is used to specify how the image should look.

## Build

