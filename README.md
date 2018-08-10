# Docker

Download Django to local
    
    docker-compose run web django-admin.py startproject composeexample .
    (https://docs.docker.com/compose/django/#create-a-django-project)
    
Enable/disable Hyper-V

    bcdedit /set hypervisorlaunchtype off (Disable to run Android emulator)
    bcdedit /set hypervisorlaunchtype auto (Enable to run Docker)
    
Use tools from Docker to process data in host machine

    docker run --rm -v $(pwd):/app -w /app php:cli php hello.php (Linux)
    docker run --rm -v %cd%:/app -w /app php:cli php hello.php (Windows)
    
    docker run --rm -v $(pwd):/app -w /app composer/composer create-project --prefer-dist laravel/laravel html (Linux)
    docker run --rm -v %cd%:/app -w /app composer/composer create-project --prefer-dist laravel/laravel html (Windows)
    
Remove all images from PowerShell

    docker stop $(docker ps -a -q)
    docker ps -a -q | % { docker rm $_ }
    docker images -q | % { docker rmi $_ }
    docker volume prune

# Postgres

Login to localhost as user "postgres"

    psql -h localhost -U postgres
    
List all database

    postgres-# \l
