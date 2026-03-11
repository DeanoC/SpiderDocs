# Node Service Catalog Overview

This page explains the role of node-exported venoms and namespace drivers at a
high level. It no longer carries the canonical message list because that drifted
from the implementation.

## What The Catalog Represents

- Nodes publish venom metadata into the control plane.
- Spiderweb projects that metadata into the namespace and into workspace mount
  selection.
- Executable namespace venoms can be backed by native process, native in-proc,
  or WASM runtimes.

## Canonical References

Canonical reference:
- [`unified-v2-control.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/unified-v2-control.md)

Related canonical references:
- [`namespace-driver-abi-v1.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/namespace-driver-abi-v1.md)
- [`spider-venom-wasm-abi-v1.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/spider-venom-wasm-abi-v1.md)

## Notes

- The canonical control reference is the source of truth for currently supported
  `control.*` catalog operations.
- Older watch/event names that were previously documented here are intentionally
  not repeated in this overview unless they are present in the canonical
  generated reference.
