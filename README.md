# Mastodon setup
This docker will setup Mastodon on your server.
To use this configuration, you will have to also run the `traefik-docker` project available [here](https://github.com/m1rkwood/traefik-docker).

## Envionment
Duplicate the `.env.template` file and rename it to `.env`
Fill the information & fill the information for each.
Don't forget to point the chosen DNS (SUB_DOMAIN/DOMAIN) to your server IP.

## Run the containers for the first time
Before you start, you need to change the permissions of the `provision.sh` file so that it can be executed when the containers start:
- `chmod +x provision.sh`

Start the containers (with logs)
- `docker-compose up -d && docker-compose logs -f`
You can monitor the logs while it's starting, just to make sure nothing suspicious happens. To exit the logs, do `ctrl+c`.
The script `provision.sh` will migrate the database before starting the application.

Create an Owner account & make the public directory writable by the application:
- `docker exec -it mastodon-web bash`
- `bin/tootctl accounts create $MASTODON_ADMIN_USERNAME --email $MASTODON_ADMIN_EMAIL --confirmed --role Owner`

Make the `/public` directory writable for the application (log in as root)
- `docker exec -it -u root mastodon-web bash`
- `chown -R 991:991 public/system`
