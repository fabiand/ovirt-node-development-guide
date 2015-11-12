# Design

## Core concepts

The design relies on a couple of distinct and independent concepts:

* Image format: liveimg
* Installation: anaconda
* Upgrade & Rollback: imgbased
* Filesystem layout and concepts: Like [OSTree](https://github.com/GNOME/ostree) and ["Project Stateless"](http://0pointer.net/blog/projects/stateless.html)

## Image Format: Liveimg

The liveimg image format is a Fedora- and CentOS-ish format used to deliver LiveCDs.
A liveimg is a filesystem image wrapped into a squashfs image.
The reasoning behind this matroska mechanism is that the fileystem image can be mounted easily, and the squashfs image - as it can compress - is helping to reduce the size of the image.
Because it has been around for a long time, this format has mature support in dracut and anaconda.
This effectively enables two use-cases with one image:

* anaconda can use this image as a source instead of individual rpms
* dracut can boot into a liveimg

In addition - and implicit - in an image we have a single delivery for a complete OS.

## Anaconda

As stated above, anaconda can read use the liveimg as an installation source. All other functionality of anaconda works without limitations.
Anaconda can be used as-is, no customizations are needed.

## Upgrades & Rollback: imgbase

imgbase is the only new component with a larger code-base.
imgbase is actually a high-level frontend to LVM, enforcing a specific usage pattern.

In addition it has plugins to create boot entries for specific LVs, and some logic to migrate /etc from liveimg to liveimg.

## Filesystem layout and concepts

To especially let upgrades work correctly imgbase is making a few assumptions about file locations and how the filesystem is organized.
These concepts are well defined by OSTree and the Stateless project from systemd.

A few relevant main points are:

* Only /etc and /var are writable and persisted.
* Vendor presets/configuration goes to /usr/etc
* User configuration goes to /etc
* The user configuration overrides the vendor presets
* Partial configuration snippets can be placed in <conf>.d

The assumption is that these mechanisms above provide enough structure to build robust upgrades.