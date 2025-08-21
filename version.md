# Commit Message Guidelines for Automated Releases

This document provides examples of commit messages that will trigger automated software releases (Patch, Minor, or Major) using `semantic-release` and the Conventional Commits specification. Adhering to these guidelines is crucial for our automated release process to function correctly.

---

## 1. Patch Release (PATCH: `X.Y.Z` -> `X.Y.Z+1`)

A **Patch Release** is for **backward-compatible bug fixes** and very minor, non-breaking improvements. Consumers should be able to upgrade without changing their existing code.

**Key Trigger:** Commit messages starting with `fix:`

**Examples:**

*   `fix: resolve issue with user login redirect`
    *   **Explanation:** A straightforward bug fix.
*   `fix(auth): correct password reset token validation`
    *   **Explanation:** A bug fix specifically within the `auth` scope.
*   `fix: prevent crash when processing malformed input`
    *   **Explanation:** A critical bug fix.

---

## 2. Minor Release (MINOR: `X.Y.Z` -> `X.Y+1.0`)

A **Minor Release** is for **backward-compatible new features** or significant non-breaking changes. Consumers can take advantage of new functionality without breaking existing code.

**Key Trigger:** Commit messages starting with `feat:`

**Examples:**

*   `feat: add new user profile editing page`
    *   **Explanation:** Introduces a new feature.
*   `feat(api): implement new /products endpoint`
    *   **Explanation:** Adds a new API endpoint.
*   `feat: allow custom themes to be applied`
    *   **Explanation:** A new capability for the application.

---

## 3. Major Release (MAJOR: `X.Y.Z` -> `X+1.0.0`)

A **Major Release** is for **backward-incompatible changes**. This means consumers will likely need to modify their existing code or configurations to upgrade successfully.

**Key Triggers (Choose ONE of these methods):**

*   **`BREAKING CHANGE:` footer in the commit body.**
    *   Requires a blank line between the subject/body and the `BREAKING CHANGE:` line.
*   **`!` (exclamation mark) after the type/scope in the subject line.**
    *   This is a more concise way to signal a breaking change.

**Examples (using `BREAKING CHANGE:` footer):**

feat(api): remove old user authentication endpoint

This commit removes the deprecated /api/v1/auth endpoint.
Users must now use /api/v2/auth for all authentication requests.
The new endpoint requires an API key in the header.

BREAKING CHANGE: The /api/v1/auth endpoint is no longer supported.

*   **Explanation:** 
    A new feature (`feat`) that introduces a breaking change by removing an old API.<br>
    fix: correct database schema for user table

    This fix requires a database migration that is not backward-compatible
    with previous versions of the schema.

    BREAKING CHANGE: Database schema for 'users' table has changed. Manual migration required.

*   **Explanation:** A bug fix (`fix`) that unfortunately requires a breaking change due to schema updates.

**Examples (using `!` in subject line):**

*   `feat!: remove old user authentication endpoint`
    *   **Explanation:** A new feature (`feat`) that is also a breaking change.
*   `refactor(core)!: simplify internal logging mechanism`
    *   **Explanation:** A refactoring (`refactor`) that has external breaking implications.
*   `fix(types)!: update return type of 'getData' function`
    *   **Explanation:** A bug fix (`fix`) that changes a public interface, making it a breaking change.

---

## Commits That Do NOT Trigger a Release

Some commit types are important for project history but do not trigger a new version release. These will still appear in the generated changelog if a release occurs due to other commits.

**Examples:**

*   `chore: update dependencies`
*   `docs: update README with new installation instructions`
*   `style: format code according to linter rules`
*   `refactor: restructure internal utility functions`
*   `test: add unit tests for data validation`
*   `build: update webpack configuration`
*   `ci: update GitHub Actions workflow`

---

## Important Reminders:

*   **Consistency is Key:** Always use these conventions for your commit messages.
*   **Clarity:** Write clear and concise commit messages that accurately reflect the change.
*   **`fetch-depth: 0`:** Ensure your CI/CD pipeline's checkout step fetches the full Git history (`fetch-depth: 0`) for `semantic-release` to properly analyze all commits.
*   **Logs are Your Friend:** If a release doesn't happen as expected, always check the `semantic-release` logs in your CI/CD pipeline for detailed analysis.