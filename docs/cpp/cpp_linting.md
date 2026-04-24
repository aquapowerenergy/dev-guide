# C++ Linting with cpplint

This document provides guidelines for setting up and using `cpplint.py`, our chosen linter for enforcing the AquaPower C++ Style Guide.

`cpplint` is a Python script that checks C++ files for compliance with the Google C++ Style Guide. Since our style guide is heavily based on Google's, `cpplint` is an excellent tool for automated style enforcement.

## 1. Installation

`cpplint.py` is a standalone Python script. You can download it directly or install it via `pip`.

### Option 1: Download the script directly

1.  Navigate to the official Google Styleguide GitHub repository: [https://github.com/google/styleguide](https://github.com/google/styleguide)
2.  Locate `cpplint/cpplint.py` and download it to a convenient location (e.g., in a `tools/` directory in your project root or globally in your `PATH`).

### Option 2: Install via pip (recommended for easier updates)

1.  Ensure you have Python and `pip` installed.
2.  Install `cpplint` from PyPI:
    ```bash
    pip install cpplint
    ```
    This will install `cpplint` as a command-line tool.

## 2. Basic Usage

Once installed, you can run `cpplint` from your terminal.

### Linting a single file

```bash
cpplint <path/to/your/file.cpp>
```

### Linting multiple files

```bash
cpplint <path/to/file1.cpp> <path/to/file2.h>
```

### Linting all C++ files in a directory (and subdirectories)

You can use find or similar tools to process multiple files:

```bash
find . -name "*.cpp" -o -name "*.h" | xargs cpplint
```

*   `find . -name "*.cpp" -o -name "*.h"`: Finds all .cpp and .h files in the current directory and its subdirectories.
*   `xargs cpplint`: Passes the list of found files to cpplint.

## 3. Configuring cpplint

cpplint can be configured to ignore certain checks or use a custom style.

### Ignoring specific checks

You can disable specific checks using the `--filter` option. For example, to ignore all readability/alt_tokens and whitespace/indent warnings:

```bash
cpplint --filter=-readability/alt_tokens,-whitespace/indent <file.cpp>
```

The filters are comma-separated and prefixed with `-` to disable. A `+` prefix enables (though by default all are enabled).

### Configuration File (CPPLINT.cfg)

For project-wide configuration, create a file named `CPPLINT.cfg` in the root of your repository (or any parent directory). cpplint will automatically detect and use this file.

A CPPLINT.cfg example:

```ini
# Maximum line length
linelength=80

# List of filters to apply (comma-separated, - to disable, + to enable)
# For example, to disable 'build/include_order' and 'runtime/references' checks:
filter=-build/include_order,-runtime/references

# Preferred include order (regex for your project's headers)
# For AquaPower, our own headers should be prioritized
# after standard libraries.
```

### Suppressing warnings in code

For very specific cases, you can suppress a warning directly in the code using a `NOLINT` comment:

```cpp
int some_variable;  // NOLINT(whitespace/indent) - Temporarily disable indent check for this line
```

*   You can also specify specific checks to disable, e.g., `NOLINT(whitespace/indent)`.
*   Use this sparingly, only when absolutely necessary, and always add a clear explanation.

## 4. Integration with IDEs (CLion)

For an improved development experience, integrate cpplint directly into your IDE.

### CLion Setup

CLion (and other JetBrains IDEs) can be configured to run external tools, including linters.

1.  Go to **File > Settings/Preferences > Tools > External Tools**.
2.  Click the **+** icon to add a new tool.
3.  Configure the tool:
    *   **Name:** `cpplint`
    *   **Description:** Runs cpplint on the current file
    *   **Program:** `cpplint` (or the full path to cpplint.py if installed manually, e.g., `/usr/local/bin/cpplint`)
    *   **Arguments:** `--filter=-whitespace/line_length,-whitespace/tab,<other filters if needed> $FilePath$`
        *   `$FilePath$` is a macro that CLion replaces with the current file's path.
        *   Adjust filters as per our CPPLINT.cfg or specific project needs.
    *   **Working directory:** `$ProjectFileDir$`
    *   Check **"Open console"**
    *   Optional: You can configure **"Output filters"** to make CLion parse the warnings more effectively (e.g., `$FILE_PATH$:$LINE_NUMBER$: $MESSAGE$`).
4.  Save the tool.
5.  **Assign a Shortcut (Optional):** You can assign a keyboard shortcut to run this tool under **Keymap > External Tools > cpplint**.

### Pre-commit Hooks

For stricter enforcement, consider setting up Git pre-commit hooks that run cpplint automatically before every commit. This ensures that no non-compliant code is committed to the repository.

Tools like [pre-commit](https://pre-commit.com/) (a framework for managing and maintaining multi-language pre-commit hooks) can simplify this:

1.  Install pre-commit: `pip install pre-commit`
2.  Create a `.pre-commit-config.yaml` in your repo root:
    ```yaml
    repos:
      - repo: https://github.com/cpplint/cpplint
        rev: '1.6.1'  # Use the latest version
        hooks:
          - id: cpplint
    ```
3.  Install the hook: `pre-commit install`

This setup will run cpplint on staged C++ files automatically before each commit.

## References

*   [Google Styleguide - cpplint](https://github.com/google/styleguide/tree/gh-pages/cpplint)
*   [Microsoft CppLinter Overview](https://docs.microsoft.com/en-us/cpp/code-quality/code-analysis-for-c-cpp-overview) (While not cpplint, good for general linter concepts)
