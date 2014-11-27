
oVirt Engine integration
========================

The primary consumer of oVirt Node is oVirt Engine.
Several aspects of this integration are discussed in this section.


Local Image Discovery
---------------------

Engine can deploy updates of Node to existing Node setups.

This works roughly like this:

+ Discovery local updates
+ Suggest updates to user
+ Push update to Node instance

The discovery of the locally available updates is covered here.

A file is used to signal Engine which updates are available.

    /usr/lib/ovirt-node-appliance/updates.d/

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



Registration
------------

A approached solution is the generic registration.
In a nutshell: Generic registration will ask Engine to initiate the
registration with Node. This means the same registatraion mechanism
is used for Engine side and Node side initiated registration.
