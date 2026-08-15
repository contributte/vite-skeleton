# Vite skeleton

A Nette application skeleton with Vite asset bundling and Tailwind CSS.

## Requirements

- PHP 8.4 or newer
- [Composer](https://getcomposer.org/)
- Node.js 20 or newer and npm 10 or newer
- Docker and Docker Compose (optional)

## Create a project

```bash
composer create-project contributte/vite-skeleton acme
cd acme
composer install
npm ci
```

## Local development

Start the PHP application and Vite in separate terminals:

```bash
php -S 127.0.0.1:8000 -t www
npm run dev
```

Open the application at [http://127.0.0.1:8000](http://127.0.0.1:8000). Vite serves its development server separately; use the URL printed by `npm run dev`.

Build production assets with `npm run build`. `npm run preview` serves the generated Vite output for previewing it.

## Docker services

Docker Compose starts Apache/PHP at [http://localhost](http://localhost), MariaDB, Adminer at [http://localhost:8080](http://localhost:8080), and a one-shot Composer install service:

```bash
docker compose up
```

The database is not published to the host. Adminer can connect to it with server `db`, database `root`, user `root`, and password `root`.

## Configuration and database

The checked-in `config/local.neon` configures the application to use the Docker MariaDB service:

```neon
database:
	dsn: 'mysql:host=db;dbname=root'
	user: root
	password: root
```

For local PHP development without Docker, change the host and credentials to match your database. Keep `temp/` and `log/` writable by the PHP process.

Vite builds all JavaScript files from `src/scripts/` and CSS files from `src/styles/` into `www/`, and writes a Vite manifest there. Keep the generated assets and manifest available to the web application when deploying.

## Checks

CI validates Composer metadata, installs PHP dependencies, installs npm dependencies, and runs `npm run build`.

To run the bundled Tester suite manually after `composer install`:

```bash
vendor/bin/tester -s -p php --colors 1 tests
```
