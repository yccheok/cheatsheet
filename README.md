# Docker

Download Django to local
    
    C:\yocto\snapweb>docker-compose run --rm -v %cd%/django:/app -w /app django django-admin.py startproject web .
    (https://docs.docker.com/compose/django/#create-a-django-project)
    
Run Django manage script
    
    C:\yocto\snapweb>docker-compose run --rm -v %cd%/django:/app -w /app django python /app/manage.py changepassword root
    C:\yocto\snapweb>docker-compose run --rm -v %cd%/django:/app -w /app django python /app/manage.py startapp accounts
    C:\yocto\snapweb>docker-compose run --rm -v %cd%/django:/app -w /app django python /app/manage.py makemigrations
    
Generate empty migration file

    C:\yocto\jstock-insider>docker-compose run --rm -v %cd%/django:/app -w /app django python /app/manage.py makemigrations users --empty -n alter_ts_default_to_now
    
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

Went into db container
    
    docker-compose exec db bash
   
Login to localhost as user "postgres"

    psql -h localhost -U postgres
    
List all databases

    postgres-# \l
    
Use a database

    postgres-# \c postgres 
    
List all tables

    postgres-# \dt   


