# Neuraplus

**AI-powered home rehabilitation platform for stroke survivors** — with first-class support for Urdu and Punjabi.

Neuraplus addresses a real gap: stroke survivors in Pakistan and similar regions often cannot access professional speech or physical therapy. This platform brings structured, evidence-based rehabilitation into the home, in the user's language.

> This project is built with [Nx](https://nx.dev).

## Project Structure

```
.
├── apps/
│   ├── main/          # Marketing website (Next.js)
│   ├── web/           # Dashboard (Next.js)
│   ├── mobile/        # Mobile app (Expo)
│   └── backend/       # Python API (FastAPI + uv)
│       ├── backend/   # Python source code (the actual package)
│       ├── pyproject.toml
│       └── uv.lock
├── packages/          # Shared libraries (empty for now, add here)
├── tools/
│   └── scripts/       # Workspace-level scripts
├── nx.json            # Nx configuration (plugins, caching rules)
├── package.json       # Root JS dependencies and workspaces
├── pnpm-workspace.yaml
├── tsconfig.base.json # Shared TypeScript config
```

---

## Prerequisites

Install these before doing anything else.

| Tool                            | Version                      | Why                      |
| ------------------------------- | ---------------------------- | ------------------------ |
| [Node.js](https://nodejs.org)   | 20.x LTS or higher           | Required for all JS apps |
| [pnpm](https://pnpm.io)         | 9.x or higher                | Package manager for JS   |
| [Python](https://python.org)    | 3.12 (see `.python-version`) | Required for backend     |
| [uv](https://docs.astral.sh/uv) | Latest                       | Python package manager   |
| [Git](https://git-scm.com)      | Any                          | Version control          |

### Checking your versions

```bash
node --version    # Should be 20.x+
pnpm --version    # Should be 9.x+
python --version  # Should be 3.12.x
uv --version      # Should be 0.x
```

---

## First-Time Setup

### 1. Clone the repository

```bash
git clone https://github.com/your-org/neuraplus.git
cd neuraplus
```

### 2. Install JavaScript dependencies

```bash
pnpm install
```

This installs all JS/TS dependencies for the entire monorepo in one command. Nx, Next.js, Expo, and all shared packages are installed here.

### 3. Install the Nx CLI globally (optional but useful)

```bash
npm install -g nx
```

If you skip this, prefix all `nx` commands with `pnpm exec nx` or `npx nx`.

### 4. Set up the Python backend

```bash
# Install Python dependencies for the backend using uv
nx run backend:install
```

This creates a virtual environment inside `apps/backend/.venv` and installs all Python packages defined in `pyproject.toml`.

## Running the Apps

### Run a single app in development

```bash
nx dev main      # Start the hero website (usually http://localhost:3000)
nx dev web       # Start the dashboard (usually http://localhost:4200)
nx dev mobile    # Start the Expo development server
```

> Nx figures out port assignments from each app's Next.js or Expo config. Check the terminal output for the exact URL.

### Run all apps simultaneously

```bash
nx run-many -t dev --all
```

> Warning: this starts all four apps at once including the mobile bundler. Only do this if your machine can handle it. Running them individually is usually better during development.

### Run the Python backend

```bash
# Nx does not have a 'dev' target for the Python backend yet.
# Run it directly via uv:
cd apps/backend
uv run uvicorn backend.main:app --reload --port 8000
```

> The backend will be available at `http://localhost:8000`

---

## All Nx Commands

### General pattern

```bash
nx <target> <project>
```

Example: `nx build web` runs the `build` target on the `web` project.
