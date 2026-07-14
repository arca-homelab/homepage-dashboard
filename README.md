# homepage-dashboard

Setup for [Homepage](https://gethomepage.dev/), a modern, self-hosted dashboard for your services and bookmarks.

This repo runs the official Homepage Docker image via Docker Compose, with the configuration stored in [`config/`](config/) so it can be version-controlled and edited freely. Config changes are picked up without rebuilding the image — just refresh the page (use the reload icon in the UI, or restart the container if a change doesn't show up).

## Prerequisites

- Docker
- Docker Compose (bundled with Docker Desktop)

## Getting started

1. Copy the environment file and adjust it if needed:

   ```sh
   cp .env.example .env
   ```

2. Start the stack:

   ```sh
   docker compose up -d
   ```

3. Open [http://localhost:3000](http://localhost:3000).

4. Stop the stack:

   ```sh
   docker compose down
   ```

## Project structure

```
config/
  settings.yaml   # title, theme, layout
  services.yaml   # your services, grouped
  bookmarks.yaml  # quick links, grouped
  widgets.yaml    # top info widgets (resources, search, datetime, ...)
  custom.css      # optional style overrides
  custom.js       # optional script overrides
images/           # custom icons/backgrounds referenced from the config files
docker-compose.yml
.env.example
```

## Editing the dashboard

- Add services in [`config/services.yaml`](config/services.yaml).
- Add quick links in [`config/bookmarks.yaml`](config/bookmarks.yaml).
- Change appearance/layout in [`config/settings.yaml`](config/settings.yaml).
- Add/remove top info widgets in [`config/widgets.yaml`](config/widgets.yaml).

Full configuration reference: <https://gethomepage.dev/configs/>

## Optional: Docker integration

To let Homepage auto-discover containers and show their status, uncomment the Docker socket volume in `docker-compose.yml`:

```yaml
volumes:
  - /var/run/docker.sock:/var/run/docker.sock:ro
```

See <https://gethomepage.dev/configs/docker/> for details.

## Running on another machine

Copy this repo (or just `config/`, `.env`, and `docker-compose.yml`) to the target machine and run `docker compose up -d` there — it pulls the same official image from `ghcr.io/gethomepage/homepage`, no build step needed.
