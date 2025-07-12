# Drupal 11 Development Environment

This document outlines the steps to set up and manage your Drupal 11 development environment using Docker.

## Prerequisites

Before you begin, ensure you have the following installed:

*   **Docker Desktop:** [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

## Getting Started

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd d11php # Or your project directory name
    ```

2.  **Start the Docker containers:**
    This command will build the necessary Docker images (if not already built) and start all the services (Nginx, PHP-FPM, MySQL, phpMyAdmin) in detached mode.
    ```bash
    docker-compose up -d --build --force-recreate
    ```

    *Note: The `--build` flag forces a rebuild of the images, and `--force-recreate` forces recreation of containers, ensuring all latest changes are applied.*

## Accessing the Services

Once the containers are up and running, you can access your services at the following URLs:

*   **Drupal 11 Site:** [http://localhost:8080](http://localhost:8080)
*   **phpMyAdmin:** [http://localhost:8081](http://localhost:8081)

## Database Access (phpMyAdmin)

To log in to phpMyAdmin:

*   **Server:** `db`
*   **Username:** `root`
*   **Password:** `rootpassword`

### Importing a Database

1.  Go to [http://localhost:8081](http://localhost:8081) and log in.
2.  Select the `drupal` database from the left sidebar.
3.  Click on the "Import" tab.
4.  Choose your `.sql` file and click "Go".

## Running Drush Commands

To execute Drush commands, you need to run them inside the `web` container. Use the following format from your project's root directory:

```bash
docker-compose exec web drush <your-drush-command>
```

**Example: Clear Drupal cache**
```bash
docker-compose exec web drush cr
```

## Stopping the Services

To stop and remove all the running containers, networks, and volumes (including persistent database data):

```bash
docker-compose down -v
```

To stop containers without removing volumes (useful if you want to preserve your database data):

```bash
docker-compose down
```

## Troubleshooting

If you encounter issues, here are some common troubleshooting steps:

*   **Check container status:**
    ```bash
    docker-compose ps
    ```
*   **View logs for a specific service (e.g., `web` or `nginx`):**
    ```bash
    docker-compose logs web
    docker-compose logs nginx
    docker-compose logs db
    ```
*   **Rebuild and restart all services (clean slate):**
    ```bash
    docker-compose down -v
    docker-compose up -d --build --force-recreate
    ```
