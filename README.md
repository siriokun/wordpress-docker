# WordPress Docker with correct file permission

1. Clone this repo
2. cd `wordpress-docker`
3. run `docker-compose up -d`
4. run `docker ps`

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
2bb5949a7e8d        wordpress:latest    "docker-entrypoint.s…"   41 minutes ago      Up 23 minutes       0.0.0.0:2021->80/tcp                wp
2216ce37099f        mysql:5.7           "docker-entrypoint.s…"   41 minutes ago      Up 23 minutes       3306/tcp, 0.0.0.0:2022->33060/tcp   wp-db
```

5. Login to your dcker container, in this case CONTAINER ID of `wp` container,

```bash
docker exec -it 2bb5949a7e8d bash
```

Run these commands inside this container,

```bash
chown -R www-data:www-data /var/www
```

```bash
find /var/www/ -type d -exec chmod 0755 {} \;
```

```bash
find /var/www/ -type f -exec chmod 644 {} \;
```

```bash
exit
```

6. After exit from container, restart container with `docker-compose restart`

7. Complete WordPress installation when you open `http://localhost:2021`

8. Now you can install themes or plugins from within wp-admin.