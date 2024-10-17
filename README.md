# Valgrind Exercise

## Standard install via command-line
```bash
# Configure the project and generate a native build system:
  # Must re-run this command whenever any CMakeLists.txt file has been changed.
  cmake -S ./ -B build/
# To build with debugging information, do:
  cmake -S ./ -B build/ -D CMAKE_BUILD_TYPE=Debug
# Compile and build the project:
  # rebuild only files that are modified since the last build
  cmake --build build/
  # or rebuild everything from scracth
  cmake --build build/ --clean-first
  # to see verbose output, do:
  cmake --build build/ --verbose
# Run program:
  ./build/app/shell-app
# Clean
  cmake --build build/ --target clean
# Clean and start over:
  rm -rf build/
```

## Valgrind Behavior with Static Linking

### What happens when the executable is linked statically?

When the executable is linked statically, the resulting binary includes all the necessary code to run the program, incorporating libraries and dependencies directly into the application. This leads to several important outcomes:

1. **Inclusion of Library Code**: All library functions and their implementations become part of the executable. While this results in a larger binary size, it simplifies deployment since there are no external dependencies.

### Does Valgrind still detect those same bugs?

Yes, Valgrind still detects memory errors (such as uninitialized memory usage, memory leaks, etc.) in statically linked executables. 

### Why or why not?

The reason is that Valgrind operates at the binary level, analyzing the executable and its runtime behavior regardless of how the libraries were linked (statically or dynamically). 

- **Memory Management**: Valgrind checks the memory management across the entire executable, regardless of whether the functions belong to the main codebase or are part of statically linked libraries.
- **Code Behavior**: The actual execution flow and memory access patterns remain unchanged, allowing Valgrind to identify issues like uninitialized values or memory leaks that may occur in any part of the executable.

### Summary

In summary, linking statically does not prevent Valgrind from detecting memory-related bugs. Valgrind analyzes the complete binary, ensuring that any issues present in the code or linked libraries are reported during execution