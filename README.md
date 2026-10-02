# React 19 Frontend Application

A modern, containerized frontend web application built with **React 19**, **Vite 8**, and **Oxlint**, fully orchestrated with **Docker Compose**.

---

## 🛠 Tech Stack

- **Framework**: [React 19](https://react.dev/) (`react`, `react-dom`)
- **Build Tool & Dev Server**: [Vite 8](https://vitejs.dev/) with [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react)
- **Linter**: [Oxlint](https://oxc.rs/docs/guide/usage/linter.html) (high-performance Rust-based JavaScript/React linter)
- **Containerization**: [Docker](https://www.docker.com/) & Docker Compose (`node:22-alpine`)

---

## 🚀 Quick Start (Docker)

All development and build processes are containerized. You do not need Node.js installed on your host machine—only **Docker** and **Docker Compose**.

### 1. Clone & Setup Environment

```bash
# Clone the repository
git clone git@github-personal:Vishnu-Selva-Kumar/react-js-frontend.git
cd react-js-frontend

# Copy environment variables
cp .env.example .env
```

### 2. Start Development Server

```bash
docker compose up -d
```

The application will be available at:
👉 **[http://localhost:5173](http://localhost:5173)**

Hot Module Replacement (HMR) is enabled with polling support (`CHOKIDAR_USEPOLLING=true`) for seamless cross-platform live reload.

### 3. Stop Containers

```bash
# Stop containers
docker compose stop

# Stop and remove containers and network
docker compose down
```

---

## 💻 CLI Commands Reference

All commands must be executed through the running Docker service (`web`):

| Action | Command |
| :--- | :--- |
| **Start Dev Server (Detached)** | `docker compose up -d` |
| **View Live Logs** | `docker compose logs -f web` |
| **Run Linter (Oxlint)** | `docker compose exec web npm run lint` |
| **Production Build** | `docker compose exec web npm run build` |
| **Install New Package** | `docker compose exec web npm install <package-name>` |
| **Install Dev Dependency** | `docker compose exec web npm install <package-name> --save-dev` |
| **Open Container Shell** | `docker compose exec web sh` |
| **Rebuild Docker Image** | `docker compose build` |

> For additional Docker CLI reference and standalone run commands, see [`.docs/cli-documents.md`](.docs/cli-documents.md).

---

## 🔍 Code Quality & Standards

- **Linting**: Run `docker compose exec web npm run lint` before committing to ensure adherence to React 19 hook rules and code hygiene.
- **Component Architecture**: Keep presentation clean; extract business logic, data fetching, and state into custom hooks in `src/hooks/`.
- **Git Commits**: All commit messages follow the [Conventional Commits](https://www.conventionalcommits.org/) format (`<type>(<scope>): <description>`). See [`.agents/rules/git-commit.md`](.agents/rules/git-commit.md) for allowed types and scopes.

---

## 📄 License

This project is private and proprietary.
