
oVirt Engine Integration
========================

The primary consumer of oVirt Node is oVirt Engine.
Several aspects of this integration are discussed in this section.


Local Image Discovery
---------------------

Images stored on a host on which Engine resides as well are called _local images_.

These local images _could_ be used by Engine to

+ deploy updates to existing Node setups
+ deploy new Nodes through Foreman (_idea-only_)

The discovery of the locally available updates is covered here.

A file is used to signal Engine which updates are available.

    /usr/lib/ovirt-node-appliance/images.d/

The file should contain a pointer to the image, as well as some additional
imfornatioms which can be used by Engine to offer suggestions to a user.

    [image]
    filename=
    checksum=
    builddate=

    [platform]
    name=Fedora
    version=20
    builddate=

    [ovirt]
    version=3.5
    builddate=


Updating
--------

Engine can use the local images to discover updates for existing Node setups.

The update itself is roughly working like this:

+ Discover local updates
+ Suggest updates to user
+ Push update to Node instance


Registration
------------

The approached solution is the generic registration.

In a nutshell: Generic registration will ask Engine to initiate the
registration with Node. This means the same mechanism
is used for Engine side and Node side initiated registration.
