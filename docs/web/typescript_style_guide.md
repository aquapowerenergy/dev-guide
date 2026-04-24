# Web (TypeScript) Style Guide

This document outlines the coding standards and best practices for TypeScript development at AquaPower, primarily for our web-based applications and ground-station interfaces.

Our goal is to ensure consistency, readability, and maintainability across all TypeScript projects. We generally adhere to established industry best practices for TypeScript and JavaScript.

## 1. Naming Conventions

### File Names

*   **Format:** Kebab-case (`kebab-case`). Use hyphens to separate words.
    *   **Good:** `user-dashboard.component.ts`, `data-service.ts`, `utility-functions.ts`
    *   **Bad:** `UserDashboardComponent.ts`, `dataService.ts`, `utility_functions.ts`

### Type Names (Interfaces, Classes, Enums, Type Aliases)

*   **Format:** PascalCase (`PascalCase`).
    *   **Good:** `TelemetryData`, `UserComponent`, `ApiResponse`
    *   **Bad:** `telemetryData`, `user_component`

### Variable Names

*   **Format:** camelCase (`camelCase`).
    *   **Good:** `const userName: string;`, `let isActive: boolean;`, `const telemetryPacket: TelemetryData;`
    *   **Bad:** `user_name`, `is_active`

### Function Names

*   **Format:** camelCase (`camelCase`).
    *   **Good:** `fetchData()`, `processTelemetry()`, `updateUI()`
    *   **Bad:** `fetch_data()`, `processtelemetry()`

### Constants (Global/Module-level)

*   **Format:** UPPER_SNAKE_CASE (`UPPER_SNAKE_CASE`). For `const` variables that are truly immutable and known at compile time.
    *   **Good:** `const API_BASE_URL = 'https://api.example.com';`, `const MAX_RETRIES = 5;`
    *   **Bad:** `apiBaseUrl`, `maxRetries`

## 2. Formatting

We enforce consistent formatting using automated tools.

### Indentation

*   Use **2 spaces** for indentation. **Never use tabs.**

### Semicolons

*   Always use semicolons at the end of statements.

### Line Length

*   Strive for a maximum line length of **100-120 characters**. Break long lines logically for readability.

### Quotes

*   Use **single quotes** for string literals. Backticks for template literals.
    *   **Good:** `'hello'`, `` `Hello, ${name}` ``
    *   **Bad:** `"hello"`

### Braces

*   Opening brace on the same line as the statement.
    ```typescript
    if (condition) {
      // ...
    } else {
      // ...
    }

    class MyClass {
      constructor() {
        // ...
      }
    }
    ```

## 3. Type Safety

Leverage TypeScript's type system to its fullest.

*   **Explicit Types:** Explicitly declare types for variables, function parameters, and return values. Avoid `any` unless absolutely necessary and justified.
    *   **Good:** `function greet(name: string): string { ... }`
    *   **Bad:** `function greet(name) { ... } // Implicit any`
*   **Interfaces & Types:** Use interfaces or type aliases for defining object shapes and complex types.
*   **Enums:** Use `enum` for sets of related constants, or prefer union types of string literals for more flexibility.

## 4. Comments and Documentation

Clear and concise comments improve code understanding.

*   **JSDoc:** Use JSDoc-style comments for functions, classes, and complex types to describe their purpose, parameters, and return values. This aids in generating documentation and IDE intellisense.
    ```typescript
    /**
     * @brief Fetches telemetry data from the API.
     * @param {string} endpoint The API endpoint to fetch from.
     * @param {number} timeoutMs The maximum time to wait for the request in milliseconds.
     * @returns {Promise<TelemetryData[]>} A promise that resolves with an array of telemetry data.
     */
    async function getTelemetryData(endpoint: string, timeoutMs: number): Promise<TelemetryData[]> {
        // ...
    }
    ```
*   **In-line Comments:** Use sparingly to explain complex logic or non-obvious choices.

## 5. Tooling

We use ESLint and Prettier for automated code quality and formatting.

### ESLint

*   **Purpose:** Lints TypeScript code for potential errors, stylistic issues, and adherence to best practices.
*   **Configuration:** Our `.eslintrc.js` in the project root defines the specific rules.
*   **Usage:** Integrate with your IDE, or run via `npm run lint`.

### Prettier

*   **Purpose:** An opinionated code formatter that ensures consistent code style by automatically reformatting your code.
*   **Configuration:** Our `.prettierrc.js` in the project root defines formatting rules (e.g., single quotes, semicolon usage, line length).
*   **Usage:** Integrate with your IDE (e.g., "Format on Save"), or run via `npm run format`.

## 6. Project Structure

*   Organize code into logical modules or features.
*   Keep components small and focused on a single responsibility.
*   Use `index.ts` files for barrel exports to simplify imports.

## 7. Error Handling

*   Use `try-catch` blocks for synchronous error handling.
*   Handle asynchronous errors with `.catch()` for Promises or `try-catch` with `await`.
*   Provide meaningful error messages and log errors appropriately.

## 8. Modularity and Reusability

*   Design functions and components to be reusable and independent.
*   Avoid global state where possible; pass data as parameters.
*   Break down large files or functions into smaller, manageable units.
