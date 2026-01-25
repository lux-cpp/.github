# Lux C++ 🔧

**High-Performance C++ Libraries for Lux Network**

Native C++ implementations for cryptography, FHE, and blockchain components with maximum performance.

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      Lux C++ Stack                              │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────┬─────────────┬─────────────┬─────────────┐      │
│  │   liblux    │  libluxfhe  │ libluxcrypto│  luxvm      │      │
│  │   (Core)    │    (FHE)    │   (Crypto)  │   (VM)      │      │
│  └─────────────┴─────────────┴─────────────┴─────────────┘      │
│                              │                                   │
│  ┌───────────────────────────────────────────────────────┐      │
│  │              LLVM-based Compilation                    │      │
│  │         Python • Rust • Go • Ruby • Elixir            │      │
│  └───────────────────────────────────────────────────────┘      │
│                              │                                   │
│  ┌───────────────────────────────────────────────────────┐      │
│  │           Hardware Acceleration                        │      │
│  │      CUDA • ROCm • Metal • AVX-512 • NEON             │      │
│  └───────────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

## 📦 Repositories

### Core Libraries
| Repository | Description | Status |
|------------|-------------|--------|
| [liblux](https://github.com/luxcpp/liblux) | Core Lux library | ✅ Stable |
| [libluxfhe](https://github.com/luxcpp/libluxfhe) | FHE operations | ✅ Stable |
| [libluxcrypto](https://github.com/luxcpp/libluxcrypto) | Cryptographic primitives | ✅ Stable |
| [luxvm](https://github.com/luxcpp/luxvm) | Virtual machine | 🚧 Beta |

### Acceleration
| Repository | Description | Status |
|------------|-------------|--------|
| [luxaccel](https://github.com/luxcpp/luxaccel) | GPU acceleration | ✅ Stable |
| [luxntt](https://github.com/luxcpp/luxntt) | NTT implementations | ✅ Stable |
| [luxfft](https://github.com/luxcpp/luxfft) | FFT implementations | ✅ Stable |

### Bindings
| Repository | Description | Status |
|------------|-------------|--------|
| [luxpy](https://github.com/luxcpp/luxpy) | Python bindings | ✅ Stable |
| [luxrs](https://github.com/luxcpp/luxrs) | Rust bindings | ✅ Stable |
| [luxgo](https://github.com/luxcpp/luxgo) | Go bindings (CGO) | ✅ Stable |

## 🚀 Quick Start

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

## 🔧 Build Requirements

- CMake 3.20+
- C++20 compiler (GCC 12+, Clang 15+, MSVC 2022+)
- Optional: CUDA 12+, ROCm 5+, Metal

## 🔗 Related Organizations

| Organization | Focus | Link |
|--------------|-------|------|
| **Lux C++** | C++ implementations | [github.com/luxcpp](https://github.com/luxcpp) |
| **Lux Network** | Go implementations | [github.com/luxfi](https://github.com/luxfi) |
| **Lux FHE** | Docs & examples | [github.com/luxfhe](https://github.com/luxfhe) |
| **Hanzo AI** | AI infrastructure | [github.com/hanzoai](https://github.com/hanzoai) |

## 📄 License

Apache 2.0 - See individual repositories for details.

---

**Part of the [Lux Network](https://lux.network) ecosystem**
