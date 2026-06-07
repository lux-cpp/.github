# Lux C++

Public, **permissively-licensed** C/C++ build dependencies for the Lux
Network's Go node and reference crypto — vendored upstreams and thin glue.
Everything in this org is BSD/MIT/Apache/upstream, so the Lux node and crypto
build and run on the **pure-Go path with no license required**.

The high-performance GPU kernels and advanced C++ acceleration — "the moat" —
have been **extracted to the private, licensed
[`lux-private`](https://github.com/lux-private)** org and ship as prebuilt
**binary plugins** to licensed users. The pure-Go node loads them at runtime
when present and falls back to the permissive pure-Go implementations
otherwise.

## Where things live (post-extraction)

| Layer | Repos | License | Build |
|-------|-------|---------|-------|
| **Chain + crypto (reference)** | [`luxfi/node`](https://github.com/luxfi/node), [`luxfi/crypto`](https://github.com/luxfi/crypto), [`luxfi/accel`](https://github.com/luxfi/accel) | BSD-3 / permissive | pure-Go, `CGO_ENABLED=0`, **no license** |
| **C build deps (this org)** | `blst`, `pqclean`, `intx`, `evmc`, `evmmax`, `ed25519-donna`, `blake3-reference`, `grpc`, `http`, `session`, `zap-cpp-core` | permissive / upstream | optional `CGO_ENABLED=1` |
| **GPU + advanced C++ (the moat)** | [`lux-private/*`](https://github.com/lux-private) — `gpu`, `gpu-kernels`, `lux-{metal,cuda,webgpu}`, `metal`, `cuda`, `webgpu`, `fhe`, `cevm`, `crypto`, `lattice`, `accel`, `aivm`, `mpcvm`, `xvm`, … | proprietary / licensed | binary plugins (Conan, reproducible) |

## Principle

Pure-Go does everything correctly and permissively — **the chain runs with no
C++ or GPU**. The C++/GPU layer is a *licensed accelerator* that drops in at
runtime:

```bash
CGO_ENABLED=0 go build ./...   # permissive path — full chain, no license
# add the licensed lux-private plugins for GPU-accelerated crypto on supported HW
```

## Licensing

This org is the permissive build-dependency tier. The full Lux IP / licensing
strategy — tier definitions, "Authorized Network", "Descending Chain",
commercial-license terms, and the `lux-private` moat — is canonical at the Lux
org profile:
**[github.com/luxfi/.github](https://github.com/luxfi/.github/blob/main/profile/README.md)**.

- Building on Lux / a Descending Chain, or a research/hobby project? Free under
  the permissive tier here + `luxfi/*`.
- Need the production GPU/CUDA/Metal kernels (`lux-private/*`)? Commercial
  license — `licensing@lux.network`.

## Related Organizations

| Organization | Focus | Link |
|--------------|-------|------|
| **Lux Network** | Go reference implementation (permissive) | [github.com/luxfi](https://github.com/luxfi) |
| **Lux C++** | Permissive C/C++ build deps (this org) | [github.com/luxcpp](https://github.com/luxcpp) |
| **Lux Private** | GPU kernels + advanced C++ (licensed) | [github.com/lux-private](https://github.com/lux-private) |
| **Hanzo AI** | AI infrastructure | [github.com/hanzoai](https://github.com/hanzoai) |

---

Part of the [Lux Network](https://lux.network) ecosystem.
