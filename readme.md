# BoxLang Todo App

A BoxLang web application with session-based authentication and full CRUD todo management, backed by SQLite and running in Docker.

## Features

- **Login / Logout** — Session-based authentication with SHA-256 password hashing
- **Todo CRUD** — Create, read, update, and delete todos scoped per user
- **Toggle completion** — Mark todos as done or pending
- **Post/Redirect/Get** — All form submissions redirect to prevent resubmission dialogs
- **404 handling** — Friendly error page for invalid routes
- **Route protection** — Handlers and services are not directly accessible via URL

## Project Structure

```
├── Application.bx          # App config, datasource, auth guards, lifecycle hooks
├── index.bxm               # Entry redirect (logged in → todos, else → login)
├── Compose.yml              # Docker Compose service definition
├── assets/
│   └── css/
│       └── app.css          # Global stylesheet (flat grey & light blue theme)
├── pages/
│   ├── login.bxm            # Login page with form handling
│   ├── todos.bxm            # Todo list with stats, add form, edit modal
│   ├── logout.bxm           # Session cleanup and redirect
│   └── 404.bxm              # Not-found error page
├── handlers/
│   ├── LoginHandler.bx      # Validates credentials, populates session
│   └── TodoHandler.bx       # Dispatches CRUD actions to TodoService
├── services/
│   ├── UserService.bx       # User schema, seeding, authentication queries
│   └── TodoService.bx       # Todo schema and CRUD queries
└── config/
    ├── boxlang.json/         # BoxLang server configuration
    └── server.json/          # Server settings
```

## Default Credentials

| Username | Password |
|----------|----------|
| `admin`  | `admin123` |

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

1. **Clone the repository:**

   ```bash
   git clone <repository-url>
   cd BoxLang-TODO-APP
   ```

2. **Start the application:**

   ```bash
   docker compose up
   ```

   This pulls the `ortussolutions/boxlang:miniserver` image, installs the `bx-sqlite` module, mounts the code, and starts the server.

3. **Open in your browser:**

   [http://localhost:8080](http://localhost:8080)

4. **Stop the application:**

   ```bash
   docker compose down
   ```

   To also remove the SQLite data volume:

   ```bash
   docker compose down -v
   ```

## Running in the Background

```bash
docker compose up -d
```

Check logs:

```bash
docker compose logs -f
```

## Configuration

| File | Purpose |
|------|---------|
| `Compose.yml` | Docker Compose service definition (ports, volumes, environment) |
| `config/boxlang.json` | BoxLang server configuration (port, rewrites, debug mode) |
| `Application.bx` | App settings, datasource, session management, route guards |

### Environment Variables

Defined in `Compose.yml`:

| Variable | Default | Description |
|----------|---------|-------------|
| `BOXLANG_DEBUG` | `true` | Enable debug output |
| `BOXLANG_MODULES` | `bx-sqlite` | BoxLang modules to auto-install |
| `MAX_MEMORY` | `1g` | JVM max heap size |
| `MIN_MEMORY` | `512m` | JVM min heap size |
| `TZ` | `UTC` | Server timezone |

## Tech Stack

- **Runtime:** BoxLang Miniserver (Docker)
- **Database:** SQLite via `bx-sqlite` module (persisted in a Docker volume)
- **Auth:** Server-side sessions with SHA-256 hashed passwords
- **Styling:** Custom CSS (flat grey & light blue theme)
