[![Actions Status](https://github.com/TheLartians/Ccache.cmake/workflows/CI/badge.svg)](https://github.com/TheLartians/Ccache.cmake/actions)

# Ccache.cmake

A simple Ccache integration for CMake.
 
## About

Ccache.cmake makes it easy to use [_Ccache_](https://ccache.dev) inside a _CMake_ project.
It adds an addition configuration option `USE_CCACHE` that, when enabled, configures CMake to compile sources using the ccache compiler cache.
It is compatible with _Makefile_, _Ninja_ and _Xcode_ targets.

After [integrating](#how-to-integrate) _Ccache.cmake_, you can configure your project to compile with _Ccache_ with the following command.

```bash
cmake . -DUSE_CCACHE=YES
```

## How to integrate

### Using [CPM.cmake](https://github.com/TheLartians/CPM) (recomended)

Run the following from the project's root directory to add CPM to your project.

```bash
mkdir -p cmake
wget -O cmake/CPM.cmake https://raw.githubusercontent.com/TheLartians/CPM/master/cmake/CPM.cmake
```

Add the following lines to the project's `CMakeLists.txt` after calling `project(...)`.

```CMake
include(cmake/CPM.cmake)

CPMAddPackage(
  NAME Ccache.cmake
  GITHUB_REPOSITORY TheLartians/Ccache.cmake
  VERSION 1.1
)
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

_Ccache.cmake_ requires _CMake_ and [_ccache_](https://ccache.dev).
