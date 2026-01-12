# Sioyek PDF Viewer

## Project Overview

Sioyek is a cross-platform PDF viewer built with C++ and the Qt framework. It is designed with a focus on textbooks and research papers, offering features like smart jump, table of contents search, and highlighting. The project uses `mupdf` for PDF rendering and includes a custom UI built with Qt.

## Building and Running

The project uses `qmake` and `make` for building. There are separate build scripts for each platform:

### Linux

To build on Linux, run the following command:

```bash
./build_linux.sh
```

This will create an AppImage in the root directory.

### Windows

To build on Windows, open the Visual Studio Developer Command Prompt and run:

```bash
build_windows.bat
```

This will create a `sioyek-release-windows` directory with the compiled application.

### macOS

To build on macOS, run:

```bash
./build_mac.sh
```

This will create a `sioyek.dmg` file in the `build` directory.

## Development Conventions

*   The code is written in C++17.
*   The project uses the Qt framework for its UI and application logic.
*   The project has a dependency on `mupdf` for PDF rendering.
*   The build system is based on `qmake` and `make`.
*   There are separate build scripts for each platform (`build_linux.sh`, `build_windows.bat`, `build_mac.sh`).
*   The application's configuration is handled through `prefs.config` and `keys.config` files. User-specific configurations are stored in `prefs_user.config` and `keys_user.config`.
