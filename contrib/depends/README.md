All of the following are executed from within this directory. 

### Usage

To build dependencies for the current arch+OS, from this working directory:

```bash
make
```

To build for another arch/OS:

```bash
make HOST=host-platform-triplet
```

For example:

```bash
make HOST=x86_64-w64-mingw32 -j4
```

A toolchain will be generated that's suitable for plugging into Monero's
cmake. In the above example, a dir named x86_64-w64-mingw32 will be
created. To use it for Monero, from the top of the Monero source tree:

```bash
mkdir build
cd build
cmake -DCMAKE_TOOLCHAIN_FILE=$PWD/../contrib/depends/x86_64-w64-mingw32/share/toolchain.cmake ..
```
The following optional flags can also be used to configure the build.

- `-D STATIC=ON` to create a statically linked build
- `-D CMAKE_BUILD_TYPE=Release` to build without debug symbols or `Debug` to build with them

Common `host-platform-triplets` for cross compilation are:

- `i686-w64-mingw32` for Win32
- `x86_64-w64-mingw32` for Win64
- `x86_64-apple-darwin` for MacOSX x86_64
- `arm-linux-gnueabihf` for Linux ARM 32 bit
- `aarch64-linux-gnu` for Linux ARM 64 bit
- `riscv64-linux-gnu` for Linux RISCV 64 bit

No other options are needed, the paths are automatically configured.

Next, run make inside the build directory. The -j option can be used
to set the number of jobs that should be used. 

Dependency Options:
The following can be set when running make: make FOO=bar

```
SOURCES_PATH: downloaded sources will be placed here
BASE_CACHE: built packages will be placed here
FALLBACK_DOWNLOAD_PATH: If a source file can't be fetched, try here before giving up
DEBUG: disable some optimizations and enable more runtime checking
HOST_ID_SALT: Optional salt to use when generating host package ids
BUILD_ID_SALT: Optional salt to use when generating build package ids
```

Additional targets:

```
download: run 'make download' to fetch all sources without building them
download-osx: run 'make download-osx' to fetch all sources needed for osx builds
download-win: run 'make download-win' to fetch all sources needed for win builds
download-linux: run 'make download-linux' to fetch all sources needed for linux builds
```

#Mingw builds

Building for 32/64bit mingw requires switching alternatives to a posix mode

```bash
update-alternatives --set x86_64-w64-mingw32-g++ x86_64-w64-mingw32-g++-posix
update-alternatives --set x86_64-w64-mingw32-gcc x86_64-w64-mingw32-gcc-posix
```

### Other documentation

- [description.md](description.md): General description of the depends system
- [packages.md](packages.md): Steps for adding packages

