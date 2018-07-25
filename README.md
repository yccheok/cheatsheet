# Docker

Use tools from Docker to process data in host machine

    docker run --rm -v $(pwd):/app -w /app php:cli php hello.php (Linux)
    docker run --rm -v %cd%:/app -w /app php:cli php hello.php (Windows)
    
    docker run --rm -v $(pwd):/app -w /app composer/composer create-project --prefer-dist laravel/laravel html (Linux)
    docker run --rm -v %cd%:/app -w /app composer/composer create-project --prefer-dist laravel/laravel html (Windows)
    
# Postgres

Login to localhost as user "postgres"

    psql -h localhost -U postgres
    
List all database

    postgres-# \l
