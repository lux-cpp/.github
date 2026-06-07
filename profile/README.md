# Lux C++

Public, **permissively-licensed** C/C++ build dependencies for the Lux
Network's Go node and reference crypto — vendored upstreams and thin glue.
Everything in this org is BSD/MIT/Apache/upstream, so the Lux node and crypto
build and run on the **pure-Go path with no license required**.

## Where things live

| Layer | Repos | License | Build |
|-------|-------|---------|-------|
| **Chain + crypto (reference)** | [`luxfi/node`](https://github.com/luxfi/node), [`luxfi/crypto`](https://github.com/luxfi/crypto), [`luxfi/accel`](https://github.com/luxfi/accel) | BSD-3 / permissive | pure-Go, `CGO_ENABLED=0`, **no license** |
| **C build deps (this org)** | `blst`, `pqclean`, `intx`, `evmc`, `evmmax`, `ed25519-donna`, `blake3-reference`, `grpc`, `http`, `session`, `zap-cpp-core` | permissive / upstream | optional `CGO_ENABLED=1` |
| **GPU acceleration** | proprietary — **commercial license** | proprietary | prebuilt binary plugins |

The pure-Go chain runs with **no C++ or GPU**. GPU acceleration is an optional,
licensed accelerator that loads at runtime on supported hardware.

## High-performance GPU acceleration (licensed)

Lux ships GPU-optimized implementations across the entire stack:

| Component | What's accelerated |
|-----------|--------------------|
| **EVM (C-Chain)** | GPU Block-STM parallel execution; GPU precompiles (BN254, KZG, modexp, secp256k1 ecrecover) |
| **DEX** | GPU order-book matching engine + AMM / CLOB |
| **FHE** | GPU TFHE bootstrapping (NTT-fused) — portable across NVIDIA, AMD, and Apple |
| **Crypto** | GPU batch BLS12-381, ML-DSA, ML-KEM, SLH-DSA, Poseidon2, MSM, Keccak |
| **All chains** | GPU-accelerated X / P / C / M-Chain, Bridge, and AI VMs |

**Backends:** Metal (Apple Silicon) · CUDA (NVIDIA) · Vulkan (cross-vendor) ·
WebGPU/WGSL (portable) · HIP (AMD/ROCm). One portable kernel set, native
per-platform — a single SPIR-V binary spans NVIDIA, AMD, and Apple.

Performance figures, detailed benchmarks, and access to the accelerated builds
are provided **under commercial license**. **Contact licensing@lux.network** —
access is granted upon licensing.

## Licensing

- Building on Lux, a Descending Chain, or a research/hobby project? **Free** under
  the permissive tier (this org + [`luxfi/*`](https://github.com/luxfi)).
- Need the GPU-accelerated production builds? **Commercial license** —
  `licensing@lux.network`.

## Related Organizations

| Organization | Focus | Link |
|--------------|-------|------|
| **Lux Network** | Go reference implementation (permissive) | [github.com/luxfi](https://github.com/luxfi) |
| **Lux C++** | Permissive C/C++ build deps (this org) | [github.com/luxcpp](https://github.com/luxcpp) |
| **Hanzo AI** | AI infrastructure | [github.com/hanzoai](https://github.com/hanzoai) |

---

Part of the [Lux Network](https://lux.network) ecosystem.
