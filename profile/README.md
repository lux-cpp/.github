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

`luxcpp` is the C++ kernel and GPU acceleration org. It implements a mix
of public reference primitives, patent-protected inventions, and
production-grade closed-source kernels that constitute the Lux performance
moat.

The full Lux IP and licensing strategy lives at the canonical Lux org
profile: [github.com/luxfi/.github/blob/main/profile/README.md](https://github.com/luxfi/.github/blob/main/profile/README.md).
That document is the source of truth. The table below records the binding
license declared in each `luxcpp` repository's `LICENSE` file.

| Subdir | License | Tier |
|--------|---------|------|
| cevm | Apache-2.0 | Public |
| crypto | Lux Ecosystem v1.2 | Patent-protected |
| cuda | Proprietary | Private moat |
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
considered all-rights-reserved private moat until a `LICENSE` file is
added. Contact `licensing@lux.network` for commercial use.

## Related Organizations

| Organization | Focus | Link |
|--------------|-------|------|
| **Lux C++** | C++ kernel and GPU acceleration | [github.com/luxcpp](https://github.com/luxcpp) |
| **Lux Network** | Go reference implementation | [github.com/luxfi](https://github.com/luxfi) |
| **Lux FHE** | FHE docs and examples | [github.com/luxfhe](https://github.com/luxfhe) |
| **Hanzo AI** | AI infrastructure | [github.com/hanzoai](https://github.com/hanzoai) |

---

Part of the [Lux Network](https://lux.network) ecosystem.
