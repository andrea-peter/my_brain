# LazyVim - Package manager

{% embed url="https://lazy.folke.io" %}

## Plugin spec

[https://lazy.folke.io/spec](https://lazy.folke.io/spec)

* `init`: `fun(LazyPlugin)`, always executed at startup
* `opts`:&#x20;
  * table: will be merged with parent specs)
  * `fun(LazyPlugin, opts:table)`:
    * &#x20;return a table to replaces parent specs
    * or just change the received table&#x20;
* `config`:&#x20;
  * `fun(LazyPlugin, opts:table)`: The default implementation will automatically run `require(MAIN).setup(opts)` if `opts` or `config = true` is set
  * `true`: See above

