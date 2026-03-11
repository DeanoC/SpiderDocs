# Acheron WorldFS Overview

This page describes the namespace model at a conceptual level. The exact Acheron
wire protocol and node-FS message catalog are maintained in the canonical
`spider-protocol` reference docs.

## Namespace Model

- Acheron is the filesystem-style protocol surface that exposes the Spiderweb
  namespace to agents and external clients.
- The visible namespace is projected from runtime state, built-in venoms, and
  node-exported services.
- Node filesystem traffic is carried over Acheron JSON envelopes on `/v2/fs`.

## Canonical References

Canonical reference:
- [`acheron-runtime-v1.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/acheron-runtime-v1.md)

Related canonical references:
- [`node-fs-unified-v2.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/node-fs-unified-v2.md)
- [`unified-v2-control.md`](../../Spiderweb/deps/spider-protocol/docs/protocols/unified-v2-control.md)

## Namespace Layout

The current namespace layout is still best understood from the runtime and
product docs in `SpiderDocs/runtime/` and `SpiderDocs/protocols/`, but message
names, handshake order, and fixture examples should be read from the canonical
reference set above.
