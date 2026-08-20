# Vite skeleton

A Nette application skeleton with Vite asset bundling and Tailwind CSS.

## Requirements

- PHP 8.4 or newer
- [Composer](https://getcomposer.org/)
- Node.js 20 or newer and npm 10 or newer

## Create a project

```bash
composer create-project contributte/vite-skeleton acme
cd acme
npm ci
```

## Current blocker

The checked-in application is not currently runnable after installation. `composer.json` autoloads `Contributte\Vite\` from `Vite/src`, and `config/services.neon` registers `Contributte\Vite\Nette\Extension`, but the repository does not contain `Vite/src`. Composer still generates that autoload mapping, but the Nette application then fails with HTTP 500 because the configured extension class cannot be loaded.

Until that extension source is restored or replaced in the project itself, there is no verified application startup, test, or first-success path to document. The commands below describe only the frontend scripts that are present; they do not resolve the PHP application blocker.

## Frontend commands

```bash
npm run dev      # start the Vite development server
npm run build    # create a production build
npm run preview  # preview the production build
```

## Configuration and database

`config/local.neon` is tracked by this skeleton and currently configures the Docker MariaDB service:

```neon
database:
	dsn: 'mysql:host=db;dbname=root'
	user: root
	password: root
```

Treat this file as project configuration, not as an ignored secrets boundary. Before adding real credentials, introduce an appropriate untracked local override or environment-based configuration. For local PHP development without Docker, the database host and credentials would also need to match the local database. Keep `temp/` and `log/` writable by the PHP process.

Vite builds all JavaScript files from `src/scripts/` and CSS files from `src/styles/` into `www/`, and writes a Vite manifest there. Keep the generated assets and manifest available to the web application when deploying.

No test suite is present in the repository. Restoring or replacing the missing Vite extension is required before an application smoke test can be defined honestly.
