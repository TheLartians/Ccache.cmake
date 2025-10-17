[![Actions Status](https://github.com/TheLartians/Ccache.cmake/workflows/CI/badge.svg)](https://github.com/TheLartians/Ccache.cmake/actions)

# Ccache.cmake

A simple, Xcode compatible _Ccache_ integration for _CMake_, based on [this](https://crascit.com/2016/04/09/using-ccache-with-cmake) article by Craig Scott.
 
## About

[Ccache](https://ccache.dev) is a compiler cache that can drastically improve build times for C and C++ projects.
This script makes it easy to configure a CMake project to use Ccache by adding the configuration option `USE_CCACHE` which will active Ccache support when enabled.
Build-specific environmental variables can be set with the `CCACHE_OPTIONS` configuration parameter.
It is currently compatible with _Makefile_, _Ninja_ and _Xcode_ generators.
Example usage:

```bash
cmake . -DUSE_CCACHE=YES -DCCACHE_OPTIONS="CCACHE_CPP2=true;CCACHE_SLOPPINESS=clang_index_store"
```

## How to integrate

### Using [CPM.cmake](https://github.com/TheLartians/CPM) (recommended)

Run the following from the project's root directory to add CPM to your project.

```bash
mkdir -p cmake
wget -O cmake/CPM.cmake https://github.com/cpm-cmake/CPM.cmake/releases/latest/download/get_cpm.cmake
```

Add the following lines to the project's `CMakeLists.txt` after calling `project(...)`.

```CMake
include(cmake/CPM.cmake)

CPMAddPackage("gh:TheLartians/Ccache.cmake@1.2.5")
```

### Using git submodules (not suited for libraries)

Run the following from the project's root directory.

```bash
git submodule add https://github.com/TheLartians/Ccache.cmake 
```

In add the following lines to the project's `CMakeLists.txt` after calling `project(...)`.

```CMake
add_subdirectory(Ccache.cmake)
```

## Dependencies

Ccache.cmake requires CMake and [_Ccache_](https://ccache.dev).
