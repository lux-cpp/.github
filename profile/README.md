# Lux C++

High-performance C++ kernel and GPU acceleration for the Lux Network. The
performance moat under the public Go reference implementations published at
[github.com/luxfi](https://github.com/luxfi).

## Architecture

```
+------------------------------------------------------------------+
|                          Lux C++ Stack                           |
+------------------------------------------------------------------+
|  +-----------+  +------------+  +-------------+  +----------+    |
|  |  liblux   |  | libluxfhe  |  | libluxcrypt |  |  luxvm   |    |
|  |  (Core)   |  |   (FHE)    |  |   (Crypto)  |  |   (VM)   |    |
|  +-----------+  +------------+  +-------------+  +----------+    |
|                              |                                   |
|  +------------------------------------------------------------+  |
|  |                LLVM-based Compilation                      |  |
|  |        Python  Rust  Go  Ruby  Elixir bindings             |  |
|  +------------------------------------------------------------+  |
|                              |                                   |
|  +------------------------------------------------------------+  |
|  |             Hardware Acceleration                          |  |
|  |     CUDA   ROCm   Metal   AVX-512   NEON   FPGA            |  |
|  +------------------------------------------------------------+  |
+------------------------------------------------------------------+
```

## Repositories

### Core Libraries
| Repository | Description |
|------------|-------------|
| [liblux](https://github.com/luxcpp/liblux) | Core Lux library |
| [libluxfhe](https://github.com/luxcpp/libluxfhe) | FHE operations |
| [libluxcrypto](https://github.com/luxcpp/libluxcrypto) | Cryptographic primitives |
| [luxvm](https://github.com/luxcpp/luxvm) | Virtual machine |

### Acceleration
| Repository | Description |
|------------|-------------|
| [luxaccel](https://github.com/luxcpp/luxaccel) | GPU acceleration |
| [luxntt](https://github.com/luxcpp/luxntt) | NTT implementations |
| [luxfft](https://github.com/luxcpp/luxfft) | FFT implementations |

### Bindings
| Repository | Description |
|------------|-------------|
| [luxpy](https://github.com/luxcpp/luxpy) | Python bindings |
| [luxrs](https://github.com/luxcpp/luxrs) | Rust bindings |
| [luxgo](https://github.com/luxcpp/luxgo) | Go bindings (CGO) |

## Quick Start

### Build from Source
```bash
git clone https://github.com/luxcpp/liblux
cd liblux
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
sudo make install
```

### Use in CMake Project
```cmake
find_package(luxfhe REQUIRED)
target_link_libraries(myapp luxfhe::luxfhe)
```

### C Example
```c
#include <luxfhe.h>

luxfhe_context_t* ctx = luxfhe_init();
luxfhe_keygen(ctx);

luxfhe_ciphertext_t* ct = luxfhe_encrypt_u64(ctx, 42);
// Compute on encrypted data...

luxfhe_destroy(ctx);
```

### C++ Example
```cpp
#include <luxfhe.hpp>

auto ctx = luxfhe::Context::create();
ctx->keygen();

auto ct = ctx->encrypt(42);
auto result = ct + ctx->encrypt(8);
std::cout << ctx->decrypt<uint64_t>(result);  // 50
```

## Build Requirements

- CMake 3.20+
- C++20 compiler (GCC 12+, Clang 15+, MSVC 2022+)
- Optional: CUDA 12+, ROCm 5+, Metal

## IP and Licensing

`luxcpp` is the C++ kernel and GPU acceleration org for the Lux Network.
It is one of three tiers in the Lux IP strategy:

1. **Public** — `github.com/luxfi/*` (BSD-3-Clause Go reference + a few
   inherited upstream licenses).
2. **Patent-protected** — `github.com/luxfi/*` Eco-tier and `luxcpp/*`
   Eco-tier subdirs (Lux Ecosystem License v1.2). Free for Authorized
   Networks; commercial license required outside.
3. **Private moat** — `lux-private/*` (private GitHub org) and the
   PROPRIETARY subdirs in `luxcpp/*`. Closed source. Commercial license
   only.

**The canonical IP / licensing strategy document is the Lux org profile:
[github.com/luxfi/.github/blob/main/profile/README.md](https://github.com/luxfi/.github/blob/main/profile/README.md).
Read it.** That page is the source of truth for tier definitions,
"Authorized Network", "Descending Chain", commercial-license CTAs, and
extraction status for `lux-private/*`.

The table below records the binding license declared in each `luxcpp`
subdirectory's `LICENSE` file. The `LICENSE` file is the binding artifact;
this table is a navigational aid.

| Subdir | License | Tier |
|--------|---------|------|
| cevm | Apache-2.0 | Public (going-forward C++ EVM kernel; replaces LGPL `luxfi/evm` over time) |
| crypto | Lux Ecosystem v1.2 | Patent-protected |
| cuda | PROPRIETARY (Lux Industries Inc.) | Private moat |
| dex | BSD-3-Clause Ecosystem | Public |
| evmc | Apache-2.0 | Public |
| fhe | Lux Ecosystem v1.2 | Patent-protected |
| gpu | BSD-3-Clause | Public |
| grpc | Apache-2.0 | Public |
| http | MIT (Drogon) | Public |
| lattice | Lux Ecosystem v1.2 | Patent-protected |
| session | MIT (libsession-util) | Public |
| zap-cpp-core | Apache-2.0 | Public |

Subdirectories without a `LICENSE` file (`aivm`, `bridgevm`, `consensus`,
`lux-accel`, `lux-cuda`, `lux-gpu`, `lux-metal`, `lux-webgpu`,
`luxcpp.github.io`, `metal`, `mpcvm`, `platformvm`, `webgpu`, `xvm`) are
**all-rights-reserved** until a `LICENSE` file is added. The GPU kernel
subdirs (`lux-cuda`, `lux-gpu`, `lux-metal`, `lux-webgpu`) are slated for
extraction into `lux-private/gpu-kernels` once that org is bootstrapped.
Contact `licensing@lux.network` for commercial use.

### What this means for you

- Building a research prototype, academic paper, hobbyist tool? Free
  under "Research Use" / personal use across all visible tiers.
- Building a Lux Descending Chain (subnet of Lux Primary or downstream)?
  You are an Authorized Network. Eco-tier code is free.
- Building a sovereign L1 unrelated to Lux and want to embed `crypto`,
  `fhe`, `lattice`, etc.? You need a commercial license —
  `licensing@lux.network`.
- Need the production C++/CUDA/Metal performance kernels (`cuda/*` here,
  `lux-private/*` once extracted)? Contract via `licensing@lux.network`.

There are **no planned license flips** from Eco to BSD-3 in either org —
the Eco tier is the catalog Lux licenses commercially, and loosening it
would erase that revenue surface.

## Related Organizations

| Organization | Focus | Link |
|--------------|-------|------|
| **Lux C++** | C++ kernel and GPU acceleration | [github.com/luxcpp](https://github.com/luxcpp) |
| **Lux Network** | Go reference implementation | [github.com/luxfi](https://github.com/luxfi) |
| **Lux FHE** | FHE docs and examples | [github.com/luxfhe](https://github.com/luxfhe) |
| **Hanzo AI** | AI infrastructure | [github.com/hanzoai](https://github.com/hanzoai) |

---

Part of the [Lux Network](https://lux.network) ecosystem.
