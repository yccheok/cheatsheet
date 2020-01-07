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

Clean Git checkout from master and overwrite everything

    git fetch --all; git reset --hard origin/master
       
Clean up docker log

    truncate -s 0 /var/lib/docker/containers/*/*-json.log
    
Clean build on images in case something went wrong

    docker-compose up -d --force-recreate --build
    
Clear redis cache

    docker exec -it jstockiex_redis_1 redis-cli FLUSHALL

# Postgres

Went into db container
    
    docker-compose exec postgres sh
   
Login to localhost as user "postgres"

    psql -h localhost -U postgres
    
List all databases

    postgres-# \l
    
Use a database

    postgres-# \c jstock_iex 
    
List all tables

    postgres-# \dt   

Check whether news notifications are being sent today

    select ts from notification where (request->'data'->'news_alerts') is not null order by ts desc limit 100;
    
    
# Facebook

Add debug key to Facebook

    c:\yocto>keytool -exportcert -alias androiddebugkey -keystore c:\Users\yccheok\.android\debug.keystore | c:\openssl-0.9.8k_X64\bin\openssl.exe sha1 -binary | c:\openssl-0.9.8k_X64\bin\openssl.exe base64
    Enter keystore password:  android
    
# Google

Add debug key to Google

    c:\yocto>keytool -exportcert -list -v -keystore c:\Users\yccheok\.android\debug.keystore
    Enter keystore password:  android
