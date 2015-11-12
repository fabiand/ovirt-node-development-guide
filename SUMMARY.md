Summary
=======

* [Introduction](README.md)
* [Design](design.md)
* [Appliance Specification](README.md#spec)
* [Lifecycle](runtime/README.md)
  * [Installation](runtime.md#installation)
    * Manual
    * Automatic
  * [Configuration](runtime.md#configuration)
    * Local
    * Managed
  * [Upgrade & Rollback](runtime.md#upgrade)
    * Persistence
  * [Removal](runtime.md#removal)
  * [Customization](runtime.md#customization)
    * Package installation
    * Plugins
* [Implementation](impl.md#README)
  * [Platform / Appliance](impl.md#platform)
    * Specification
    * Build
  * [Image Storage](impl.md#lvm)
    * Creation
    * Update
    * Fallback
  * [Fallback](impl.md#boot)
    * BLS
  * [Persistence](impl.md#persistence)
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
