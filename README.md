# SnCore

Core foundation for Sn* projects. Provides platform detection, utility macros, API export/import helpers,
common callback type definitions, and cross-platform UTF-8/UTF-16 conversion utilities.

## The Sn Project
The **Sn Project** is a collection of modular C libraries designed to provide reusable building blocks for native software development.
Each library focuses on a specific area while sharing consistent design principles and API conventions.
The project originated from an experimental cross-platform game engine, with reusable components gradually extracted into standalone libraries as the repeated-need pattern emerged.

| Library | Description |
|---------|-------------|
| [**SnCore**](https://github.com/kshku/SnCore) | Core foundation for Sn libraries |
| [**SnMemory**](https://github.com/kshku/SnMemory) | Memory allocators and virtual memory abstraction |
| [**SnThreads**](https://github.com/kshku/SnThreads) | Thread and synchronization abstraction library |
| [**SnLogger**](https://github.com/kshku/SnLogger) | Logging library with synchronous and asynchronous modes |
| [**SnPlatform**](https://github.com/kshku/SnPlatform) | Platform abstraction layer |
| [**SnContainer**](https://github.com/kshku/SnContainer) | Generic container library |
| [**SnFile**](https://github.com/kshku/SnFile) | File system and I/O utilities |
| [**SnEnv**](https://github.com/kshku/SnEnv) | Environment variable and process environment utilities |
| [**SnDL**](https://github.com/kshku/SnDL) | Dynamic loading library for shared libraries |
| [**SnTime**](https://github.com/kshku/SnTime) | Time and clock utilities |
| [**SnTracer**](https://github.com/kshku/SnTracer) | Tracing library |
| [**SnTest**](https://github.com/kshku/SnTest) | Unit testing framework |
| [**SnNetwork**](https://github.com/kshku/SnNetwork) | Socket and networking abstraction library |

## Contents

- **platform.h** — Compiler, OS, architecture, and endian detection
- **defines.h** — Utility macros (inline, assert, min/max, bit flags, alignment, stringify, byte arrays)
- **api_common.h** — Shared `SN_API_HELPER_EXPORT` / `SN_API_HELPER_IMPORT` macros
- **types.h** — Common callback type definitions (`SnMemoryAllocateFn`, `SnLockFn`, `SnTimeNowFn`, etc.)
- **utf8.h** — UTF-8 ↔ UTF-16 conversion functions (Windows: real conversion; other platforms: stubs)

## Usage

```c
#include <sncore/platform.h>
#include <sncore/defines.h>
#include <stdio.h>

int main(void) {
#if defined(SN_OS_LINUX)
    printf("Running on Linux\n");
#elif defined(SN_OS_WINDOWS)
    printf("Running on Windows\n");
#endif

    // Alignment helper
    uint64_t unaligned = 0x1003;
    uint64_t aligned = SN_GET_ALIGNED(unaligned, 8);
    printf("Aligned: %llu\n", (unsigned long long)aligned);  // 0x1008

    return 0;
}
```

## Adding to your project

```cmake
include(FetchContent)
FetchContent_Declare(sncore
    GIT_REPOSITORY https://github.com/kshku/SnCore.git
    GIT_TAG <tag>  # e.g., v0.1.0
)
FetchContent_MakeAvailable(sncore)

target_link_libraries(myapp PRIVATE sncore)
```

## Dependencies

- None. SnCore has no external dependencies.
