# Development Best Practices

A collection of software development practices and philosophies focused on reducing human error through clear, consistent workflows.

Open source under the [MIT License](LICENSE).

---

## Table of Contents
1. [Language](#language)
2. [Guiding Principle](#guiding-principle-keep-it-clean-and-simple)
3. [Git Workflow](#git-workflow)
4. [Commit Message Conventions](#commit-message-conventions)
5. [AI-Assisted Development](#ai-assisted-development)

---

## Language

All project communication must be in **English** — this includes:

*   README and documentation
*   Commit messages and PR titles/descriptions
*   Code comments and inline documentation
*   Issue titles and comments

*   **Why?** English is the lingua franca of software development. Keeping everything in one language ensures the history is readable by any contributor or reviewer, regardless of background.

---

## Guiding Principle: Keep it Clean and Simple

Reduce complexity and increase clarity. A clean `main` branch, understandable commit history, and consistent processes lead to better software.

---

## Git Workflow

A workflow designed to maintain a clean and linear project history in the `main` branch.

### 1. Pull Request Requirements

Changes to `main` should go through a pull request. Direct commits to `main` create a messy history.

*   **One PR Per Feature Branch:** Each feature branch addresses a single, specific purpose and results in exactly one pull request.
*   **Why?** This maintains a clear history of what was changed and why.

### 2. Squash Merge Policy

Pull requests targeting the `main` branch benefit from squash merging. This condenses the feature's entire commit history into a single, meaningful commit on the `main` branch.

*   **Why?** Keeps the `main` branch history clean, readable, and focused on features and fixes rather than incremental work-in-progress commits.
*   **PR Number Recommendation:** Include the PR number in brackets at the end (e.g., `feat: Add user authentication (#42)`) for traceability between commits and pull requests.

### 3. Delete Head Branch on Merge

Always delete the feature branch as part of the merge command itself.

*   **How:** Pass `--delete-branch` to the `gh pr merge` command:
    ```
    gh pr merge <number> --squash --delete-branch --subject "feat: Your title (#42)"
    ```
*   **Why?** Makes branch cleanup an explicit, visible step rather than a hidden repository setting. Nothing is left to chance.

### 4. Pull Request Review Philosophy

Most changes can be self-reviewed and merged by the author. However, certain changes benefit from explicit stakeholder approval.

#### Standard PRs (Self-Review)

Most pull requests fall into this category.

*   **Examples:** Bug fixes, feature additions, refactoring, tests, documentation updates
*   **Approach:** Self-review thoroughly before merging.

#### Consider Stakeholder Review

Changes that modify interfaces or introduce breaking changes benefit from stakeholder input.

*   **Examples:**
    *   Breaking API changes that affect consumers (frontend, mobile apps, external clients)
    *   Integrating another system (e.g., connecting ML models to APIs)
    *   Modifying shared contracts or interfaces
*   **Approach:** Tag and get feedback from affected parties before merging.
*   **Why?** Ensures coordination when connecting systems and prevents breaking dependent services.

---

## Commit Message Conventions

Following [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) creates an explicit and readable commit history.

Prefix commit messages with a type:

*   **feat:** A new feature
*   **fix:** A bug fix
*   **docs:** Changes to documentation
*   **style:** Formatting, missing semi-colons, etc.; no production code change
*   **refactor:** Refactoring production code, e.g., renaming a variable
*   **test:** Adding missing tests, refactoring tests; no production code change
*   **chore:** Updating build tasks etc.; no production code change

**Example:** `feat: Add user authentication endpoint`

### Commit Message Body Guidelines

When adding a commit body (the detailed description after the subject line), keep it concise:

*   **Maximum 3 bullet points:** Limit commit bodies to 3 bullet points of description.
*   **Why?** This enforces clarity and prevents commits from becoming too large or unfocused. If you need more than 3 points, consider breaking the work into smaller, more atomic commits.
*   **Applies to all commits:** This guideline applies to merge commits, squash commits, and regular commits alike.

---

## AI-Assisted Development

AI tools (such as Claude, GitHub Copilot, ChatGPT, etc.) can significantly accelerate development when used thoughtfully.

### Development Workflow with AI

#### During Development (Feature Branch)

*   **AI-Assisted Commits:** Use AI to create commits during active development on feature branches.
*   **Iterate Freely:** Use AI to rapidly prototype, refactor, and experiment. The feature branch is a workspace for iteration.
*   **Rationale:** Maximizes development velocity while the code is still in progress and not yet integrated into the main codebase.

#### Before Merging (Pull Request Review)

*   **Manual Review Recommended:** Review and understand all AI-generated or AI-assisted code during the pull request review process before merging to `main`.
*   **Review Checklist:**
    *   Understand what the code does and how it works
    *   Verify it follows coding standards and best practices
    *   Check for potential security vulnerabilities
    *   Ensure it integrates properly with existing code
    *   Confirm tests are adequate and passing
*   **Rationale:** Ensures code quality, maintains security standards, and guarantees the developer understands and takes responsibility for the code entering the main branch.

### Commit Authorship

*   **Human Authorship:** Consider listing only human developers as commit authors.
*   **Example to avoid:**
    ```
    Co-Authored-By: Claude <noreply@anthropic.com>
    Co-Authored-By: GitHub Copilot <noreply@github.com>
    ```
*   **Rationale:** Commits reflect human authorship and responsibility. While AI is a helpful tool, the developer is ultimately responsible for all code committed to the repository.

---

*This document is a living standard. Suggestions for improvement can be made via pull requests to this repository.*
