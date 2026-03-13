# Development Best Practices

A collection of software development practices and philosophies focused on reducing human error through clear, consistent workflows.

This guide is written primarily for **AI coding assistants** (Claude, GitHub Copilot, ChatGPT, etc.) to follow when contributing to a project. Human developers are equally welcome to adopt these conventions.

Open source under the [MIT License](LICENSE).

---

## Table of Contents
1. [Language](#language)
2. [Default Branch Naming](#default-branch-naming)
3. [Guiding Principle](#guiding-principle-keep-it-clean-and-simple)
4. [Git Workflow](#git-workflow)
5. [Commit Message Conventions](#commit-message-conventions)
6. [AI-Assisted Development](#ai-assisted-development)

---

## Language

All project communication must be in **English** — this includes:

*   README and documentation
*   Commit messages and PR titles/descriptions
*   Code comments and inline documentation
*   Issue titles and comments

*   **Why?** English is the lingua franca of software development. Keeping everything in one language ensures the history is readable by any contributor or reviewer, regardless of background.

---

## Default Branch Naming

Always name the default branch **`main`**.

*   **How:** When creating a new repository, set the default branch to `main`. For existing repositories using `master`, rename it via GitHub Settings → Branches → Rename.
*   **Why?** `main` is the modern standard. Consistent naming across all repositories reduces confusion and makes tooling and documentation universally applicable.

---

## Guiding Principle: Keep it Clean and Simple

Reduce complexity and increase clarity. A clean `main` branch, understandable commit history, and consistent processes lead to better software.

---

## Git Workflow

A workflow designed to maintain a clean and linear project history in the `main` branch.

### 1. Branch Naming Convention

Feature branches must be named using the same type prefix as the conventional commit that will result from the PR, followed by a short kebab-case description.

*   **Format:** `<type>/<short-description>` (e.g. `feat/user-auth`, `fix/login-bug`, `docs/api-guide`)
*   **Types:** Use the same prefixes as commit types — `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
*   **Why?** Makes the purpose of a branch immediately clear from its name, and keeps branch names consistent with commit history.

### 2. No Direct Commits to Main

Never commit directly to `main`. All changes must go through a feature branch and a pull request.

*   **Why?** Direct commits bypass review, break the linear squash-merge history, and make it impossible to associate changes with a PR number.

### 3. Pull Request Requirements

Changes to `main` should go through a pull request. Direct commits to `main` create a messy history.

*   **One PR Per Feature Branch:** Each feature branch addresses a single, specific purpose and results in exactly one pull request.
*   **PR Title Format:** The PR title must follow the same conventional commit format as the resulting squash merge commit (e.g. `feat: Add user authentication`). The PR number is appended automatically during merge.
*   **Test Plan:** PRs that change code behaviour must include a test plan — a markdown checklist of steps to verify the change works as expected. Check off each item before merging. Pure documentation or configuration changes do not require a test plan.
*   **Why?** Ensures code changes are explicitly verified before reaching `main`, reducing the risk of regressions.

### 4. Squash Merge Policy

Pull requests targeting the `main` branch benefit from squash merging. This condenses the feature's entire commit history into a single, meaningful commit on the `main` branch.

*   **Why?** Keeps the `main` branch history clean, readable, and focused on features and fixes rather than incremental work-in-progress commits.
*   **PR Number Recommendation:** Include the PR number in brackets at the end (e.g., `feat: Add user authentication (#42)`) for traceability between commits and pull requests.

#### Exception: Experiment and Research Branches

Branches used for experiments, research, or exploratory work should use a **regular merge** (not squash).

*   **Why?** The individual commits in an experiment tell the story of what was tried and why. Squashing that history into one commit loses the scientific trail. The spirit of the rule — keep `main` clean and understandable — is what matters, not the mechanism.

### 5. Delete Head Branch on Merge

Always delete the feature branch as part of the merge command itself.

*   **How:** Pass `--delete-branch` to the `gh pr merge` command:
    ```
    gh pr merge <number> --squash --delete-branch --subject "feat: Your title (#42)"
    ```
*   **Why?** Makes branch cleanup an explicit, visible step rather than a hidden repository setting. Nothing is left to chance.

### 6. Pull Request Review Philosophy

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
