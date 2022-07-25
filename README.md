# Emergency Action Plan when Digital Ocean Disk is Full

1. Go to jstock_notification folder
2. Clean up the /tmp folder in postgres_backup docker
3. Truncate notification and notification_data table in postgres docker

# iCloud Document

Monitor sync activities

    brctl log -w --shorten | grep CloudDocs
    
# Python
    
    C:\yocto\sandbox>python -m virtualenv venv
    C:\yocto\sandbox>venv\Scripts\activate.bat
    (venv) C:\yocto\sandbox>pip install requests
    (venv) C:\yocto\sandbox>python A.py
    
# Cloud Storage

Differnt provider profiles

    C:\Users\yccheok\.aws\credentials

List all files

    aws s3api list-object-versions --bucket wenote-b
    aws s3api list-object-versions --bucket wenote-b --profile space --endpoint-url https://fra1.digitaloceanspaces.com
    aws s3api list-object-versions --bucket wenote-b --profile wasabi --endpoint-url https://s3.eu-central-1.wasabisys.com
    
Inspect individual file

    aws s3api head-object --bucket wenote-b --key user-2/attachment/f995bdb4-691b-4c44-8a1f-dd348665da82.jpg
    aws s3api head-object --bucket wenote-b --key user-2/attachment/f995bdb4-691b-4c44-8a1f-dd348665da82.jpg --profile space --endpoint-url https://fra1.digitaloceanspaces.com
    aws s3api head-object --bucket wenote-b --key user-2/attachment/f995bdb4-691b-4c44-8a1f-dd348665da82.jpg --profile wasabi --endpoint-url https://s3.eu-central-1.wasabisys.com
    

# Android Studio

Clear app data

    adb shell pm clear com.yocto.wenote
    
# Python

Run Python in virtual environment

    python -m venv .
    Scripts\activate.bat
    
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

Clean build on ONE images in case something went wrong

    docker-compose up -d --force-recreate --no-deps --build flask
    
Clean build on ALL images in case something went wrong

    docker-compose up -d --force-recreate --build
    
Clear redis cache

    docker exec -it jstockiex_redis_1 redis-cli FLUSHALL

Remove postgres volume

    docker-compose down --volumes (DANGEROUS!!!)
    docker-compose up -d --force-recreate --build
    
    
Let Flask access local drive

    flask:
        #
        # FOR DEVELOPMENT (Not using internal network for volume mapping to work)
        #
        #networks:
        #    - internal
        #
        build:
            context: ./flask
            dockerfile: Dockerfile
        restart: always
        depends_on:
            - pgbouncer
        expose:
            - "5000"

        #
        # FOR DEVELOPMENT
        #
        volumes:
            - C:/xxx/flask:/app
        logging:
            driver: "json-file"
            options:
            max-file: "10"
            max-size: "10m"
            
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
    
Check table size usage

    select table_name, pg_relation_size(quote_ident(table_name))
    from information_schema.tables
    where table_schema = 'public'
    order by 2
    
Delete a row
    
    delete from notification where ts < timestamp '2020-08-20 00:00:00';
    
Claim back disk space

    vacuum full;

Restore from pgdump

    (PGPASSWORD="$DB_PASSWORD" pg_dump -c -h "$DB_HOST" "$DB_DB" -p "$DB_PORT" -U "$DB_USER" > $FILE)
    psql -h localhost -U postgres wenote_cloud_storage < /tmp/pg_dump-20210520_125646.sql
    
    (PGPASSWORD="$DB_PASSWORD" pg_dump -c -C -h "$DB_HOST" "$DB_DB" -p "$DB_PORT" -U "$DB_USER" > $FILE)
    psql -h localhost -U postgres < /tmp/pg_dump-20210520_131418.sql
    
# RabbitMQ
    
Check queues

    rabbitmqadmin -u <username> -p <password> list queues vhost name node messages message_stats.publish_details.rate

# Facebook

Add debug key to Facebook

    c:\yocto>keytool -exportcert -alias androiddebugkey -keystore c:\Users\yccheok\.android\debug.keystore | c:\openssl-0.9.8k_X64\bin\openssl.exe sha1 -binary | c:\openssl-0.9.8k_X64\bin\openssl.exe base64
    Enter keystore password:  android
    
# Google

Add debug key to Google

    c:\yocto>keytool -exportcert -list -v -keystore c:\Users\yccheok\.android\debug.keystore
    Enter keystore password:  android
    
# Google Play store screenshots
    Create an image 1242 x 2208
    Scale down screenshot size to 90% till 972 x 1728
    Place screenshot @ position x=135, y=345
    Use font Tahoma 84 Fixed (96 DPI)
    
# Google App Engine

    gcloud app deploy --project jstock-webapp app.yaml
    
