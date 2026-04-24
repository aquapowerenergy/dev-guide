# C++ Style Guide

This document outlines the C++ coding standards and best practices for all AquaPower projects. Adhering to this guide ensures consistency, readability, and maintainability across our C++ codebase.

Our primary reference for these guidelines is the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html), with specific adaptations and emphases noted below.

## 1. Naming Conventions

Consistent naming makes code easier to read and understand.

### File Names

*   **Header Files:** Use `.h` extension.
*   **Implementation Files:** Use `.cpp` extension.
*   **General:** All file names should be lowercase and can use underscores (`_`) if necessary. Avoid hyphens.
    *   **Good:** `my_class.h`, `sensor_data_processor.cpp`
    *   **Bad:** `MyClass.hpp`, `sensor-data-processor.cpp`

### Type Names (Classes, Structs, Enums, Type Aliases)

*   **Format:** Start with a capital letter, then mixed case (CamelCase). No underscores.
    *   **Good:** `MyClass`, `SensorDataPacket`, `TelemetryState`
    *   **Bad:** `my_class`, `sensor_data_packet`

### Variable Names

*   **General:** Use descriptive names. Avoid single-letter variable names unless the context is extremely clear (e.g., loop counters `i`, `j`).
*   **Local Variables:** Lowercase, with underscores between words (snake_case).
    *   **Good:** `int sensor_value;`, `double altitude_meters;`
    *   **Bad:** `int sVal;`, `double altM;`
*   **Member Variables (Non-Static, Non-Const):** Start with `m_` prefix, followed by mixed case (CamelCase).
    *   **Good:** `int m_sensorId;`, `float m_currentTemperature;`
    *   **Bad:** `sensorId_`, `currentTemperature`
*   **Global Variables:** Start with `g_` prefix, followed by mixed case (CamelCase). Generally, avoid global variables.
    *   **Good:** `int g_systemStatus;`
    *   **Bad:** `systemStatus`
*   **Constant Variables (`const`):** Start with `k` prefix, followed by mixed case (CamelCase).
    *   **Good:** `const int kMaxRetries = 3;`, `const double kPi = 3.14159;`
    *   **Bad:** `MAX_RETRIES`, `pi`

### Function Names

*   **Format:** Start with a capital letter, then mixed case (CamelCase).
    *   **Good:** `CalculateChecksum()`, `ProcessSensorData()`, `InitHardware()`
    *   **Bad:** `calculate_checksum()`, `processsensordata()`

### Macro Names

*   **Format:** All uppercase, with underscores between words.
    *   **Good:** `#define MAX_BUFFER_SIZE 1024`
    *   **Bad:** `#define MaxBufferSize`
    *   *Note: Prefer `const` variables, `enum`, or `constexpr` over macros where possible.*

## 2. Documentation and Comments <a name="documentation"></a>

Every non-obvious function, class, and complex block of code **must** be documented. We aim for clarity and maintainability.

### Class Comments

Every non-obvious class or struct declaration should have an accompanying comment that describes its purpose, how it should be used, and any important considerations.

We use **Doxygen standards** for class documentation. CLion and other IDEs should automatically register and autocomplete Doxygen comments.

```cpp
/**
 * @class SensorDataProcessor
 * @brief Handles the acquisition, filtering, and processing of raw sensor data.
 *
 * This class is responsible for interacting with various sensor peripherals,
 * applying calibrated filters, and providing processed data in a standardized format.
 * It operates in a non-blocking manner and manages internal state for each sensor.
 *
 * @note This class assumes sensors are initialized externally.
 */
class SensorDataProcessor {
public:
    // ...
};
```

### Function Comments

Every non-obvious function declaration (and definition if separate) should have a comment describing what it does, its parameters, return value, and any side effects.

Use Doxygen standards for function documentation:

```cpp
/**
 * @brief Reads a single data sample from the specified sensor.
 *
 * @param sensorId The unique identifier of the sensor to read from.
 * @return A SensorDataPacket containing the latest reading, or an invalid packet on error.
 * @retval Valid SensorDataPacket if successful.
 * @retval Invalid SensorDataPacket (e.g., with error flag set) if reading fails.
 */
SensorDataPacket ReadSensorSample(int sensorId);
```

### In-line Comments

Use comments to explain complex logic, non-obvious decisions, or to mark areas for improvement (TODO:).

```cpp
// Check if the current velocity exceeds the safe threshold for descent.
if (currentVelocity > kMaxDescentVelocity) {
    LogWarning("Descent velocity exceeded safe limits!");
    // TODO: Implement emergency braking sequence.
}
```

## 3. Formatting

Consistent code formatting is crucial for readability. We adhere to the Google C++ Style Guide's formatting rules.

### Indentation

*   Use 2 spaces for indentation. Never use tabs.

### Brace Placement

*   Non-empty blocks: Opening brace on the same line as the statement, closing brace on its own line.
    ```cpp
    if (condition) {
      // ...
    } else {
      // ...
    }
    ```
*   Empty blocks: Can be `{}`, or `void Foo() {}`.

### Line Length

*   Maximum line length is 80 characters. Break long lines thoughtfully.

### Pointers and References

*   The asterisk or ampersand is part of the type, not the variable name.
    *   Good: `const string* pstr;`, `const string& str;`
    *   Bad: `const string *pstr;`, `const string &str;`

### Horizontal Whitespace

*   Use spaces around operators (`=`, `+`, `==`, etc.).
*   No spaces inside parentheses, brackets, or before commas.
*   One space after keywords (e.g., `if`, `for`, `while`).

## 4. Linting

We use cpplint as our primary linter to enforce these style guidelines automatically. See the [C++ Linting Guide](cpp_linting.md) for setup and usage instructions.

## 5. C++ Specific Practices

### Includes

*   Order of includes: Related header, C system headers, C++ system headers, other library headers, your project's headers. Group them and separate with blank lines.
*   Use angle brackets for system headers (`#include <iostream>`) and double quotes for your project's headers (`#include "my_header.h"`).
*   Use include guards in all header files (`#ifndef`, `#define`, `#endif`).

### Scoping

*   Use namespaces to avoid name collisions.
*   Avoid using `namespace std;` in header files. In `.cpp` files, limit using namespace to function scope or specific aliases.

### Classes and Structs

*   Prefer classes for objects with behavior and internal state. Use structs for plain old data (POD) structures.
*   Declare member variables private or protected. Provide public methods for access.

### Error Handling

*   Use exceptions for truly exceptional conditions where a function cannot proceed.
*   For expected errors or failures, return error codes or use `std::optional`/`std::expected` (C++17/C++23).

### Memory Management

*   Prefer smart pointers (`std::unique_ptr`, `std::shared_ptr`) over raw pointers for managing dynamic memory.
*   Avoid raw `new` and `delete` when smart pointers can be used.

## References

*   [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
*   [Doxygen Manual](https://www.doxygen.nl/manual/index.html)
