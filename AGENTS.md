# Repository Guidelines

## Project Structure & Module Organization
- `pdf_viewer/` holds the core C++/Qt application, with `pdf_viewer/touchui/` for touch UI and `pdf_viewer/synctex/` for SyncTeX helpers.
- `mupdf/`, `zlib/`, and `fzf/` are vendored dependencies; avoid refactoring or reformatting them unless required.
- `resources/`, `icons/`, `pdf_viewer/shaders/`, and `resources.qrc` contain assets and Qt resource definitions.
- `scripts/`, `android/`, and `windows_runtime/` cover tooling and platform-specific resources; `tutorial/` and `tutorial.pdf` are end-user docs.

## Build, Test, and Development Commands
- `./build_linux.sh` builds MuPDF and the app via `qmake`, producing `build/sioyek` plus config files. Set `QMAKE=/path/to/qmake-qt6` if needed.
- `MAKE_PARALLEL=8 ./build_mac.sh` builds and packages `build/sioyek.app` and `sioyek-release-mac.zip`.
- `build_windows.bat` (run in a Visual Studio Developer Command Prompt) produces `sioyek-release-windows/`.
- The development branch expects Qt 6.7/6.8; confirm with `qmake --version`.

## Coding Style & Naming Conventions
- C++17 with Qt; follow the existing 4-space indent and same-line braces.
- Naming mirrors current code: `snake_case` for functions/locals and `PascalCase` for types/classes; keep Qt `Q...` conventions intact.
- No top-level formatter config; keep diffs focused and do not reformat vendored code.

## Testing Guidelines
- There is no dedicated automated test suite for the main app; verify changes by running the built binary and exercising affected features.
- Vendored dependencies include their own tests (e.g., under `mupdf/` or `zlib/`), but they are not part of the usual workflow.

## Commit & Pull Request Guidelines
- Recent commits use short, imperative summaries and occasional Conventional-Commit-style prefixes like `feat(scrollbar): ...`; follow that pattern when helpful.
- PRs should describe the change, list target platform(s), and include reproduction or verification steps; add screenshots or recordings for UI changes.
- Call out config updates (`prefs*.config`, `keys*.config`) and any edits to third-party code.
