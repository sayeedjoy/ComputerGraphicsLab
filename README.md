# OpenGL_Course (macOS + CLion)

Minimal OpenGL starter project using:
- GLFW for window/context creation
- GLAD for OpenGL function loading
- CMake for build configuration

When run successfully, it opens an `800x600` window with a red background.

## Prerequisites (macOS)

1. Install Xcode Command Line Tools:
```bash
xcode-select --install
```
2. Install Homebrew (if not already installed):  
https://brew.sh
3. Install dependencies:
```bash
brew install cmake glfw
```

## Open In CLion

1. Open CLion.
2. Select **Open** and choose this project folder (`untitled`).
3. Wait for CMake to configure.

## If CLion Cannot Find `glfw3`

This project uses:
```cmake
find_package(glfw3 CONFIG REQUIRED)
```

If configuration fails, add Homebrew's prefix to CMake options in CLion:

1. Go to **Settings/Preferences > Build, Execution, Deployment > CMake**.
2. In **CMake options**, add:
```bash
-DCMAKE_PREFIX_PATH=$(brew --prefix)
```
OR 
```
-DCMAKE_PREFIX_PATH=/opt/homebrew;/opt/homebrew/opt/glfw
```
3. Reload CMake.

For Apple Silicon, Homebrew is usually under `/opt/homebrew`.  
For Intel Macs, it is usually under `/usr/local`.

## Build And Run In CLion

1. Ensure the run configuration target is `untitled`.
2. Build with the hammer icon (or `Cmd+F9`).
3. Run with the play button (or `Ctrl+R`).

## Project Files

- `main.cpp`: creates window, initializes GLAD, renders red clear color.
- `glad.c`: GLAD loader source.
- `include/`: GLAD/KHR headers.
- `CMakeLists.txt`: build + link setup (GLFW and macOS frameworks).
