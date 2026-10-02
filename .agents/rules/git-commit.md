# Git Commit & Workflow Rules

This document outlines mandatory standards for Git commit messages, branch management, staging, and commit workflows for the **react-js** project.

> [!IMPORTANT]
> **Mandatory User Confirmation Policy**:
> 1. **Branching**: NEVER create, checkout, or switch to a new branch without explicit user confirmation.
> 2. **Commit**: ALWAYS obtain explicit user confirmation before executing `git commit`.
> 3. **Push**: NEVER execute `git push` to any remote repository without explicit user confirmation.

---

## 1. Conventional Commits Standard

All commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <short description>
```

- **Format**: Lowercase type, optional scope in parentheses, colon, space, followed by an imperative short description.
- **Example**: `feat(ui): add responsive navigation bar with theme toggle`

### 1.1 Allowed Commit Types

| Type | Description | When to Use |
| :--- | :--- | :--- |
| `feat` | New feature | Adding new functionality, pages, hooks, or components |
| `fix` | Bug fix | Resolving a defect, UI glitch, or runtime bug |
| `refactor` | Code refactoring | Restructuring component hierarchy or logic without changing external behavior |
| `perf` | Performance improvement | Memoization, bundle size reduction, code splitting |
| `docs` | Documentation | Updating README, CLI docs, or rule files |
| `test` | Automated testing | Adding, modifying, or fixing tests |
| `style` | Code formatting | Formatting, whitespace, or lint fixes without logic changes |
| `chore` | Maintenance tasks | Updating npm packages, config tweaks |
| `build` | Build / Environment | Dockerfile, docker-compose, Vite configuration, or bundling changes |
| `ci` | Continuous Integration | CI/CD workflows, automated build scripts |
| `revert` | Reverting changes | Reverting a previous commit |

### 1.2 Message Formatting Rules
- **Imperative mood**: Use verbs like `add`, `fix`, `refactor`, `prevent` (not `added`, `fixes`, `fixing`).
- **Lowercase**: The description must start with a lowercase letter.
- **No trailing period**: Do not end the description with a period (`.`).
- **Subject length**: Concise and descriptive (maximum 72 characters).
- **No vague messages**: Never use generic messages such as `update`, `changes`, `done`, `fix`, or `code changes`.

### 1.3 Preferred Scopes for `react-js`
Select the single scope that best describes the affected area:
- `ui`: General UI updates, design systems, layouts
- `component`: Specific reusable UI component (e.g., `button`, `modal`, `navbar`)
- `hook`: Custom React hooks (`useTheme`, `useFetch`, `useAuth`)
- `page`: Page views or major view compositions
- `style`: CSS files, themes, design tokens, responsive breakpoints
- `docker`: Dockerfile, docker-compose configuration, container setup
- `config`: Vite config, Oxlint config, environment variables
- `deps`: Adding or updating npm packages
- `lint`: Lint fixes, Oxlint rule adjustments
- `build`: Production build optimization, bundling assets

---

## 2. Mandatory Git Workflow

### 2.1 Branching Rules
- **Do not create or switch branches autonomously.**
- Always ask the user and obtain explicit confirmation before executing `git checkout -b <branch>`, `git switch -c <branch>`, or `git branch <branch>`.

### 2.2 Pre-Commit Inspection
Before staging or committing:
1. Run `git status` to identify untracked and modified files.
2. Run `git diff` to understand all unstaged code changes.
3. Determine the primary purpose of the change and select the single matching commit type and scope.
4. Compose the Conventional Commit message following the formatting guidelines.

### 2.3 Staging Rules
- **Stage atomically**: Only stage files that belong to the current logical change (`git add <file1> <file2>`).
- **No blind staging**: Do not run `git add .` or `git add -A` when unrelated modifications exist.
- **Review staged diff**: Always run `git diff --cached` to verify staged changes before committing.

### 2.4 Commit Execution
- Present the proposed commit message and list of staged files to the user.
- **Obtain explicit user confirmation before executing `git commit`.**
- Verify the committed result immediately with `git log -1 --oneline`.

### 2.5 Remote Push
- **Never run `git push` without explicit user confirmation.**

---

## 3. Security & Secret Protection

The following sensitive files and patterns must **NEVER** be staged or committed:
- Environment configuration: `.env`, `.env.*`, `.env.local`
- Private keys & certificates: `*.pem`, `*.key`, `*.crt`
- Credentials & secrets: API keys, access tokens, auth credentials
- Generated folders: `node_modules/`, `dist/`

---

## 4. Atomic Commits Policy

- **Do not combine unrelated changes** into a single commit.
- Keep features, bug fixes, dependency updates, and refactoring in separate, focused commits.

---

## 5. Examples

### Good Examples
- `feat(component): add accessible modal dialog with backdrop blur`
- `fix(hook): resolve stale closure in useDebounce`
- `refactor(ui): extract card layout into reusable container`
- `perf(build): optimize vite chunks and dynamic import splitting`
- `docs(docker): update container execution instructions`
- `chore(deps): update vite and react dependencies`
- `build(docker): add chokidar polling flag for windows volume sync`

### Bad Examples (DO NOT USE)
- `update code`
- `changes`
- `fix`
- `done`
- `updated files`
- `Added New Feature`
- `Fixed the issue.`
