# XDFBrowser

A GUI application for viewing and editing [XDF (Extensible Data Format)](https://github.com/sccn/xdf) files. XDF is a multi-modal, multi-rate time series format used in the [Lab Streaming Layer](https://labstreaminglayer.org/) ecosystem.

Pre-built Windows binaries are available from the [Actions tab](../../actions) (select the latest successful run on `master` and download the artifact).

## Features

- Browse all chunks in an XDF file (file headers, stream headers, samples, clock offsets, boundaries, stream footers)
- Inspect and edit the text content of header and footer chunks
- Memory-efficient: defaults to a 50 MB working set regardless of file size, loading sample data on demand

## Building

**Requirements:**
- CMake 3.16+
- Qt 6.3+ (Widgets module)
- A C++11-capable compiler (MSVC 2019+, GCC, Clang)

```bash
cmake -S . -B build -DQt6_DIR=<path/to/Qt6/lib/cmake/Qt6>
cmake --build build --config Release
cmake --install build --config Release --prefix install
```

On Windows, deploy the Qt runtime after installing:
```bash
windeployqt --release install/XDFBrowser.exe
```

The `install/` directory will then contain a self-contained, redistributable build.

## CI

GitHub Actions builds a Windows x64 package on every push to `master` and on `v*` tags using Qt 6.8 LTS. See [`.github/workflows/build.yml`](.github/workflows/build.yml).
