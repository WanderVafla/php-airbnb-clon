# PHP Airbnb Clone

A simple Airbnb-style rental platform built with **Laravel** as a Jobtrek training project (brief `JT_DEV_B52`).

Users can offer their own apartments for rent and book apartments offered by other users. Pages are rendered on the server with **Blade** templates; no frontend JavaScript framework is used.

## Features

- Registration, login and logout with username, email and password (Laravel built-in authentication).
- Apartments list with filters (my apartments, my bookings, location) and sorting (price, number of rooms).
- Create, edit (owner or admin) and delete (owner) an apartment, with photo upload.
- Apartment details page with availability status.
- Book an apartment when it is available, and cancel a future booking.
- "My bookings" page.
- Home page with the 3 most rented locations and 2 apartment suggestions per location.
- Profile page to edit username, email and password.
- Admin dashboard to list, delete and promote users.

## Dependencies

### Required tools

| Tool | Version | Used for |
| --- | --- | --- |
| [PHP](https://www.php.net/) | 8.5+ with `pdo_pgsql` | Running the application |
| [Composer](https://getcomposer.org/) | 2+ | PHP dependencies |
| [Node.js](https://nodejs.org/) and npm | 22+ | Building CSS and assets with Vite |
| [Docker](https://www.docker.com/) with Docker Compose | recent | Running the PostgreSQL database |

### Main packages

| Package | Role |
| --- | --- |
| `laravel/framework` 13 | PHP framework |
| PostgreSQL 18 (Docker image `postgres:18-alpine`) | Database |
| `vite` + `laravel-vite-plugin` | Asset bundling |
| `tailwindcss` 4 | Styling |
| `laravel/pint` (PSR-12 preset) | Code formatter |
| `pestphp/pest` | Tests |

The full lists are in `composer.json` and `package.json`.

## Installation

1. Clone the repository and go into the folder:

   ```bash
   git clone git@github.com:WanderVafla/php-airbnb-clon.git
   cd php-airbnb-clon
   ```

2. Create your environment file:

   ```bash
   cp .env.example .env
   ```

   The database settings in `.env` (`DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD`, `DB_PORT`) are also used by Docker Compose to create the database. If port `5432` is already used on your machine, set another port in both `DB_PORT` and `FORWARD_DB_PORT` (for example `5433`).

3. Start the PostgreSQL database:

   ```bash
   docker compose up -d
   ```

   Check that the container is `healthy` with `docker compose ps`.

4. Install the dependencies, generate the app key, run the migrations and build the assets:

   ```bash
   composer setup
   ```

   This runs `composer install`, `php artisan key:generate`, `php artisan migrate`, `npm install` and `npm run build`.

5. Start the application:

   ```bash
   composer dev
   ```

   Then open <http://localhost:8000>.

To stop the database, run `docker compose down`. The data stays in the Docker volume `pgsql-data`.

## Development

| Task | Command |
| --- | --- |
| Run the tests | `php artisan test` |
| Format the code (Pint, PSR-12) | `vendor/bin/pint` |
| Reset the database | `php artisan migrate:fresh` |
