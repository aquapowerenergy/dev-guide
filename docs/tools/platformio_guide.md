# PlatformIO Guide

PlatformIO is our recommended ecosystem for embedded development, offering a powerful, cross-platform build system and IDE integration (primarily with VS Code). This guide covers its setup, project structure, and best practices at AquaPower.

## 1. Why PlatformIO?

PlatformIO provides several advantages over traditional IDEs for embedded development:

*   **Cross-Platform:** Works seamlessly on Windows, macOS, and Linux.
*   **Unified Build System:** Supports numerous development platforms (e.g., Espressif, STM32, Arduino, Teensy) and frameworks (Arduino, ESP-IDF, STM32Cube).
*   **Intelligent Code Completion:** Excellent intellisense, linting, and refactoring with VS Code.
*   **Robust Library Management:** Easy installation and management of project-specific libraries.
*   **Integrated Debugging:** Supports hardware debuggers (JTAG/SWD) for many platforms.
*   **Test Integration:** Built-in unit testing framework.

## 2. Installation and Setup

### VS Code Extension

1.  **Install VS Code:** If you don't have it, download and install [Visual Studio Code](https://code.visualstudio.com/).
2.  **Install PlatformIO IDE Extension:**
    *   Open VS Code.
    *   Go to the Extensions view (Ctrl+Shift+X or Cmd+Shift+X).
    *   Search for "PlatformIO IDE" and click "Install".
    *   VS Code will then guide you through installing the PlatformIO Core.

## 3. Project Structure

PlatformIO creates a standardized project structure:

```
MyPlatformIOProject/
├── .pio/                    # PlatformIO internal build environment
├── .vscode/                 # VS Code workspace settings
├── include/                 # Custom header files
├── lib/                     # Private libraries/modules for this project
│   └── MyCustomSensor/      # Example: a custom library for a sensor
│       ├── MyCustomSensor.h
│       └── MyCustomSensor.cpp
├── src/                     # Source files (main code)
│   └── main.cpp
├── test/                    # Unit tests
├── platformio.ini           # Project configuration file (VERY IMPORTANT)
├── .gitignore               # Git ignore file
└── README.md
```

### Key Folders Explained

*   **`src/`**: This is where your main application code (`.cpp`, `.c`, `.h`, `.ino` files) resides. For Arduino framework projects, your primary sketch file (e.g., `main.cpp` or `main.ino`) should be here.
*   **`include/`**: For header files that are *part of your application* but not intended to be a standalone library.
*   **`lib/`**: This is crucial for **local library management**. Any custom drivers, utility functions, or reusable modules specific to *this project* should be placed here as subfolders, structured as a PlatformIO library.
    *   **Best Practice:** Save libraries locally in `lib/` for self-contained projects, avoiding global conflicts.

## 4. `platformio.ini` - The Project Configuration File

This file defines your project's build environment, board, framework, libraries, and more.

### Basic `platformio.ini` Example

```ini
[env:esp32dev]          ; Environment name, descriptive and unique
platform = espressif32  ; Hardware platform (e.g., espressif32, ststm32)
board = esp32dev        ; Specific board (e.g., esp32dev, nucleo_f401re)
framework = arduino     ; Development framework (e.g., arduino, espidf, stm32cube)
build_flags =           ; Compiler flags
    -DDEBUG_MODE=1
lib_deps =              ; Project-specific libraries from PlatformIO Registry
    adafruit/Adafruit Unified Sensor@^1.1.4
    adafruit/Adafruit BME280 Library@^2.1.2
upload_port = /dev/ttyUSB0 ; Specify upload port (optional)
monitor_speed = 115200  ; Serial monitor baud rate
```

### Key Options

*   **`platform`**: Defines the chip vendor/family.
*   **`board`**: Specifies the exact development board.
*   **`framework`**: The software framework used (e.g., Arduino, ESP-IDF, Zephyr).
*   **`build_flags`**: Custom flags passed to the compiler (e.g., `#define` macros, optimization levels).
*   **`lib_deps`**: List of libraries to be downloaded and used for this project.
    *   Can be from the PlatformIO Registry (e.g., `author/library_name@^version`).
    *   Can be a local path (e.g., `file://../some_lib_folder`).
*   **`lib_extra_dirs`**: If you have custom libraries outside the `lib/` folder, you can specify their directories here. However, placing them directly in `lib/` is preferred.
*   **`upload_port`**: The serial port for uploading firmware.
*   **`monitor_speed`**: Baud rate for the serial monitor.

## 5. Library Management

PlatformIO's library manager is a powerful feature:

*   **Project-Local Libraries:** `lib_deps` in `platformio.ini` automatically downloads and uses libraries only for that specific project. This avoids version conflicts between projects.
*   **Custom Local Libraries:** For libraries you write yourself or don't want to publish, place them in the project's `lib/` folder as a sub-directory. PlatformIO will automatically detect and compile them.
    *   Example: If you have `lib/MySensorDriver/MySensorDriver.h` and `lib/MySensorDriver/MySensorDriver.cpp`, you simply `#include <MySensorDriver.h>` in your source code.

## 6. Building, Uploading, and Monitoring

PlatformIO integrates seamlessly into VS Code via the PlatformIO sidebar or command palette (Ctrl+Shift+P / Cmd+Shift+P).

*   **Build:** PlatformIO: Build (or the "Build" icon in the PlatformIO toolbar).
*   **Upload:** PlatformIO: Upload (or the "Upload" icon).
*   **Monitor:** PlatformIO: Serial Monitor (or the "Plug" icon).
*   **Build & Upload:** PlatformIO: Upload and Monitor

## 7. Debugging (Hardware Debugger)

PlatformIO supports hardware debugging (e.g., with J-Link, ST-Link, ESP-Prog) for many platforms.

### Basic Debug Setup in `platformio.ini`

```ini
[env:nucleo_f401re]
platform = ststm32
board = nucleo_f401re
framework = arduino
debug_tool = stlink          ; Specify your debug probe (e.g., stlink, jlink, esp-prog)
debug_port = /dev/ttyUSB0    ; Optional: port if multiple probes are connected
```

### Starting a Debug Session

1.  Build your project in "debug" mode (usually PlatformIO: Build in Debug Mode).
2.  Go to the "Run and Debug" view in VS Code (Ctrl+Shift+D or Cmd+Shift+D).
3.  Select the appropriate "PlatformIO Debug" configuration and click the "Start Debugging" button.

## 8. Unit Testing

PlatformIO has a built-in unit testing solution.

1.  Create Test Files: Place your test files (e.g., `test_main.cpp`) in the `test/` directory.
2.  Run Tests: Use PlatformIO: Test from the command palette or the PlatformIO toolbar.

## 9. C/C++ Linter Integration

PlatformIO, through VS Code, automatically provides C/C++ linting via clang-tidy and clang-format. Ensure these are configured to match our C++ Style Guide.

*   **clang-format:** Use a `.clang-format` file in your project root to define automatic code formatting rules.
*   **clang-tidy:** Provides more in-depth code analysis and warnings.

By leveraging PlatformIO, we can maintain a consistent, efficient, and robust embedded development workflow across all AquaPower projects.
