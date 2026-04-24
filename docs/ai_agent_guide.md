# AI Agent Protocol for AquaPower Development Standards

This document outlines the protocol for AI agents interacting with AquaPower's development environment, particularly concerning adherence to our style guides, workflows, and documentation standards. The goal is to ensure that AI-generated or assisted contributions seamlessly integrate with human-generated code and processes.

## 1. General Directive

AI agents are expected to adhere to all established AquaPower development standards as outlined in this `AquaPowerDevGuide` repository, acting as a direct extension of human development principles.

## 2. Style Guide Adherence

AI agents **MUST** strictly follow all relevant style guides:

*   **[Git Style Guide](git/git_style_guide.md):**
    *   **Branch Naming:** Adhere to the `sistema/atividade/código` convention.
    *   **Commit Messages:** Use imperative mood, present tense, and include appropriate types/emojis. Ensure the first line is under 72 characters.
    *   **Versioning:** Understand and apply Semantic Versioning for any proposed version bumps or tags.
*   **[C++ Style Guide](cpp/cpp_style_guide.md):**
    *   **Naming Conventions:** Apply CamelCase for types/functions, snake_case for local variables, `m_` for member variables, `k` for constants, and UPPER_SNAKE_CASE for macros.
    *   **Formatting:** Use 2-space indentation, correct brace placement, 80-character line limit, and pointer/reference formatting.
    *   **Linting:** Understand `cpplint` rules and ensure generated code passes `cpplint` checks.
*   **[Web (TypeScript) Style Guide](web/typescript_style_guide.md):**
    *   **Naming Conventions:** Apply PascalCase for types, camelCase for variables/functions, kebab-case for filenames, and UPPER_SNAKE_CASE for module-level constants.
    *   **Formatting:** Use 2-space indentation, semicolons, single quotes, and a 100-120 character line limit.
    *   **Linting/Formatting:** Generate code that would pass ESLint and Prettier checks.

## 3. Documentation Standards

AI agents **MUST** generate and maintain documentation according to our standards:

*   **Class & Function Comments:** Provide Doxygen-style comments for all non-trivial classes and functions, explaining purpose, parameters, return values, and any side effects.
*   **In-line Comments:** Use comments to explain complex logic or non-obvious design choices.
*   **`README.md` & Project Documentation:** When modifying or generating new modules/projects, ensure that `README.md` files and any other relevant project documentation are created or updated to reflect the changes.

## 4. Workflow Integration

AI agents **MUST** integrate with our established development workflows:

*   **Task Management (ClickUp):**
    *   Understand the concept of a ClickUp task as a unit of work.
    *   When performing a task (e.g., generating code for a feature), the AI should associate its work with a specific ClickUp task ID, ideally by including it in Git commit messages and Pull Request descriptions.
    *   An AI should be able to update task statuses (e.g., from "Open" to "In Progress" or "In Review" upon PR creation) if integrated with the ClickUp API.
*   **Git Flow:**
    *   **Branching:** Create new branches from `dev` following the `sistema/atividade/código` convention for new features or bug fixes.
    *   **Pull Requests:** When submitting code, create a Pull Request against the `dev` branch, adhering to the [Pull Request Template](.github/PULL_REQUEST_TEMPLATE.md).
    *   **Code Review:** Be capable of understanding and responding to code review feedback (if applicable to the AI's capabilities) by iterating on the code or clarifying intent.

## 5. Tooling Awareness

AI agents **MUST** be aware of and respect our development tools:

*   **PlatformIO:** Understand PlatformIO's project structure, `platformio.ini` configuration, and local library management for embedded projects.
*   **Arduino Framework:** Understand when the Arduino framework is appropriate for rapid prototyping versus production code.
*   **Linters/Formatters:** Assume `cpplint`, ESLint, and Prettier will be run and generate code that passes their checks.

## 6. Interaction & Clarification

*   **Clarity:** AI-generated outputs (code, documentation, commit messages) should be as clear and unambiguous as possible.
*   **Questioning:** If a request from a human is ambiguous or contradicts established guidelines, the AI agent should seek clarification rather than proceeding with a potentially incorrect interpretation.
*   **Self-Correction:** AI agents should be capable of (or provide suggestions for) self-correction based on linter warnings, test failures, or explicit human feedback.

---

By adhering to this protocol, AI agents will significantly enhance our development capabilities while maintaining the high standards and collaborative environment critical to AquaPower's success.
