# App Store URL
1. https://apps.apple.com/app/id1562256136 - WeNote
   
2. https://apps.apple.com/app/id6670156126 - Melonote
   
# How to remove a cloud storage account safety
1. select * from customer where email = 'xxx';
2. UPDATE customer SET enabled = false WHERE id = 1;


# Cloud Storage Server Maintenance

1. Use `htop` to check available memory. (Current free memory: 500 MB)
2. Use `df -h --output=avail /` to check available disk space. (Currently: 34 GB free)
3. Do not use `docker-compose restart`, as it will cause downtime. Instead, use: `docker-compose up -d --force-recreate --build`
4. Run the same command for Traefik: `docker-compose up -d --force-recreate --build`
5. Verify the service is running at: https://.../info


# Dockerfile

    # Build
    docker build -t worker-faster_whisper .
    # Run
    docker run -it worker-faster_whisper bash
    
# A Beginner's Guide to Testing In-App Purchases in the Sandbox Environment
1. Using a real device is **mandatory**.
2. Log out of the current account on the real device.
3. Log in to the real device using a sandbox account.
4. Sandbox accounts can be found at: https://appstoreconnect.apple.com/access/users/sandbox.
5. To clear the purchase history, select the sandbox account at https://appstoreconnect.apple.com/access/users/sandbox and click the "Clear Purchase History" button.
6. In real device, go to Settings/ App Store/ Sanbox Account to simulate subscription cancellation.
7. To simulate a refund scenario, use the following code snippet:

---
    // Initialize the transaction variable in the listenForTransactions and purchase functions within the Store class.
    var transction: Transaction?
    
    func refund() async {
        if let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene {
            do {
                let status = try await transction?.beginRefundRequest(in: windowScene)
            } catch {
                print("Failed to begin refund request: \(error)")
            }
        }
    }

# Short URL

    Melonote - https://apple.co/3Vs4br9
    
# Kill Firebase emulator port occupy
    kill -9 $(lsof -t -i :8085)
    lsof -i :8085
    kill -9 <PID>

# Firestore
    # Update index file
    firebase firestore:indexes
    
# Firebase
    firebase init
    
    firebase emulators:start
    kill -9 $(lsof -t -i :8085); firebase emulators:start
    
    firebase deploy
    
# Python

    # Create virtual env
    python3 -m venv env

    # Activate virtual env
    source env/bin/activate

    # Install all packages
    pip install -r requirements.txt

    # List down all installed packages
    pip list
  
# Update WeNote Cloud user paid status

    select * from customer where id = 1;
    select * from customer_google_subscription where fk_customer_id = 1;
    select payment_state from google_subscription where id = 1;
    select * from paid_customer where id = 1;

    # DANGEROUS COMMAND!
    UPDATE google_subscription SET payment_state = 1 WHERE id = 1;

# Command to keep the container running (For easy debugging)
    CMD ["tail", "-f", "/dev/null"]

# How to restore SQL dump file from production?

    1) Place pg_dump-20240129_000002.sql in postgres folder.
    
    2) Change postgres/Dockerfile to
    
        FROM postgres:13.3
    
        RUN mkdir /postgres_logs
        RUN chown postgres:postgres /postgres_logs
    
        ENV POSTGRES_DB wenote_cloud_storage
    
        ADD postgres.sql /docker-entrypoint-initdb.d/
    
    
        COPY . /app
        WORKDIR /app
    
    3) docker-compose exec postgres bash

    4) psql -h localhost -U postgres

    ⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️
    5) ⚠️⚠️⚠️ drop DATABASE wenote_cloud_storage; ⚠️⚠️⚠️
    ⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️⚠️
    
    6) create DATABASE wenote_cloud_storage;

    7) exit
    
    8) psql -U postgres wenote_cloud_storage < pg_dump-20240129_000002.sql


# How to capture images for the onboarding screen in iOS?

1. Use an iPhone SE (3rd generation) with iOS 16.2.
2. Set the font size to Large.
3. Capture a screenshot in the simulator with the size of 750x1334 pixels.
4. Use Gimp to edit the screenshot down to a region with the size of 750x1024 pixels.


# Replicate a bug seen when installing an app via App Bundle from the Google Play store?
    // Generate APKs.
    bundletool build-apks --bundle=~/Desktop/com.yocto.wenote-536-5.36-release.aab --output=~/Desktop/output.apks --ks=~/yocto/my-release-key.jks --ks-key-alias=yocto

    // Install APK to connected device. Connected device can be an emulator.
    bundletool install-apks --apks=~/Desktop/output.apks
    
