# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Sioyek is a cross-platform PDF viewer built with C++17 and Qt, designed for textbooks and research papers. It uses MuPDF for PDF rendering and OpenGL for display.

## Build Commands

**Linux:**
```bash
./build_linux.sh
# Set QMAKE=/path/to/qmake-qt6 if needed
# Output: build/sioyek
```

**macOS:**
```bash
MAKE_PARALLEL=8 ./build_mac.sh
# Output: build/sioyek.app
```

**Windows:** (Visual Studio Developer Command Prompt)
```bash
build_windows.bat
# Output: sioyek-release-windows/
```

**Qt Version:** Development branch requires Qt 6.7 or 6.8. Verify with `qmake --version`.

## Testing

There is no automated test suite. Verify changes by building the binary and manually testing affected features.

## Architecture

### Core Components

| Component | Files | Purpose |
|-----------|-------|---------|
| MainWidget | main_widget.h/cpp | Central orchestrator, handles UI and command dispatch |
| Document | document.h/cpp | PDF document model, annotations, marks, bookmarks |
| DocumentView | document_view.h/cpp | View state, navigation, viewport management |
| PdfViewOpenGLWidget | pdf_view_opengl_widget.h/cpp | OpenGL rendering, page layout |
| PdfRenderer | pdf_renderer.h/cpp | MuPDF integration |
| InputHandler | input.h/cpp | Keyboard/mouse/command processing |
| DatabaseManager | database.h/cpp | SQLite persistence |
| ConfigManager | config.h/cpp | Settings management |

### Directory Structure

- `pdf_viewer/` - Core application source
- `pdf_viewer/touchui/` - Touch UI components (QML + C++)
- `pdf_viewer/synctex/` - SyncTeX parser for LaTeX integration
- `pdf_viewer/shaders/` - OpenGL fragment/vertex shaders
- `mupdf/`, `zlib/`, `fzf/` - Vendored dependencies (do not reformat)
- `scripts/` - Python utility scripts

### Data Flow

```
User Input → InputHandler → CommandManager → MainWidget/DocumentView
    → Document → PdfRenderer + OpenGL → DatabaseManager (persist)
```

### Coordinate Systems

The codebase uses multiple coordinate systems: Document coordinates, Absolute coordinates, Normalized Window coordinates, and Window coordinates. See `coordinates.h/cpp`.

### Configuration Files

- `prefs.config` / `keys.config` - Default settings
- `prefs_user.config` / `keys_user.config` - User overrides

## Coding Conventions

- C++17 with Qt framework
- 4-space indentation, same-line braces
- `snake_case` for functions/locals, `PascalCase` for types/classes
- Preserve Qt `Q...` naming conventions
- No top-level formatter; keep diffs focused
- Do not reformat vendored code (mupdf, zlib, fzf)

## Commit Style

Use short imperative summaries with optional Conventional Commit prefixes:
```
feat(scrollbar): add customizable scrollbar styling
fix(render): correct page alignment issue
```

## PR Guidelines

- Describe the change and list target platform(s)
- Include reproduction/verification steps
- Add screenshots for UI changes
- Note any config file updates (prefs*.config, keys*.config)
- Call out any edits to third-party code
