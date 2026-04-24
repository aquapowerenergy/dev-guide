# Arduino Framework Guide for Rapid Prototyping

The Arduino framework is an invaluable tool at AquaPower for rapid prototyping, quick proof-of-concept development, and initial hardware testing. This guide covers its usage and best practices within our workflow.

## 1. When to Use Arduino

Use the Arduino framework for:

*   **Rapid Prototyping:** Quickly validate sensor interfaces, basic control logic, or communication protocols.
*   **Initial Hardware Bring-up:** Get new hardware components running and performing basic functions quickly.
*   **Proof-of-Concept:** Test core algorithms or ideas without getting bogged down in complex embedded system setup.
*   **Educational / Learning:** It's an excellent platform for quickly getting new team members familiar with embedded development.

**Avoid using Arduino for:**

*   **Flight-critical systems:** Production flight software requires more robust development practices, real-time operating systems (RTOS), and extensive testing.
*   **High-performance computing:** For intensive data processing or complex control loops, dedicated microcontrollers with bare-metal or RTOS environments are preferred.
*   **Long-term, maintainable codebase:** While good for initial stages, transitioning to a more structured C++/C environment (e.g., PlatformIO with custom build systems) is recommended for production code.

## 2. Development Environment

You can use either the **Arduino IDE** or **PlatformIO** for Arduino development.

### Arduino IDE (Recommended for absolute beginners)

The official Arduino IDE is simple to use for basic sketches.

*   **Download:** Get the latest version from the [Arduino website](https://www.arduino.cc/en/software).
*   **Board Support:** Install necessary board packages (e.g., ESP32, ESP8266, SAMD boards) via `Tools > Board > Board Manager...`.
*   **Library Management:** Install libraries via `Sketch > Include Library > Manage Libraries...`.

### PlatformIO (Recommended for experienced users and integration)

PlatformIO offers a more professional environment with better project management, library handling, and integration with VS Code. It is our preferred environment when moving beyond basic sketches.

*   Refer to the [PlatformIO Guide](platformio_guide.md) for detailed setup and usage.

## 3. Project Structure & Best Practices

When using the Arduino framework, even for prototyping, try to maintain some best practices:

### File Organization

*   **`.ino` file:** Contains your main `setup()` and `loop()` functions. Keep this file relatively clean by abstracting logic into separate `.h` and `.cpp` files.
*   **Header Files (`.h`):** Declare functions, classes, and global variables.
*   **Source Files (`.cpp`):** Implement the functions declared in header files.
*   **`lib/` folder (PlatformIO specific):** For local libraries or custom modules. See PlatformIO guide for details.

### Example Arduino Sketch Structure

```
MySensorProto/
├── MySensorProto.ino
├── SensorDriver.h
├── SensorDriver.cpp
├── Utils.h
├── Utils.cpp
├── platformio.ini (if using PlatformIO)
```

### Coding Guidelines (Even for Prototypes)

*   **Descriptive Names:** Use meaningful names for variables, functions, and classes.
*   **Comments:** Add comments to explain complex logic or non-obvious choices.
*   **Modular Code:** Break down large `loop()` functions into smaller, more focused functions.
*   **Avoid Global Variables:** Minimize the use of global variables. Pass data via function parameters where possible.
*   **Error Handling (Basic):** Implement basic error checks, especially for sensor initialization or communication. Use `Serial.println()` for debugging.

## 4. Library Management

### Global vs. Local Libraries

*   **Arduino IDE:** Libraries are typically installed globally and are available to all sketches.
*   **PlatformIO:** Strongly encourages **local library management**.
    *   Libraries specified in `platformio.ini` are downloaded and managed per project.
    *   For custom libraries or modules, place them in the project's `lib/` directory. This ensures project self-containment and avoids conflicts.

### Example `platformio.ini` for local libraries

```ini
[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino
lib_deps =
    # Public library from PlatformIO registry
    adafruit/Adafruit Unified Sensor@^1.1.4
    adafruit/Adafruit BME280 Library@^2.1.2

# Custom local library (e.g., in your project's 'lib/MyCustomSensor' folder)
# lib_extra_dirs = lib
# lib_ldf_mode = deep+
```

## 5. Debugging

*   **Serial.println():** The most common debugging tool in Arduino. Use it extensively to print variable values, status messages, and trace execution flow.
*   **Serial Plotter:** For visualizing sensor data or other numerical values over time (Tools > Serial Plotter in Arduino IDE).
*   **PlatformIO Debugger:** PlatformIO, especially with boards that support JTAG/SWD, offers more advanced debugging capabilities. Refer to the [PlatformIO Guide](platformio_guide.md) for setting up hardware debugging.

By following these guidelines, you can effectively leverage the Arduino framework for rapid development while maintaining a level of structure that facilitates eventual transition to production systems.
