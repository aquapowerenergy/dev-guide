# ClickUp Workflow

ClickUp is our primary tool for project management and task tracking. This guide outlines how we use ClickUp to organize, prioritize, and manage our development efforts.

## 1. Hierarchy

Our ClickUp workspace is organized hierarchically to ensure clarity and manageability:

*   **Workspace:** AquaPower
*   **Spaces:** Represent major departments or project groups (e.g., `Arara`, `Ground Station`, `Structures`, `Software`).
*   **Folders:** Used to group related projects or major initiatives within a Space.
*   **Lists:** Represent individual projects or specific workstreams within a Folder.
*   **Tasks:** Individual units of work within a List. This is where most developer interaction happens.
*   **Subtasks:** Used for breaking down a task into smaller, manageable steps.

## 2. Task Management Principles

### Objective and "Small" Tasks

*   Tasks should be **objective** and **small** enough to be completed within a reasonable timeframe (ideally a few hours to a few days).
*   If a task is too large, break it down into subtasks or create multiple smaller tasks.
*   Each task should represent a clear deliverable or outcome.

### Assignees

*   Every task should have a clear **assignee**. This ensures accountability.
*   If a task requires multiple people, consider assigning it to one primary person and adding others as "Watchers" or creating subtasks for each individual.

### Due Dates

*   Assign **due dates** to tasks to help with prioritization and deadline management.
*   Communicate proactively if a due date cannot be met.

### Priorities

*   Use ClickUp's priority levels (Urgent, High, Normal, Low) to indicate the importance of a task.
    *   **Urgent:** Immediate attention required, blocking critical path.
    *   **High:** Important, should be worked on soon.
    *   **Normal:** Standard priority, regular work.
    *   **Low:** Less critical, can be picked up if higher priority tasks are complete.

## 3. Creating and Updating Tasks

### Creating a New Task

When creating a new task:

1.  **Title:** Provide a clear, concise title that summarizes the task.
2.  **Description:**
    *   Clearly describe the **"what"** (what needs to be done) and the **"why"** (the purpose or problem it solves).
    *   Include any relevant links (e.g., to GitHub issues, documentation, design documents).
    *   Use checklists within the description for internal sub-steps that don't warrant separate subtasks.
3.  **Assignee:** Assign the task to yourself or the responsible team member.
4.  **Due Date:** Set a realistic due date.
5.  **Priority:** Set the appropriate priority.
6.  **Tags (Optional):** Use tags to categorize tasks (e.g., `firmware`, `frontend`, `testing`).

### Updating Task Status

Keep your task statuses updated to reflect your current progress. Common statuses include:

*   **Open/To Do:** Task is assigned and ready to start.
*   **In Progress:** Currently working on the task.
*   **In Review:** Task is complete and awaiting review (e.g., a Pull Request has been opened).
*   **Blocked:** Progress is halted due to an external factor (e.g., awaiting hardware, waiting for another team's input). Always provide a comment explaining the blockage.
*   **Closed/Done:** Task is completed.

### Comments

*   Use comments to provide updates, ask questions, or share relevant information about the task.
*   Whenever you change a task's status (especially to "Blocked"), add a comment explaining why.
*   Mention (`@`) team members to get their attention on specific comments.

## 4. Linking GitHub Pull Requests to ClickUp Tasks

For seamless integration, link your GitHub Pull Requests (PRs) directly to your ClickUp tasks.

1.  When you create a PR, include the ClickUp task ID in the PR title or description (e.g., `[TASK-123] feat: Implement new telemetry parser`).
2.  ClickUp's GitHub integration will automatically link the PR to the task, updating the task's status (e.g., to "In Review") when the PR is opened.
3.  Conversely, you can link the GitHub issue/PR from within the ClickUp task using the "Add Link" option.

This integration provides traceability from code changes back to the original task, and vice-versa.

## 5. Daily Stand-ups / Weekly Syncs

*   Be prepared to provide a brief update on your ClickUp tasks during daily stand-ups or weekly sync meetings.
*   Focus on what you completed, what you plan to do, and any blockers you're facing.
