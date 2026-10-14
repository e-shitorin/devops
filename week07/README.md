# Week 07 — Docker Compose

## 1. Container Status

Command: `docker compose ps`

After scaling, three web containers were running:
- `guestbook-web-1` — Up (healthy)
- `guestbook-web-2` — Up (healthy)
- `guestbook-web-3` — Up (healthy)
- `guestbook-redis-1` — Up (healthy)
- `guestbook-nginx-1` — Up

Nginx is exposed on port 8081.

## 2. Scaling and Load Balancing

Command: `docker compose up -d --scale web=3`

Repeated requests through Nginx returned different container hostnames, confirming that requests were distributed across the web containers.

Screenshot: output showing the different `Pod/Host` values.

## 3. Volume Persistence Test

### `docker compose down` then `docker compose up`

The guestbook entry remained after restarting the containers because the Redis volume was preserved.

### `docker compose down -v` then `docker compose up`

The guestbook entry disappeared because the Redis volume was removed and a new empty volume was created.

## 4. Why `.env` Must Not Be Pushed to Git

The `.env` file contains environment variables and may contain passwords or other secrets. Pushing it to a public or shared repository could expose them. The `.env` file is ignored by Git; `.env.example` provides a template without the real password.

## 5. Screenshots

- [Container status](./screenshots/compose-ps.png)
- [Load balancing — changing hostnames](./screenshots/load-balancing.png)
- [Volume persistence test](./screenshots/volume-persistence.png)
