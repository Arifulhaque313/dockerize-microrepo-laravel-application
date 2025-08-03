# Laravel Project Dockerized 

A Laravel application running with Docker, using Nginx, PHP, and MySQL.

## Prerequisites

Before you begin, ensure you have the following installed:
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Git](https://git-scm.com/downloads)

## Getting Started

### 1. Clone the Repository

```bash
# Clone the repository
git clone https://github.com/Arifulhaque313/dockerize-microrepo-laravel-application.git

# Navigate to the project directory
cd dockerize-microrepo-laravel-application
```

### 2. Environment Setup

```bash
# Copy the example env file
cp .env.example .env

# Update the following variables in .env file
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=laravel
```

### 3. Build and Run Docker Containers

```bash
# Build and start the containers in detached mode
docker compose up -d

# Install PHP dependencies
docker compose exec laravel-app composer install

# Generate application key
docker compose exec laravel-app php artisan key:generate
```

### 4. Database Setup

```bash
# Run database migrations
docker compose exec laravel-app php artisan migrate

# (Optional) Seed the database
docker compose exec laravel-app php artisan db:seed
```

## Docker Container Structure

The project contains the following containers:
- **app**: PHP-FPM container for Laravel application
- **nginx**: Nginx web server
- **mysql**: MySQL database

## Available Services

| Service | Port |
|---------|------|
| Application | `http://localhost:8081` |
| MySQL | `3306` |

## Useful Commands

### Docker Commands

```bash
# Start containers
docker compose up -d

# Stop containers
docker compose down

# View container logs
docker compose logs -f

# Access PHP container shell
docker compose exec laravel-app bash

# List running containers
docker compose ps
```

### Laravel Commands

```bash
# Clear application cache
docker compose exec laravel-app php artisan cache:clear

# Run migrations
docker compose exec laravel-app php artisan migrate

# Create a new controller
docker compose exec laravel-app php artisan make:controller ControllerName

# Run tests
docker compose exec laravel-app php artisan test
```

## Development Workflow

1. Make changes to your code
2. The changes will be automatically reflected due to volume mapping
3. If you modify dependencies:
   ```bash
   docker compose exec laravel-app composer update
   ```
4. If you modify the database:
   ```bash
   docker compose exec laravel-app php artisan migrate
   ```

## Troubleshooting

### Common Issues and Solutions

1. **Permission Issues**
   ```bash
   # Fix storage permissions
   docker compose exec laravel-app chown -R www-data:www-data storage
   docker compose exec laravel-app chmod -R 775 storage
   ```

2. **Container Won't Start**
   ```bash
   # Check logs
   docker compose logs

   # Rebuild containers
   docker compose up -d --build
   ```

3. **Database Connection Issues**
   - Ensure MySQL container is running
   - Check .env database credentials
   - Wait a few seconds after container startup for MySQL to initialize

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
