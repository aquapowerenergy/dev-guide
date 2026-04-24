# Git Style Guide

This document outlines the conventions and best practices for using Git within AquaPower projects. Adhering to these guidelines ensures a consistent, readable, and maintainable commit history and project structure.

## Naming Convention

### Repositories

All repositories should be named using **CamelCase**. This means each word starts with a capital letter and words are joined without spaces.
*   **Example:** `AquaPowerDevGuide`, `FlightControlSystem`, `GroundStationTelemetry`

### Branching

*   **Purpose:** Branches should be short, descriptive, and clearly indicate the purpose of the changes.
*   **Format:** We use the pattern `sistema/atividade/código`
    *   `sistema`: The high-level component or system being worked on (e.g., `PDA`, `avionics`, `ground-station`).
    *   `atividade`: The type of work (e.g., `feature`, `bug`, `refactor`, `doc`).
    *   `código`: A short, descriptive identifier or issue number related to the work (e.g., `Inst_10`, `new-sensor-integration`, `fix-telemetry-loss`).
*   **Examples:**
    *   `avionics/feature/bmp280-driver`
    *   `PDA/bug/calibration-issue-15`
    *   `ground-station/refactor/ui-components`
*   **Origin:** All new feature branches should typically branch off the `dev` branch (or `main` if a `dev` branch is not explicitly used for the project).
    *   `git checkout dev`
    *   `git checkout -b avionics/feature/new-sensor-test`

## Git Commit Messages

Clear, concise, and well-formatted commit messages are crucial for understanding project history.

### Principles

*   Use the **present tense** ("Add feature" not "Added feature").
*   Use the **imperative mood** ("Move cursor to..." not "Moves cursor to...").
*   Limit the first line (subject) to **72 characters or less**.
*   Reference issues and pull requests liberally after the first line.
*   Keep commits small and focused on a single logical change.

### Structure

A commit message should ideally be structured as follows:

```
type: Subject line (72 chars or less)

Optional body paragraph explaining more in detail.

  - Bullet points can be used here.
  - Elaborate on the "what" and "why" of the change.

References: #IssueID, PR#PullRequestID
```

### Types (Categories)

Consider starting the commit message with a type to categorize the change:

*   `feat`: (feature) A new feature or functionality.
*   `fix`: (bug fix) A bug fix.
*   `refactor`: A code change that neither fixes a bug nor adds a feature (e.g., restructuring code).
*   `docs`: Documentation only changes.
*   `test`: Adding missing tests or correcting existing tests.
*   `build`: Changes that affect the build system or external dependencies (e.g., gulp, broccoli, npm).
*   `ci`: Changes to our CI configuration files and scripts (e.g., GitHub Actions, Travis, Circle).
*   `perf`: A code change that improves performance.
*   `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semicolons, etc).
*   `chore`: Other changes that don't modify src or test files.

### Optional Emojis for Subject Line

While optional, emojis can provide a quick visual cue about the commit's nature.

*   ✨ `:sparkles:` when adding a new feature.
*   🐛 `:bug:` when fixing a bug.
*   ♻️ `:recycle:` when refactoring code.
*   📝 `:memo:` when writing docs.
*   🚀 `:rocket:` when deploying or releasing.
*   ⬆️ `:arrow_up:` when upgrading dependencies.
*   ⬇️ `:arrow_down:` when downgrading dependencies.
*   ✅ `:white_check_mark:` when adding tests.
*   🎨 `:art:` when improving the format/structure of the code.
*   🔥 `:fire:` when removing code or files.
*   💚 `:green_heart:` when fixing the CI build.

### Commit Example

```
feat: Add BME280 sensor data acquisition

This commit introduces the initial driver and acquisition logic for the BME280
sensor.

  - Reads temperature, pressure, and humidity.
  - Integrates with the existing sensor interface.
  - Includes basic error handling for sensor initialization.

References: #42, PR#55
```

## Versioning (Semantic Versioning)

We follow [Semantic Versioning 2.0.0](https://semver.org/) for tagging releases and managing project versions.

*   A version number takes the form `MAJOR.MINOR.PATCH`.
*   **MAJOR** version: Incremented for incompatible API changes.
*   **MINOR** version: Incremented for adding functionality in a backward-compatible manner.
*   **PATCH** version: Incremented for backward-compatible bug fixes.
*   Initial development is denoted by `0.y.z`, where anything may change at any time.

## Tips

### Authentication with GitHub

To interact with GitHub repositories, you have two main options:

#### Option 1: GitHub CLI (Recommended)

Use **GitHub CLI** for seamless authentication management:
*   [Install GitHub CLI](https://cli.github.com/)
*   Run: `gh auth login` and follow the interactive setup
*   Select your preferred protocol: **SSH** (recommended) or **HTTPS**
*   Verify: `gh auth status`

GitHub CLI automatically handles credentials and eliminates the need to repeatedly enter passwords.

#### Option 2: SSH Keys (Manual Setup)

Manually configure SSH keys for Git operations:
*   [Generating SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
*   [Adding your SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

#### Option 3: HTTPS with Personal Access Token

For HTTPS-based access:
*   [Create a Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
*   Use your PAT as the password when cloning or pushing to repositories
*   Note: PATs need to be managed and rotated for security

---
For a visual overview of version control best practices, refer to external resources on Git workflows.