# Create custom Java runtime image

    jlink --no-header-files --no-man-pages --compress=2 --strip-debug --module-path "C:\Program Files\Zulu\zulu-17\jmods" --add-modules java.base,java.datatransfer,java.desktop,java.logging,java.naming,java.prefs,java.rmi,java.security.sasl,java.sql,java.xml,javafx.base,javafx.controls,javafx.graphics,javafx.media,javafx.swing,javafx.web,jdk.jsobject,jdk.unsupported,jdk.crypto.ec --output jre

# Find all dependencies

    C:\Users\yccheok\Desktop\jstock>jdeps --ignore-missing-deps --list-deps jstock.jar lib\*.jar
    Warning: split package: javax.xml jrt:/java.xml lib\stax-api-1.0.1.jar lib\xml-apis.jar
    Warning: split package: javax.xml.datatype jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.namespace jrt:/java.xml lib\stax-api-1.0.1.jar lib\xml-apis.jar
    Warning: split package: javax.xml.parsers jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.stream jrt:/java.xml lib\stax-api-1.0.1.jar
    Warning: split package: javax.xml.stream.events jrt:/java.xml lib\stax-api-1.0.1.jar
    Warning: split package: javax.xml.stream.util jrt:/java.xml lib\stax-api-1.0.1.jar
    Warning: split package: javax.xml.transform jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.transform.dom jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.transform.sax jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.transform.stream jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.validation jrt:/java.xml lib\xml-apis.jar
    Warning: split package: javax.xml.xpath jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom jrt:/java.xml lib\xml-apis.jar lib\xom-1.1.jar
    Warning: split package: org.w3c.dom.bootstrap jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.css jrt:/jdk.xml.dom lib\xml-apis.jar
    Warning: split package: org.w3c.dom.events jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.html jrt:/jdk.xml.dom lib\xercesImpl.jar lib\xml-apis.jar
    Warning: split package: org.w3c.dom.ls jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.ranges jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.stylesheets jrt:/jdk.xml.dom lib\xml-apis.jar
    Warning: split package: org.w3c.dom.traversal jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.views jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.w3c.dom.xpath jrt:/jdk.xml.dom lib\xml-apis.jar
    Warning: split package: org.xml.sax jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.xml.sax.ext jrt:/java.xml lib\xml-apis.jar
    Warning: split package: org.xml.sax.helpers jrt:/java.xml lib\xml-apis.jar
       java.base
       java.datatransfer
       java.desktop/sun.awt.geom
       java.logging
       java.naming
       java.prefs
       java.rmi
       java.security.sasl
       java.sql
       java.xml/com.sun.org.apache.xerces.internal.parsers
       java.xml/com.sun.org.apache.xerces.internal.util
       java.xml/com.sun.org.apache.xerces.internal.xni.parser
       javafx.base/com.sun.javafx.collections
       javafx.base/com.sun.javafx.event
       javafx.base/com.sun.javafx.runtime
       javafx.controls/com.sun.javafx.scene.control
       javafx.controls/com.sun.javafx.scene.control.behavior
       javafx.graphics/com.sun.javafx.css
       javafx.graphics/com.sun.javafx.scene.traversal
       javafx.media
       javafx.swing
       javafx.web/com.sun.javafx.webkit
       javafx.web/com.sun.webkit
       jdk.jsobject
       jdk.unsupported

An additional dependency `jdk.crypto.ec` is required, due to runtime error when we are trying to perform news fetching - https://stackoverflow.com/questions/54770538/received-fatal-alert-handshake-failure-in-jlinked-jre/54785281#54785281

# How to execute JStock

    C:\Users\yccheok\Desktop\jstock>jre\bin\java.exe -Dsun.java2d.dpiaware=false -Xms64m  -Xmx512m --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang.reflect=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.desktop/java.awt.font=ALL-UNNAMED --add-opens java.desktop/java.awt=ALL-UNNAMED -jar jstock.jar

