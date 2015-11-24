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
