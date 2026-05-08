# C++ Style Guide

This document outlines the C++ coding standards and best practices for all
AquaPower projects. Adhering to this guide ensures consistency, readability,
and maintainability across our C++ codebase.

Our primary reference for these guidelines is the
[Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html),
with specific adaptations and emphases noted below.

## 1. Naming Conventions

Consistent naming makes code easier to read and understand.

### File Names

*   **Header Files:** Use `.h` extension.
*   **Implementation Files:** Use `.cpp` extension.
    *   *Note: Google's guide recommends `.cc`, but `.cpp` is the established
        convention for Arduino/PlatformIO projects at AquaPower. Either is
        acceptable; prefer `.cpp` for consistency within the project.*
*   **General:** All file names should be lowercase. Use underscores (`_`) to
    separate words. Avoid hyphens.
    *   **Good:** `my_class.h`, `sensor_data_processor.cpp`
    *   **Bad:** `MyClass.hpp`, `sensor-data-processor.cpp`

### Type Names (Classes, Structs, Enums, Type Aliases)

*   **Format:** Start with a capital letter, then mixed case (PascalCase). No
    underscores.
    *   **Good:** `MyClass`, `SensorDataPacket`, `TelemetryState`
    *   **Bad:** `my_class`, `sensor_data_packet`

### Variable Names

*   **General:** Use descriptive names. Avoid single-letter variable names
    unless the context is extremely clear (e.g., loop counters `i`, `j`).
*   **Local Variables and Function Parameters:** Lowercase, with underscores
    between words (snake_case).
    *   **Good:** `int sensor_value;`, `double altitude_meters;`
    *   **Bad:** `int sVal;`, `double altM;`
*   **Class Member Variables (Non-Static and Static):** Lowercase snake_case
    with a **trailing underscore**. This is the Google C++ Style Guide
    standard. Do **not** use `m_` or `g_` prefixes.
    *   **Good:** `int sensor_id_;`, `float current_temperature_;`
    *   **Bad:** `int m_sensorId;`, `float m_currentTemperature;`, `int sensor_id`
*   **Struct Data Members:** Lowercase snake_case, **without** the trailing
    underscore (structs are for plain data, no hidden state).
    *   **Good:** `int sensor_id;`, `float temperature;`
    *   **Bad:** `int sensor_id_;`, `int m_sensorId;`
*   **Global Variables:** Avoid global variables. When absolutely necessary,
    use descriptive snake_case names and document them thoroughly.
    *   **Good:** `int system_status;`
*   **Constant Variables (`constexpr` or `const` with static storage):**
    Start with `k` prefix, followed by mixed case (CamelCase).
    *   **Good:** `const int kMaxRetries = 3;`, `constexpr double kPi = 3.14159;`
    *   **Bad:** `MAX_RETRIES`, `pi`, `k_max_retries`
    *   *Note: For `const` local variables (automatic storage duration), the
        `k` prefix is optional; plain snake_case is also acceptable.*

### Function Names

*   **General Functions and Methods:** Start with a capital letter, then mixed
    case (PascalCase).
    *   **Good:** `CalculateChecksum()`, `ProcessSensorData()`, `InitHardware()`
    *   **Bad:** `calculate_checksum()`, `processsensordata()`
*   **Accessors and Mutators (getters/setters):** May use snake_case to mirror
    the member variable they correspond to (omitting the trailing underscore).
    *   **Good:** `int sensor_id() const;`, `void set_sensor_id(int id);`
    *   *Note: Either PascalCase or snake_case is acceptable for accessors, but
        be consistent within a class.*

### Enumerator Names

*   **Format:** Enumerators should be named like constants — `k` prefix
    followed by mixed case (CamelCase). **Do not** use ALL_CAPS for
    enumerators.
    *   **Good:**
        ```cpp
        enum class TelemetryState {
          kIdle,
          kTransmitting,
          kError,
        };
        ```
    *   **Bad:** `TELEMETRY_STATE_IDLE`, `IDLE`

### Macro Names

*   **Format:** All uppercase, with underscores between words.
    *   **Good:** `#define MAX_BUFFER_SIZE 1024`
    *   **Bad:** `#define MaxBufferSize`
    *   *Note: Prefer `const` variables, `enum class`, or `constexpr` over
        macros wherever possible. Macros should be a last resort.*

## 2. Documentation and Comments <a name="documentation"></a>

Every non-obvious function, class, and complex block of code **must** be
documented. We aim for clarity and maintainability.

### Class Comments

Every non-obvious class or struct declaration should have an accompanying
comment that describes its purpose, how it should be used, and any important
considerations.

We use **Doxygen standards** for class documentation. CLion and other IDEs
should automatically register and autocomplete Doxygen comments.

```cpp
/**
 * @class SensorDataProcessor
 * @brief Handles the acquisition, filtering, and processing of raw sensor data.
 *
 * This class is responsible for interacting with various sensor peripherals,
 * applying calibrated filters, and providing processed data in a standardized
 * format. It operates in a non-blocking manner and manages internal state for
 * each sensor.
 *
 * @note This class assumes sensors are initialized externally.
 */
class SensorDataProcessor {
 public:
  // ...
 private:
  int sensor_id_;
  float current_temperature_;
};
```

### Function Comments

Every non-obvious function declaration (and definition if separate) should
have a comment describing what it does, its parameters, return value, and any
side effects.

