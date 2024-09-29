# nextcloud docker compose
Nextcloud deployment via docker compose 

What we use:

nextcloud

mariadb - database

swag - certificate

duckdns - domain

Pre-requisites 

First we will need to create an acoount in duckdns from here:
https://www.duckdns.org/
Register your domain name and IP and open ports 443 and 80 to that IP.
Once all this is done copy the token for the DuckDNS site and paste it in the yaml file under DUCKDNSTOKEN.
Everything else with " " is custom information that you need to replace.
Also /path/to/folder is information that needs to be adjusted according to the enviroment you use.

Installation

After everything is corrected in the yaml file we will need to use:
-docker compose pull
-docker compose up -d
These two commands will pull the images and deploy the containers.
To verify everything is up use:
-docker ps
You should see three containers nextcloud , swag and mariadb.
Now we find the file named nextcloud.subdomain.conf.sample under SWAG's /config/nginx/proxy-confs folder and rename it to nextcloud.subdomain.conf, then restart the SWAG container .
The restart can be done with:
-docker stop swag
-docker compose up -d 


If this is the first time we are accessing Nextcloud (we've never accessed it locally before), we can simply navigate to https://nextcloud.example.duckdns.org and we should see the Nextcloud set up page.
We'll fill out the info, use the mariadb user and the password we selected in the environment variable and we'll use mariadb as the Database Host address (container name as dns hostname).

If more information is needed please check this site as I used it for my deployment:
https://docs.linuxserver.io/general/swag/#nextcloud-subdomain-reverse-proxy-example
