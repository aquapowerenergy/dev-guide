# Contributing to AquaPower Projects

We welcome and appreciate contributions to our projects! By following these guidelines, you help us maintain code quality, ensure consistency, and streamline the development process.

## How to Contribute

1.  **Read the Guidelines:** Please familiarize yourself with our detailed style guides and development practices located in the [`docs/`](/docs) directory.
2.  **Open an Issue:** Before starting any significant work, please open an [issue](#opening-issues) to discuss your proposed changes or bug fix. This helps prevent duplicated effort and ensures alignment with project goals.
3.  **Create a Feature Branch:** Always work on a new branch for your changes. Follow our [Git Branching Convention](#git-conventions) for naming.
4.  **Make Your Changes:** Implement your changes, ensuring they adhere to the relevant [Style Guides](#style-guides).
5.  **Test Your Changes:** If applicable, add or update unit tests to cover your changes. Ensure all existing tests pass.
6.  **Commit Your Changes:** Write clear and concise [Git Commit Messages](#git-conventions).
7.  **Open a Pull Request:** Submit a [Pull Request](#pull-request-guidelines) against the `main` branch of the original repository.

## <a name="style-guides"></a> Style Guides

To ensure consistency across our codebase, please refer to the following specific style guides:

*   **[Git Style Guide](docs/git/git_style_guide.md)**: Naming conventions, commit messages, and workflow.
*   **[C++ Style Guide](docs/cpp/cpp_style_guide.md)**: C++ specific coding standards, naming, and formatting.
*   **[Web (TypeScript) Style Guide](docs/web/typescript_style_guide.md)**: Guidelines for our web development projects.

## <a name="git-conventions"></a> Git Conventions

We follow specific conventions for Git branching and commit messages. Please review the [Git Style Guide](docs/git/git_style_guide.md) for full details.

### Branching

*   **Naming:** Branches should be short, descriptive, and follow the pattern `sistema/atividade/código`.
    *   **Good:** `ARARA/bug/Inst_10`, `instrumentation/feature/new-sensor-integration`
    *   **Bad:** `login_fix`, `my_changes`
*   All feature branches should branch off `dev` (or `main` if `dev` isn't used).

### Commit Messages

*   **Format:** Use the present tense and imperative mood. Limit the first line to 72 characters.
    *   **Good:** "Add function for GY-92 data acquisition"
    *   **Bad:** "Added function for GY-92 data acquisition"
*   **Types:** Consider starting with a type or emoji (e.g., `feat:`, `fix:`, `refactor:`, `docs:`, 🐛, ✨, 📝)
*   Reference related issues and pull requests.

## <a name="opening-issues"></a> Opening Issues

When opening an issue, please use the appropriate template to provide all necessary information.

*   **[Bug Report](.github/ISSUE_TEMPLATE/bug_report.md)**: For reporting bugs and unexpected behavior.
*   **[Feature Request](.github/ISSUE_TEMPLATE/feature_request.md)**: For suggesting new features or improvements.

## <a name="pull-request-guidelines"></a> Pull Request Guidelines

When submitting a pull request, please ensure:

*   You've used the [Pull Request Template](.github/PULL_REQUEST_TEMPLATE.md).
*   Your branch is up-to-date with the `main` branch.
*   Your changes adhere to all relevant [Style Guides](#style-guides).
*   Tests have been added/updated and pass.
*   Documentation has been updated if necessary.
*   You've filled out the checklist in the PR template.

## Code Review

All pull requests require a code review from another team member before being merged. Be prepared to discuss your changes and address any feedback.

---

**Thank you for contributing to AquaPower!**
