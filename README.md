# contributte/vite-skeleton

## Goal and stack

Minimal production-ready starter for Nette applications with Vite asset bundling.

- PHP 8.4+
- Nette Framework 3.2+
- Node.js and npm for frontend tooling

## Requirements

- PHP 8.4 or newer
- Node.js 20+ and npm 10+

## Installation

```bash
composer install
npm ci
```

## Development commands

```bash
npm run dev
php -S 127.0.0.1:8000 -t www
```

## Build commands

```bash
npm run build
npm run preview
```

## Writable directories

Application runtime directories must be writable by the web server/PHP process:

- `temp/`
- `log/`

Prefer correct ownership and group permissions (for example `775`) over world-writable permissions.