# Rounded corner ripple effect

    <?xml version="1.0" encoding="utf-8"?>
    <ripple android:color="?android:colorControlHighlight"
        xmlns:android="http://schemas.android.com/apk/res/android">
        <item android:id="@android:id/mask">
            <shape android:shape="rectangle">
                <corners android:topLeftRadius="16dp" android:topRightRadius="16dp"
                    android:bottomLeftRadius="0dp" android:bottomRightRadius="0dp" />
                <solid android:color="@android:color/white" />
            </shape>
        </item>

        <item>
            <shape android:shape="rectangle">
                <corners android:topLeftRadius="16dp" android:topRightRadius="16dp"
                    android:bottomLeftRadius="0dp" android:bottomRightRadius="0dp" />
                <solid android:color="@color/white_90" />
            </shape>
        </item>
    </ripple>

# How to have a fullscreen Android app

1. Apply `app:elevation="0dp"` in AppBarLayout.
2. Apply `android:background="@android:color/transparent"` in AppBarLayout and Toolbar.
3. Apply `<style name="Theme.MyApplication.AppBarOverlay" parent="ThemeOverlay.AppCompat.ActionBar" />` in AppBarLayout so that we are getting black title.
4. Apply `<item name="android:windowLightStatusBar">true</item>` in Theme.MyApplication so that we are getting black status bar icon.
5. Apply the following code in MainActivity's onCreate (Before super).

---

    Window w = getWindow();
    w.setFlags(WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS, WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS);



# Generate 1242 x 2208 screenshot for App Store

1. Use iPhone 8 Plus simulator to generate 1242 x 2208 raw screenshot.
2. Use https://www.appstorescreenshot.com/

# Generate 1284 x 2778 screenshot for App Store

1. Use iPhone 11 Pro Max simulator to generate 1242 x 2688 raw screenshot. (The reason we are using the iPhone 11 family is that at https://screenshots.pro, only the iPhone 11 has a minimalist design.)
2. Use https://screenshots.pro/

![](https://i.imgur.com/xNRHXpO.png)

![](https://i.imgur.com/dS1l8Qu.png)

Or, a better way is to login with Google account. Then, use the old template

https://screenshots.pro/editor?template_id=67d0b0ae-c2b9-40a6-9e90-3ed8b7af614f


    Position X : 56.41658961175087
    Position Y : 359.3928890266867
    Width : 1173.1307603212942
    Height : 2416.440725382908

![](https://i.imgur.com/9nKUXWE.png)

# Find error in iOS string resource file
    plutil -lint Localizable.strings

# Link to rate iOS WeNote app

    https://apps.apple.com/app/id1562256136?action=write-review

    https://apps.apple.com/tw/app/id1562256136?l=zh_tw

# Using data from production iCloud

https://stackoverflow.com/a/40414108/72437

# Print dependency tree

In Android Studio's terminal, type the following command

    ./gradlew app:dependencies
    ./gradlew jstockandroid:dependencies
    
Whether using "app" or "jstockandroid", is depending on the folder name found in the project.

# Debug multi sync feature

    // This is old format
    //select * from notification where request->>'to' in (select token from google where email = 'yancheng.cheok@gmail.com') order by ts desc;

    select * from notification where request->'message'->>'token' in (select token from google where email = 'yancheng.cheok@gmail.com') order by ts desc;
    
    select email from google where token in (select request->'message'->>'token' from notification where id >= 3030128 AND id <= 3030157);
    
# How to test on Android Auto Backup feature

1. Upload app into phone via Android Studio.
2. Write some text, attach some images, attach some voices.
3. Execute the following code in Android Studio's terminal

       adb shell bmgr backupnow com.yocto.wenote
       
   You should able to observe backup progress log
   
4. Uninstall the app from device.
5. Upload app into phone via Android Studio. We should observe the old data is still there.
       
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

    docker-compose.xml
    
      nginx:
        ...
        ports:
          - "80:80"
        ...
    
      flask:
        ...
        #
        # FOR DEVELOPMENT
        #
        volumes:
            - ./flask/:/app
        ...
    
    flask/Dockerfile
    
        CMD /usr/local/bin/gunicorn --workers=5 main:app -b 0.0.0.0:5000 --error-logfile=/var/log/gunicorn3.err.log --reload   

Get Python logging in Flask
    
    Use the following code to perform printing in Flask: print("This is message", flush=True)
    docker-compose logs -f
    
# Postgres

Went into db container
    
    docker-compose exec postgres bash
   
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

Check user subscription

    select * from google_subscription where (subscription_info->>'orderId') = 'GPA.3383-0878-7727-50427'; (expired)

    select * from google_subscription where (subscription_info->>'orderId') = 'GPA.3359-8897-6679-16612'; (active)

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
    
