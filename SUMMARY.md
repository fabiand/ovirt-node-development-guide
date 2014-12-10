Summary
=======

* [Introduction](README.md)
* [Appliance Specification](README.md#spec)
* [Lifecycle](runtime/README.md)
  * [Installation](runtime.md#installation)
    * Manual
    * Automatic
  * [Configuration](runtime.md#configuration)
    * Local
    * Management
  * [Customization](runtime.md#customization)
  * [Upgrade & Rollback](runtime.md#upgrade)
    * Persistence
  * [Removal](runtime.md#removal)
* [Implementation](impl.md#README)
  * [Platform / Appliance](impl.md#platform)
    * Specification
    * Build
  * [LVM Thin](impl.md#lvm/)
    * Creation
    * Update
    * Fallback
  * [Persistence](impl.md#persistence)
  * [BLS](impl.md#boot)
  * [Kickstart generator](impl.md#kickstart_from_cmdline)
* [Testing](testing.md)
  * Static checking
  * Unit testing
  * Functional testing
* [Customization / Extending](customization.md)
  * Derived specification
  * Offline image modification
  * Online customization
* [oVirt Engine integration](engine.md)
  * Local image discovery
  * Registration
