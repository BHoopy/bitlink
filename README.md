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

## Demo

A live instance is available at [bitlink.mxcodelab.com](https://bitlink.mxcodelab.com).

---

## Deploy on Render (Recommended)

The fastest way to get BitLink online is through Render.

### 1. Push to GitHub

Create a private GitHub repository and push this folder to it.

### 2. Create a new Web Service on Render

1. Log in to [Render](https://render.com)
2. Click **New +** → **Web Service**
3. Connect your GitHub repository
4. Set the following:

```
Runtime:         Node
Build Command:   npm install
Start Command:   npm start
```

### 3. Set the environment variable

Under the **Environment** section, add:

```
Key:        JWT_SECRET
Value:      <paste a long random string>
```

### 4. Deploy

Click **Create Web Service**. Render will build and deploy automatically.

### 5. Create the admin account

**Visit your Render URL immediately after deployment.** The first visitor is prompted to create an admin account. If someone else reaches the site before you, they could claim admin access instead.

> ⚠️ Do not share the URL publicly until you have created your admin account.

### Linking a custom domain

BitLink supports custom domains. After deployment, add your domain in the Render dashboard under **Settings** → **Custom Domain**.

> Join the [Telegram Group](https://t.me/mxcodelab) to watch how to link a personal domain.

---

## Local Hosting (Optional)

These steps are for running BitLink on your own machine.

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Copy the example file:

```
copy .example.env .env
```

Open `.env` and set `JWT_SECRET` to a random string:

```text
JWT_SECRET=your-random-secret-here
```

### 3. Initialize the database

```bash
npm run migrate
```

### 4. Start the server

Development mode:

```bash
npm run dev
```

Production mode:

```bash
npm start
```

The app starts on `http://localhost:3000`.

### 5. Create the admin account

**Visit `http://localhost:3000` immediately after starting the server.** The first visitor is prompted to create an admin account.

> ⚠️ Do not share the site URL publicly until you have created your admin account.

---

## Docker

```bash
docker compose up
```

Multiple compose files are available for different database setups:

| File | Services |
| --- | --- |
| `docker-compose.yml` | BitLink + SQLite |
| `docker-compose.sqlite-redis.yml` | BitLink + SQLite + Redis |
| `docker-compose.postgres.yml` | BitLink + Postgres + Redis |
| `docker-compose.mariadb.yml` | BitLink + MariaDB + Redis |

---

## Configuration

All settings use environment variables. Every variable also supports a `_FILE` suffix.

| Variable | Description | Default |
| --- | --- | --- |
| `JWT_SECRET` | Signs auth tokens. Use a long random string. | — |
| `PORT` | App port. | `3000` |
| `SITE_NAME` | Browser tab name. | `BitLink` |
| `DEFAULT_DOMAIN` | Host domain. | `localhost:3000` |
| `LINK_LENGTH` | Generated slug length. | `6` |
| `DB_CLIENT` | Database driver. | `better-sqlite3` |
| `DB_FILENAME` | SQLite file path. | `db/data` |
| `DISALLOW_REGISTRATION` | Block new signups. | `true` |
| `DISALLOW_ANONYMOUS_LINKS` | Require login to create links. | `true` |
| `MAIL_ENABLED` | Enable email features. | `false` |
| `OIDC_ENABLED` | Enable OpenID Connect. | `false` |
| `REDIS_ENABLED` | Enable Redis. | `false` |
| `ENABLE_RATE_LIMIT` | Rate-limit API routes. | `false` |

---

## Themes and Customization

Place custom files inside the `custom/` folder:

```
custom/
  css/        — Stylesheets
  images/     — Logo, favicon, etc.
  views/      — Handlebars templates
```

For Docker, mount `custom/` to `/kutt/custom`.

---

## Support

Join the [Telegram Group](https://t.me/mxcodelab) for help, including how to link a personal domain to your deployment.

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
