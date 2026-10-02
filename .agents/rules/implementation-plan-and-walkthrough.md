# Implementation Plan & Walkthrough Guidelines

This document outlines mandatory rules and standards for generating **Implementation Plans** and post-implementation **Walkthrough Files** during development tasks for the **react-js** project.

> [!IMPORTANT]
> **Mandatory Rule Compliance**: You MUST strictly follow all rule files in both the `.agents/rules` and `.rules` directories across all planning, code generation, validation, testing, git commits, and walkthrough phases:
> - **Pre-Execution Approval**: For **EVERY user prompt or feature request**, you MUST first convert the requirement into a structured Implementation Plan artifact, set `RequestFeedback: true`, and **obtain explicit user approval before writing or executing any code changes**.
> - **`.agents/rules/` directory**:
>   - `implementation-plan-and-walkthrough.md`: Standards for structured plans, action buttons, mermaid diagrams, and walkthrough verification reports.
>   - `react-docker.md`: All Node, npm, Vite, Oxlint, and build commands MUST execute inside `docker compose exec web ...` or `docker exec react-js-web-1 ...`.
>   - `react-components.md`: Strict separation of presentation and business logic, custom hooks, clean JSX, and CSS standards.
>   - `git-commit.md` / `commit_type.yml`: Strict Conventional Commits formatting (`<type>(<scope>): <description>`), allowed types, mandatory user confirmation (branch, commit, push), staging rules, and secret protection.

---

## 1. Implementation Plan Guidelines

For **EVERY prompt, feature, or refactoring task**, convert the request into an Implementation Plan and obtain user approval before executing:

### 1.1 Chat Content Analysis & Discovery
- Follow all rule files in the `.agents/rules` and `.rules` directories.
- Thoroughly analyze the user's prompt, past discussion, existing codebase patterns, component hierarchy, state management, routes, and styling before drafting the plan.
- Identify edge cases, breaking changes, package dependencies, and responsive design requirements.

### 1.2 Artifact Creation & Action Buttons
- Create the implementation plan as a structured Markdown (`.md`) artifact in the designated artifact directory (`<appDataDir>/brain/<conversation-id>/`).
- Configure artifact metadata with `RequestFeedback: true` and `UserFacing: true` so the interface renders interactive **"Proceed"** / **"Review"** action buttons for user confirmation.
- Format the plan with clean headings, alert callouts (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`), tables, and code snippets.

### 1.3 Workflow Architecture & Diagrams
- When the task introduces new user interactions, state transitions, or component trees, include **Mermaid Diagrams**:
  - **Component Hierarchy / Architecture**: High-level component tree showing props flow, state lifting, and custom hooks.
  - **Interaction Flowchart / State Machine**: State transitions, user event handlers, validation states, and asynchronous data fetching flows.

### 1.4 Implementation Steps & Tasks Breakdown
- Group tasks into clear, chronological phases:
  - **Phase 1: Environment & Dependencies**: New npm packages to install inside Docker container (`docker compose exec web npm install <pkg>`).
  - **Phase 2: Architecture & State Management**: Custom hooks (`src/hooks/`), context providers, state models, utilities.
  - **Phase 3: Component Development**: Reusable UI components (`src/components/`), props interfaces, presentational layouts.
  - **Phase 4: Pages & Feature Integration**: Main view assembly (`src/App.jsx` or page views), routing, feature wiring.
  - **Phase 5: Styling & Polish**: CSS styling (`src/index.css`, `src/App.css`, component CSS), transitions, responsive breakpoints.
  - **Phase 6: Code Quality & Linting**: Running Oxlint inside Docker container to ensure zero lint errors or warnings.
  - **Phase 7: Build & Verification**: Production build verification (`npm run build` inside Docker) and browser validation.

### 1.5 Testing & Verification Strategy
- Outline verification steps to be executed:
  - Static analysis: Oxlint verification via `docker compose exec web npm run lint`.
  - Build validation: Vite production bundling via `docker compose exec web npm run build`.
  - Browser inspection: Verifying UI responsiveness, console log cleanliness, interactive states (hover, active, disabled).

### 1.6 Execution Command Sequence
- Document the exact commands to be executed in sequence.
- Adhere to the environment rules (e.g., executing inside Docker container: `docker compose exec web ...` or `docker exec react-js-web-1 ...`).
- Include dependency installation, linter runs, and build executions.

### 1.7 Manual Testing Flow & Instructions
- Provide concrete manual testing instructions:
  - Step-by-step user interaction flow.
  - Expected visual states, transitions, modals, and toasts.
  - Responsive screen width testing (mobile, tablet, desktop).

---

## 2. Walkthrough File Guidelines

Upon completing the implementation and verification, generate a Walkthrough document (`<feature_name>_walkthrough.md`) in the artifact directory.

### 2.1 Overview of Changes
- Provide an executive summary of what was built, updated, or removed.
- Detail the rationale behind architectural choices and how user feedback or review comments were addressed.

### 2.2 Clickable File Links (MANDATORY)
- **Every modified, created, or deleted file MUST be formatted as a clickable link** using GitHub-style Markdown with the `file:///` protocol:
  - Format: `[relative/path/to/file.ext](file:///absolute/path/to/file.ext)`
  - When referencing specific lines or functions: `[ComponentName](file:///absolute/path/to/file.ext#L10-L25)`
  - Use forward slashes `/` even on Windows operating systems.

### 2.3 Quality & Build Verification Report
- Execute Oxlint and Vite build inside the Docker container.
- Include the verbatim output:
  - Oxlint output (`docker compose exec web npm run lint`).
  - Vite build output (`docker compose exec web npm run build`).
  - Status confirmation of zero errors.

### 2.4 Modified & Created Files Reference
- Conclude with a categorized reference index of all changed files:
  - **Components**: Reusable UI components, modals, inputs.
  - **Hooks & Utilities**: Custom hooks, state handlers, helpers.
  - **Styles & Assets**: CSS files, stylesheets, icons, images.
  - **Configuration & Environment**: `package.json`, Vite config, Docker files.
- Every entry in this reference section **must be a clickable file link**.

### 2.5 Verification & Validation Summary
- Confirm that all acceptance criteria are met.
- Document any manual testing done or instructions for final user verification.

### 2.6 Git Commit Workflow & Conventions
- Adhere strictly to the Conventional Commits specification in `.agents/rules/git-commit.md` and `.agents/rules/commit_type.yml`.
- Format: `<type>(<scope>): <description>` using allowed types (`feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `style`, `chore`, `build`, `ci`, `revert`).
- Ensure descriptions use lowercase, imperative wording, concise phrasing ($\le$ 72 chars), and no trailing period.
- Never stage sensitive files or secrets (`.env`, credentials, keys).
- Review changes with `git status` and `git diff --cached` before committing.
