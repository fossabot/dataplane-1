# A map of DPDK abstractions

This document provides a map of the various abstractions in [DPDK], and how they relate to each other.
This is intended to help new developers understand the structure of [DPDK], and how the various components fit together.

![DPDK entity-relationship diagram](./dpdk-map.svg?sanitize=true)
> The relationships between the various abstractions in DPDK

## Docs links / notes

* [flow_item](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#pattern-item")
* [flow_item_template](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#pattern-templates")
* [flow_action](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#actions")
* [flow_action_template](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#actions-templates")
* [flow_action_indirect](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#action-indirect")
* [flow_action_indirect_list](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#action-indirect-list")
* [switch_domain](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/switch_representation.html")
* [flow_table](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html#attribute-group")
* [flow](https://doc.dpdk.org/guides-24.11/prog_guide/ethdev/flow_offload.html")
* [hairpin_queue](https://inbox.dpdk.org/dev/1565703468-55617-1-git-send-email-orika@mellanox.com/")
* [membuf](https://doc.dpdk.org/guides/prog_guide/mbuf_lib.html")
* [mempool](https://doc.dpdk.org/guides/prog_guide/mempool_lib.html")
* [socket_id](#socket_id")
* [eth_dev](https://doc.dpdk.org/guides/nics/index.html")
* [queue_rx](https://doc.dpdk.org/guides/prog_guide/ring_lib.html")
* [queue_tx](https://doc.dpdk.org/guides/prog_guide/ring_lib.html")
* [socket_index](#socket_index)

## Glossary


* `socket_index` <a id="socket_index"></a>

  A 0-based index into the list of `socket_id`s in the system.

  Keep in mind that DPDK does _not_ always have access to every [NUMA] domain / socket on the system.
  See [warning](#socket_id_is_not_socket_index) for more information.

* `socket_id` <a id="socket_id"></a>

  A unique identifier for a socket.

  A better name for `socket_id` would have been [NUMA] node.  [NUMA] were historically functionally identical to CPU sockets, but in modern (e.g. AMD Genoa) chips that is not true.

  See [warning](#socket_id_is_not_socket_index) and [note](#socket_id_bit_rep) for more information.



> [!WARNING]
> <a id="socket_id_is_not_socket_index"></a>
> `socket_id` and `socket_index` are not the same thing.  
> `socket_id` is a unique identifier for a socket, while `socket_index` is an index into the list of sockets ids.
> **The two are related, but different.**  
> See [`rte_socket_id_by_idx`] for more information.

> [!NOTE]
> <a id="socket_id_bit_rep"></a>
> `socket_id` is usually represented as a _signed_, 32-bit integer (more exactly, it is a [`c_int`]).
> That said, [DPDK] is often sloppy with signs and bit widths.
> For instance, in the [`rte_lcore_to_socket_id`] function, `socket_id` is represented as an unsigned 32 bit integer.


[DPDK]: https://www.dpdk.org/

[NUMA]: https://en.wikipedia.org/wiki/Non-uniform_memory_access

[`rte_socket_id_by_idx`]: https://doc.dpdk.org/api/rte__lcore_8h.html#a688a671a9fb6c79203de98c684d6e7f2

[`c_int`]: https://doc.rust-lang.org/std/os/raw/type.c_int.html

[`rte_lcore_to_socket_id`]: https://doc.dpdk.org/api/rte__lcore_8h.html#a023b4909f52c3cdf0351d71d2b5032bc
