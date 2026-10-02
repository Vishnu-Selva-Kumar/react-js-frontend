# React Docker Execution Rules

## Environment Setup
- Node.js and npm may **NOT** be installed or consistent on the host system.
- All CLI commands related to npm, package installation, Vite, Oxlint, and testing **MUST** be executed inside the running Docker container shell.

## Docker Execution Context
- **Target service:** `web` (defined in `docker-compose.yml`)
- **Target container:** `react-js-web-1`
- **Preferred command syntax (Compose):** `docker compose exec web <command>`
- **Direct container syntax:** `docker exec react-js-web-1 <command>`
- **Interactive shell syntax:** `docker compose exec web sh` or `docker exec -it react-js-web-1 sh`

## Command Standards

### Package Management (npm)
```bash
# DO NOT run on host:
npm install <package-name>
npm install <package-name> --save-dev

# DO run inside container:
docker compose exec web npm install <package-name>
docker compose exec web npm install <package-name> --save-dev
```

### Development Server
```bash
# Start Vite development server in detached mode:
docker compose up -d

# Check running status:
docker compose ps
docker ps --filter name=react-js-web-1

# View logs:
docker compose logs -f web

# Stop container:
docker compose stop
# or tear down:
docker compose down
```

### Linting (Oxlint)
```bash
# DO NOT run on host:
npm run lint
npx oxlint

# DO run inside container:
docker compose exec web npm run lint
```

### Production Build
```bash
# DO NOT run on host:
npm run build

# DO run inside container:
docker compose exec web npm run build
```

## Agent Execution Guidelines
1. **Always verify the container is running first:** `docker ps --filter name=react-js-web-1` or `docker compose ps`.
2. **If the container is not running:** start it with `docker compose up -d`.
3. **Wrap every npm/Vite/Oxlint command** inside `docker compose exec web ...` (or `docker exec react-js-web-1 ...`).
4. The host project directory is volume-synced to `/app` inside the container, with `/app/node_modules` isolated in its own volume.
5. **Never attempt `npm`, `npx`, or `./node_modules/.bin/*` directly on the host shell.**
