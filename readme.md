# docker-d8-lemp-ssl

Docker build for creating a local Drupal 8 website running on a LEMP stack with SSL from Lets Encrypt. Includes a PHPMyAdmin container so you have a GUI for the database. Extends the official Drupal image on Docker Hub by installing APCu caching. Includes MailHog, a testing SMTP server, so you can test site messaging locally.

### Install Drupal using Composer
Adding COMPOSER_MEMORY_LIMIT=-1 to the beginning of the command helps to avoid composer memory limit issues. Change the version number to the version of Drupal you need to use.

``` COMPOSER_MEMORY_LIMIT=-1 composer create-project drupal/recommended-project:8.9.6 drupal ```

### Start up the Containers
``` docker-compose up -d ```

### Access Site
``` https://localhost ```

(or at the custom URL that you create using the instructions in the comments near the https-portal container :wink:)

### Access PHPMyAdmin
``` http://localhost:8081 ```

### Preset PHPMyAdmin creds
<p><b>User:</b> drupal</p>
<p><b>Pass:</b> drupal</p>

### Access the testing mail server inbox
``` http://localhost:8025 ```

### Edit the nginx.conf file to whitelist your IP and block others
The IP address you are looking to whitelist comes from the <i>https-portal</i> container.

Find the container's ID by running: ``` docker ps ``` to see the list of running containers.

Then run this, replacing CONTAINER_ID with the ID: ``` docker inspect CONTAINER_ID | grep "IPAddress" ```

Uncomment lines 131-134 in nginx.conf and replace XXX.XX.X.X with the container IP address.

Run ``` docker-compose up ``` to commit the changes.
