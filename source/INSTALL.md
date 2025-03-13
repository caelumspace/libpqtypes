## LIBPQTYPES INSTALLATION GUIDE

*) UNIX & WINDOWS BUILDS USING CMAKE

For quick builds, run the below:

```
mkdir build && cd buildcmake ..cmake --build .sudo cmake --install .
```

To specify a custom installation directory:

```
cmake .. -DCMAKE_INSTALL_PREFIX=/custom/pathcmake --build .sudo cmake --install .
```

To build a static library, add `-DBUILD_STATIC=ON`:

```
cmake .. -DBUILD_STATIC=ONcmake --build .
```

To enable thread safety:

```
cmake .. -DENABLE_THREAD_SAFETY=ONcmake --build .
```

The default installation prefix is `/usr/local`, so the library and headers will be installed in:

- `/usr/local/include/libpqtypes.h`
  
- `/usr/local/lib/libpqtypes.so`
  
- `/usr/local/lib/libpqtypes.a` (if built statically)
  

To dynamically link with `libpqtypes`, pass `-lpqtypes` to the linker.

*) WINDOWS BUILDS USING CMAKE

For MSVC builds, use:

```
mkdir build && cd buildcmake .. -G "Visual Studio 17 2022"cmake --build . --config Release
```

To install:

```
cmake --install .
```

Ensure you have PostgreSQL installed and its `include` and `lib` directories accessible.

*) ADDITIONAL OPTIONS

- **Clean Build**

```
rm -rf build && mkdir build && cd buildcmake ..cmake --build .
```

- **Uninstall**

```
sudo cmake --build . --target uninstall
```

This replaces the previous `Makefile`-based approach with a modern CMake build system, ensuring compatibility across different platforms and compilers.