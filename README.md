# BitLink

Modern URL shortener with custom domain support. Built for self-hosting with zero configuration.

---

## Overview

BitLink lets you create shortened URLs, set custom aliases, add passwords and expiration dates, and view click statistics. It supports SQLite, Postgres, and MySQL out of the box.

### Highlights

- Self-hosted with no build step
- Custom domain support
- Password-protected and time-expiring links
- Per-link click statistics
- Admin panel for user and link management
- RESTful API
- OpenID Connect login
- Dark and light themes

## Tech Stack

| Layer | Tooling |
| --- | --- |
| Frontend | HTML, Handlebars, CSS |
| Backend | Node.js, Express |
| Database | SQLite / Postgres / MySQL |
| Cache | Redis (optional) |
| Auth | JWT, OIDC, Passport |

## Demo Links

A live instance is available at [bitlink.mxcodelab.com](https://bitlink.mxcodelab.com).

---

## Setup

The only prerequisite is **Node.js 20 or later**. The default database is SQLite — no external services required.

### 1. Install dependencies

Open the project folder and run:

```bash
npm install
```

### 2. Configure environment variables

Copy the example file and edit it:

```
copy .example.env .env
```

Open `.env` and set at least `JWT_SECRET` to a random string:

```text
JWT_SECRET=your-random-secret-here
```

All other variables have sensible defaults. See the configuration table below for details.

### 3. Initialize the database

```bash
npm run migrate
```

This creates all required tables.

### 4. Start the server

For development:

```bash
npm run dev
```

For production:

```bash
npm start
```

The app starts on `http://localhost:3000`. On first launch you will be prompted to create an admin account.

---

## Docker

If you prefer Docker, run this from the project root:

```bash
docker compose up
```

Several compose files are included for different setups:

| File | Services |
| --- | --- |
| `docker-compose.yml` | BitLink + SQLite |
| `docker-compose.sqlite-redis.yml` | BitLink + SQLite + Redis |
| `docker-compose.postgres.yml` | BitLink + Postgres + Redis |
| `docker-compose.mariadb.yml` | BitLink + MariaDB + Redis |

The official Docker image is available on [Docker Hub](https://hub.docker.com/r/kutt/kutt).

---

## Configuration

All settings are passed through environment variables. You can set them directly or use a `.env` file.

Every variable has a `_FILE` variant. For example, `JWT_SECRET_FILE=/path/to/secret` loads the value from a file.

| Variable | Description | Default |
| --- | --- | --- |
| `JWT_SECRET` | Used to sign auth tokens. Use a long random string. | — |
| `PORT` | Port the app runs on. | `3000` |
| `SITE_NAME` | Name shown in the browser. | `BitLink` |
| `DEFAULT_DOMAIN` | Domain the app is hosted on. | `localhost:3000` |
| `LINK_LENGTH` | Length of generated URL slugs. | `6` |
| `DB_CLIENT` | Database driver: `better-sqlite3`, `pg`, `mysql2`. | `better-sqlite3` |
| `DB_FILENAME` | SQLite database file path. | `db/data` |
| `DISALLOW_REGISTRATION` | Block new user signups. | `true` |
| `DISALLOW_ANONYMOUS_LINKS` | Require login to create links. | `true` |
| `MAIL_ENABLED` | Enable email for signup, verification, and password reset. | `false` |
| `OIDC_ENABLED` | Enable OpenID Connect login. | `false` |
| `REDIS_ENABLED` | Enable Redis for caching and rate limiting. | `false` |
| `ENABLE_RATE_LIMIT` | Rate-limit certain API routes. | `false` |

---

## API

Full API reference is available at [docs.bitlink.to](https://docs.bitlink.to).

---

## Themes and Customization

Place custom styles, images, and templates inside the `custom/` folder:

```
custom/
  css/        — Override or add stylesheets
  images/     — Replace logo, favicon, and other images
  views/      — Custom Handlebars templates
```

If you use Docker, mount the `custom/` directory as a volume to `/kutt/custom`.

---

## Browser Extensions

- [Chrome Extension](https://chrome.google.com/webstore/detail/bitlink/pklakpjfiegjacoppcodencchehlfnpd)
- [Firefox Add-on](https://addons.mozilla.org/en-US/firefox/addon/bitlink/)

---

## Integrations

| Tool | Link |
| --- | --- |
| ShareX | Use BitLink as your default shortener. [Wiki →](https://github.com/thedevs-network/kutt/wiki/ShareX) |
| Alfred | [alfred-bitlink](https://github.com/thedevs-network/alfred-kutt) workflow |
| iOS Shortcut | [BitLink Shortcut](https://www.icloud.com/shortcuts/a829856aea2c420e97c53437e68b752b) |

Third-party client libraries:

| Language | Package |
| --- | --- |
| C# (.NET) | [KuttSharp](https://github.com/0xaryan/KuttSharp) |
| Python | [kutt-cli](https://github.com/RealAmirali/kutt-cli) |
| Ruby | [kutt.rb](https://github.com/RealAmirali/kutt.rb) |
| Rust | [urlshortener-rs](https://github.com/vityafx/urlshortener-rs) |
| Node.js | [node-kutt](https://github.com/ardalanamini/node-kutt) |
| Go | [kutt-go](https://github.com/raahii/kutt-go) |
| Kubernetes/Helm | [ArtifactHub](https://artifacthub.io/packages/helm/christianhuth/kutt) |

---

## Short Notes

Use `npm run dev` for local development.

Use `npm run migrate` to apply database migrations.

Use `JWT_SECRET` for authentication token signing — keep this value private.

---

## Support

If something does not work after setup, check these in order:

1. Verify `JWT_SECRET` is set in `.env`
2. Confirm `npm run migrate` completed without errors
3. Check that port 3000 is not already in use
4. Ensure the database file path is writable

> If you are still stuck, join the [Telegram Group](https://t.me/mxcodelab) for assistance.

---

## License

```
Commercial use allowed
Source-code resale prohibited
Redistribution prohibited
Sublicensing prohibited
MX CodeLab retains ownership
```

Copyright &copy; MX CodeLab. All rights reserved.
