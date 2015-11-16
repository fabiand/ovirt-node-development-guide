Documentation
=============

[oVirt Node](http://www.ovirt.org/Node) is a small scale operating system acting as a hypervisor under the oVirt umbrella. The overall experience is closer to a firmware than to a general purpose operating system.

This document describes the anatomy of Node.
You will learn from which Linux distribution it is derived, how the root filesystem is created, how images are delivered, how you can test and extend it.
Also the low-level techniques are described to soo how this goals are achieved.


## Leveling expectations

Node tries to meet a couple of goals:

+ **Stable** is a main goal. We want a reliable hypervisor.
+ **Secure** by using SELinux in enforcing mode.
+ **Easy to use** by streamlining access to the necessary functionality, i.e. with a TUI
+ **Upgrade & Rollback** by being able to go back to a working version,
  if a new one is broken (and contradiction the **stable** goal)
+ **Testable** to support the goal of beeing stable
+ **Extendable** by others (users) to allow small adjustments to suite the environment Node is living in
+ **Minimal** in the terms of disk footprint, though it hasn't got the highest priority


What we do not want to achieve

+ General prupose operating system
+ Flexible
+ Package based
