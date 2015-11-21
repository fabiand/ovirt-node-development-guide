# Filesystem layout and concepts

To especially let upgrades work correctly imgbase is making a few assumptions about file locations and how the filesystem is organized.
These concepts are well defined by OSTree and the Stateless project from systemd.

A few relevant main points are:

* Only /etc and /var are writable and persisted.
* Vendor presets/configuration goes to /usr/etc
* User configuration goes to /etc
* The user configuration overrides the vendor presets
* Partial configuration snippets can be placed in <conf>.d

The assumption is that these mechanisms above provide enough structure to build robust upgrades.