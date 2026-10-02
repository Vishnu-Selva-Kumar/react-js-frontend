# React Project CLI Commands Guide

This document provides quick-reference CLI commands for managing the Vite React application using Docker and Docker Compose.

---

### 1. Create React Project CLI
*Scaffolds a new Vite + React project inside an isolated Node Docker container without needing Node installed locally.*

```bash
docker run --rm -it -v "${PWD}:/app" -w /app node:22-alpine sh -c "npm create vite@latest . -- --template react -y"
```

---

### 2. Install React Project Dependencies CLI
*Installs all required dependencies listed in package.json inside the containerized environment.*

- **Build/rebuild image with dependencies:**
  ```bash
  docker compose build
  ```
- **Install dependencies using an ad-hoc container:**
  ```bash
  docker run --rm -v "${PWD}:/app" -w /app node:22-alpine npm install
  ```
- **Install a new package into the running service:**
  ```bash
  docker compose exec web npm install <package-name>
  ```

---

### 3. Run React Project CLI
*Starts the Vite development server with live reload and exposes port 5173.*

- **Start in background mode (Recommended):**
  ```bash
  docker compose up -d
  ```
- **Start in foreground mode (attached logs):**
  ```bash
  docker compose up
  ```
- **Run via standalone Docker command:**
  ```bash
  docker run --rm -it -p 5173:5173 -v "${PWD}:/app" -w /app node:22-alpine sh -c "npm run dev -- --host"
  ```

---

### 4. Open Shell in React Project CLI
*Opens an interactive shell (`sh`) session inside the running container for executing commands and troubleshooting.*

- **Attach shell via Docker Compose (Recommended):**
  ```bash
  docker compose exec web sh
  ```
- **Attach shell via Container Name:**
  ```bash
  docker exec -it react-js-web-1 sh
  ```
- **Open a temporary standalone container shell:**
  ```bash
  docker run --rm -it -v "${PWD}:/app" -w /app node:22-alpine sh
  ```

---

### 5. Stop React Project CLI
*Stops and tears down running project containers and networks.*

- **Stop and remove containers and network:**
  ```bash
  docker compose down
  ```
- **Stop containers without removing them:**
  ```bash
  docker compose stop
  ```