Use Doxygen standards for function documentation:

```cpp
/**
 * @brief Reads a single data sample from the specified sensor.
 *
 * @param sensor_id The unique identifier of the sensor to read from.
 * @return A SensorDataPacket containing the latest reading, or an invalid
 *         packet on error.
 * @retval Valid SensorDataPacket if successful.
 * @retval Invalid SensorDataPacket (e.g., with error flag set) if reading
 *         fails.
 */
SensorDataPacket ReadSensorSample(int sensor_id);
```

### In-line Comments

Use comments to explain complex logic, non-obvious decisions, or to mark areas
for improvement (`TODO:`).

```cpp
// Check if the current velocity exceeds the safe threshold for descent.
if (current_velocity > kMaxDescentVelocity) {
  LogWarning("Descent velocity exceeded safe limits!");
  // TODO: Implement emergency braking sequence.
}
```

## 3. Formatting

Consistent code formatting is crucial for readability. We adhere to the Google
C++ Style Guide's formatting rules.

### Indentation

*   Use **2 spaces** for indentation. Never use tabs.

### Brace Placement

*   Non-empty blocks: Opening brace on the same line as the statement, closing
    brace on its own line.
    ```cpp
    if (condition) {
      // ...
    } else {
      // ...
    }
    ```
*   Empty blocks: Can be `{}`, or `void Foo() {}`.

### Line Length

*   Maximum line length is **80 characters**. Break long lines thoughtfully.

### Pointers and References

*   The asterisk or ampersand is part of the **type**, not the variable name.
    *   **Good:** `const string* pstr;`, `const string& str;`
    *   **Bad:** `const string *pstr;`, `const string &str;`

### Horizontal Whitespace

*   Use spaces around operators (`=`, `+`, `==`, etc.).
*   No spaces inside parentheses, brackets, or before commas.
*   One space after keywords (e.g., `if`, `for`, `while`).

## 4. Linting

We use cpplint as our primary linter to enforce these style guidelines
automatically. See the [C++ Linting Guide](cpp_linting.md) for setup and
usage instructions.

## 5. C++ Specific Practices

### Header Guards

All header files **must** use `#define` guards to prevent multiple inclusion.
The format should be `<PROJECT>_<PATH>_<FILE>_H_` based on the file's full
path within the project's source tree.

```cpp
// For a file at src/sensors/bmp280.h in an "aqua" project:
#ifndef AQUA_SENSORS_BMP280_H_
#define AQUA_SENSORS_BMP280_H_

// ... header content ...

#endif  // AQUA_SENSORS_BMP280_H_
```

### Includes

*   Order of includes: Related header, C system headers, C++ system headers,
    other library headers, your project's headers. Group them and separate with
    blank lines.
*   Use angle brackets for system headers (`#include <iostream>`) and double
    quotes for your project's headers (`#include "my_header.h"`).

### Integer Types

*   Use `int` for general-purpose integers.
*   When a specific width is required, use exact-width types from `<stdint.h>`:
    `int8_t`, `uint8_t`, `int16_t`, `uint16_t`, `int32_t`, `uint32_t`,
    `int64_t`, `uint64_t`.
*   Avoid `short`, `long`, and `long long` — their widths are
    platform-dependent.
*   Do **not** use unsigned types merely to assert a value is non-negative;
    use assertions instead.

### Scoping

*   Use namespaces to avoid name collisions.
*   Avoid `using namespace std;` in header files. In `.cpp` files, limit
    `using` declarations to function scope or specific aliases.

### Classes and Structs

*   Prefer **classes** for objects with behavior and internal state.
*   Use **structs** for plain old data (POD) structures with no invariants.
*   Declare member variables `private` or `protected`. Provide `public` methods
    for access.

### Error Handling

*   Use exceptions for truly exceptional conditions where a function cannot
    proceed.
*   For expected errors or failures, return error codes or use
    `std::optional`/`std::expected` (C++17/C++23).

### Memory Management

*   Prefer smart pointers (`std::unique_ptr`, `std::shared_ptr`) over raw
    pointers for managing dynamic memory.
*   Avoid raw `new` and `delete` when smart pointers can be used.

## 6. Quick Reference: Naming Summary

| Entity                         | Convention          | Example                         |
|--------------------------------|---------------------|---------------------------------|
| Files                          | `snake_case`        | `sensor_driver.cpp`             |
| Types (class/struct/enum)      | `PascalCase`        | `SensorDataPacket`              |
| Local variables / parameters   | `snake_case`        | `int sensor_value;`             |
| Class member variables         | `snake_case_`       | `int sensor_id_;`               |
| Struct data members            | `snake_case`        | `int sensor_id;`                |
| Constants (`constexpr`/`const`)| `kCamelCase`        | `const int kMaxRetries = 3;`    |
| Functions / methods            | `PascalCase`        | `ProcessSensorData()`           |
| Accessors / mutators           | `snake_case`        | `sensor_id()`, `set_sensor_id()`|
| Enumerators                    | `kCamelCase`        | `kIdle`, `kTransmitting`        |
| Macros                         | `UPPER_SNAKE_CASE`  | `MAX_BUFFER_SIZE`               |
| Namespaces                     | `snake_case`        | `namespace aqua_sensors`        |

## References

*   [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
*   [Doxygen Manual](https://www.doxygen.nl/manual/index.html)
