# New Developer Onboarding Checklist

Welcome to AquaPower! This checklist will guide you through the initial setup and essential information to get you productive quickly. Please follow these steps in order.

## Phase 1: Initial Setup & Access

### 1. Account Creation & Access

*   [ ]  **GitHub:**
    *   [ ]  Create a GitHub account (if you don't have one).
    *   [ ]  Provide your GitHub username to your manager for organization invitation.
    *   [ ]  Accept the GitHub organization invitation.
    *   [ ]  **Install GitHub CLI:**
        *   [ ]  Download and install [GitHub CLI](https://cli.github.com/).
        *   [ ]  Run: `gh auth login` and follow the interactive prompts to authenticate your GitHub account.
        *   [ ]  When prompted for preferred protocol, select **HTTPS** for better security.
        *   [ ]  Verify authentication: `gh auth status`
*   [ ]  **ClickUp:**
    *   [ ]  Receive ClickUp invitation via email.
    *   [ ]  Join the AquaPower ClickUp workspace.
    *   [ ]  Familiarize yourself with the [ClickUp Workflow Guide](../tools/clickup_workflow.md).

### 2. Workstation Setup

*   [ ]  **Operating System:** Ensure your development machine has a suitable OS (Linux, macOS, or Windows with WSL2 recommended for C++).
*   [ ]  **Git:**
    *   [ ]  Install Git.
    *   [ ]  Configure your global Git settings:
        ```bash
        git config --global user.name "Your Name"
        git config --global user.email "your.email@aquapower.com"
        ```
*   [ ]  **Visual Studio Code (VS Code):**
    *   [ ]  Install VS Code.
    *   [ ]  Install essential VS Code extensions:
        *   PlatformIO IDE
        *   C/C++ Extension Pack (Microsoft)
        *   ESLint (for TypeScript/JavaScript)
        *   Prettier (for TypeScript/JavaScript)
        *   GitLens (highly recommended)
*   [ ]  **Python:**
    *   [ ]  Install Python (if not already present).
    *   [ ]  Install `pip`.
    *   [ ]  Install `cpplint`: `pip install cpplint`
    *   [ ]  Install `pre-commit`: `pip install pre-commit`

## Phase 2: Understanding Our Practices

### 3. Codebase & Version Control

*   [ ]  **Clone Core Repositories:** Clone the main project repositories you'll be working on. Start with this `AquaPowerDevGuide` repository.
*   [ ]  **Read Git Guides:**
    *   [ ]  [Git Style Guide](../git/git_style_guide.md) (Naming, Commit Messages, Versioning)
    *   [ ]  [Git Flow Workflow](../git/git_flow.md) (Branching strategy)
    *   [ ]  [Git Commands Cheatsheet](../git/git_commands_cheatsheet.md) (Quick reference)
*   [ ]  **Install Pre-commit Hooks:**
    *   [ ]  Navigate to the root of a cloned repository (e.g., `AquaPowerDevGuide`).
    *   [ ]  Run: `pre-commit install` (This will enforce linting/formatting rules before committing).

### 4. Language-Specific Style Guides

*   [ ]  **C++ & C:**
    *   [ ]  Read the [C++ Style Guide](../cpp/cpp_style_guide.md).
    *   [ ]  Understand [C++ Linting with cpplint](../cpp/cpp_linting.md) setup.
    *   [ ]  Familiarize yourself with Doxygen for documentation.
*   [ ]  **TypeScript (Web):**
    *   [ ]  Read the [Web (TypeScript) Style Guide](../web/typescript_style_guide.md).
    *   [ ]  Understand the use of ESLint and Prettier.

### 5. Tools & Workflow

*   [ ]  **Review ClickUp Workflow:** Re-read the [ClickUp Workflow Guide](../tools/clickup_workflow.md) and understand how tasks are created, updated, and linked to GitHub.
*   [ ]  **PlatformIO:**
    *   [ ]  Read the [PlatformIO Guide](../tools/platformio_guide.md).
    *   [ ]  Create a sample PlatformIO project and build it.
    *   [ ]  Understand how to manage libraries locally.
*   [ ]  **Arduino Framework:**
    *   [ ]  Read the [Arduino Framework Guide](../tools/arduino_framework.md).
    *   [ ]  Understand when it's appropriate for prototyping.

## Phase 3: Getting Started

### 6. First Contribution

*   [ ]  **Find a Small Task:** Work with your mentor/manager to identify a small, introductory task in ClickUp.
*   [ ]  **Open a Branch:** Create a new branch following our [naming conventions](../git/git_style_guide.md#branching).
*   [ ]  **Make Changes & Commit:** Implement the changes, ensuring compliance with style guides.
*   [ ]  **Open a Pull Request:** Create a PR, linking it to your ClickUp task, and ensure it follows our [Pull Request Template](.github/PULL_REQUEST_TEMPLATE.md).
*   [ ]  **Participate in Code Review:** Discuss your changes and address any feedback.

## Phase 4: Ongoing Learning & Resources

### 7. Important Resources

*   [ ]  **AquaPower Dev Guide Repository (this one):** Your primary resource for all best practices.
*   [ ]  **Project-Specific Documentation:** Locate and review documentation for your specific project.
*   [ ]  **Mentorship:** Don't hesitate to ask your mentor or other team members questions!
*   [ ]  **External References:**
    *   [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
    *   [Semantic Versioning 2.0.0](https://semver.org/)
    *   [Doxygen Manual](https://www.doxygen.nl/manual/index.html)

---

**Congratulations on completing your onboarding! We're excited to have you on the AquaPower team!**
