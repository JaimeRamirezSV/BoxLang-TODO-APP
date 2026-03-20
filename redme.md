# BoxLang Simple Page - Test Application

A BoxLang web application with interactive UI components designed for Playwright end-to-end testing.

## Pages

- **Home** (`index.bxm`) — Contact form, toggle, counter, data table, hover demo, drag & drop
- **About** (`about.bxm`) — Project description and feature overview
- **Contact** (`contact.bxm`) — Contact form and contact information

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on your machine.

## Setup with Docker

1. **Clone the repository:**

   ```bash
   git clone <repository-url>
   cd example-simple-page-bx-tests
   ```

2. **Start the application:**

   ```bash
   docker compose up
   ```

   This pulls the `ortussolutions/boxlang:miniserver` image, mounts the application code, and starts the server.

3. **Open in your browser:**

   [http://localhost:8080](http://localhost:8080)

4. **Stop the application:**

   ```bash
   docker compose down
   ```

## Running in the Background

To start the container in detached mode:

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
| `boxlang.json` | BoxLang server configuration (port, rewrites, debug mode) |
| `Application.bx` | BoxLang application settings (session management, mappings) |

### Environment Variables

Defined in `Compose.yml`:

| Variable | Default | Description |
|----------|---------|-------------|
| `BOXLANG_DEBUG` | `true` | Enable debug output |
| `MAX_MEMORY` | `1g` | JVM max heap size |
| `MIN_MEMORY` | `512m` | JVM min heap size |
| `TZ` | `UTC` | Server timezone |
