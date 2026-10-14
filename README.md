# Hermertia Flarum

Community forum for Hermertia, built using Flarum.

The project provides a reproducible local development environment using Docker, with PHP/Apache and MariaDB isolated from the host system.

## Architecture

The local environment consists of two Docker services:

1. web - PHP 8.4, Apache, Composer and Flarum
2. db - MariaDB 11.8

The Flarum application source is stored in: `src/`

The database is persisted using a Docker volume, so database data survives container recreation.

```
Browser
   |
   | localhost:8000
   v
PHP 8.4 + Apache
   |
   | db:3306
   v
MariaDB 11.8
```

## Requirements

You will need:

- Docker
- Docker Compose
- WSL2 recommended on Windows
- Git

No local PHP, Composer or MariaDB installation is required.

## Local Setup

Clone the repository:

```
git clone <repository-url>
cd hermertia-flarum
```

Create your local environment configuration:

```
cp .env.example .env
```

Then start the containers:

```
docker compose up -d --build
```

Check that both containers are running:

```
docker compose ps
```

The forum will be available at:

```
http://localhost:8000
```


## First-Time Flarum Setup

On a fresh database, visiting `http://localhost:8000` will open the Flarum installation screen.

For the local database use:

```
Database host:     db
Database name:     flarum
Database username: flarum
Database password: <value from .env>
```

Complete the remaining forum and administrator configuration through the installer.

## Useful Commands

Start the environment:

```
docker compose up -d
```

Stop it:

```
docker compose down
```

Rebuild the web container:

```
docker compose up -d --build
```

View logs:

```
docker compose logs -f
```

Open a shell in the Flarum container:

```
docker compose exec web bash
```

Run the Flarum CLI:

```
docker compose exec web php flarum
```

Clear the Flarum cache:

```
docker compose exec web php flarum cache:clear
```

Run Composer:
```
docker compose exec web composer install
```

## Project Structure

```
hermertia-flarum/
├── src/             # Flarum application
├── Dockerfile       # PHP/Apache development image
├── apache.conf      # Apache configuration
├── compose.yml      # Local Docker services
├── .env.example     # Example local configuration
└── README.md
```

## Development

Application source should be edited inside src/. The directory is bind-mounted into the web container, so local changes are immediately available to the running Flarum environment.

Database data is stored separately in a Docker-managed volume and should not be committed to the repository.




