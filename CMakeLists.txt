## based on https://crascit.com/2016/04/09/using-ccache-with-cmake/

cmake_minimum_required(VERSION 3.4)

option(USE_CCACHE "" OFF)

if (USE_CCACHE)

  find_program(CCACHE_PROGRAM ccache)

  if(CCACHE_PROGRAM)
      # Set up wrapper scripts
      set(C_LAUNCHER   "${CCACHE_PROGRAM}")
      set(CXX_LAUNCHER "${CCACHE_PROGRAM}")
      configure_file(launch-c.in   launch-c)
      configure_file(launch-cxx.in launch-cxx)
      execute_process(COMMAND chmod a+rx
                      "${CMAKE_CURRENT_BINARY_DIR}/launch-c"
                      "${CMAKE_CURRENT_BINARY_DIR}/launch-cxx"
      )

      if(CMAKE_GENERATOR STREQUAL "Xcode")
          # Set Xcode project attributes to route compilation and linking
          # through our scripts
          set(CMAKE_XCODE_ATTRIBUTE_CC         "${CMAKE_CURRENT_BINARY_DIR}/launch-c" CACHE INTERNAL "")
          set(CMAKE_XCODE_ATTRIBUTE_CXX        "${CMAKE_CURRENT_BINARY_DIR}/launch-cxx" CACHE INTERNAL "")
          set(CMAKE_XCODE_ATTRIBUTE_LD         "${CMAKE_CURRENT_BINARY_DIR}/launch-c" CACHE INTERNAL "")
          set(CMAKE_XCODE_ATTRIBUTE_LDPLUSPLUS "${CMAKE_CURRENT_BINARY_DIR}/launch-cxx" CACHE INTERNAL "")
      else()
          # Support Unix Makefiles and Ninja
          set(CMAKE_C_COMPILER_LAUNCHER   "${CMAKE_CURRENT_BINARY_DIR}/launch-c" CACHE INTERNAL "")
          set(CMAKE_CXX_COMPILER_LAUNCHER "${CMAKE_CURRENT_BINARY_DIR}/launch-cxx" CACHE INTERNAL "")
      endif()

      message(STATUS "Using ccache: ${CCACHE_PROGRAM}")
  else()
      message(WARNING "Could not enable Ccache: could not find program")
  endif()

endif()
