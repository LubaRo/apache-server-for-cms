# Docker based development environment for Web Sites:

- PHP versions: 5.3, 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.2;
- MySQL 5.7, MySQL 8.4;
- apache web server.

## Requirements

- Docker
- docker-compose

## Run the environment using docker:

```bash
  make up
```

## Run the interacitve bash of the server

```bash
  make bash
```

## Apache

The root directory `www`. So put the web site files there.

## Sending e-mails

There is Mailhog included. So to catch the emails by mailhog setup your site in admin panel. Go to `Settings -> E-mails` (depends on CMS) and setup next fields:

- `Method of sending e-mails:` -> `via SMTP server`
- `SMTP host` -> `127.0.0.1:1025`

## Database

All mysql data is stored in db_data folder. So it is persisted despite the state of containers.

### MySQL credentials:

Username: `root`

Password: `root`

## Result

- Apache web server on ports 80 and 443:
  - http://localhost/phpinfo.php
  - https://localhost/phpinfo.php
- Mailhog: http://localhost:8025/
- PhpMyAdmin: http://localhost:8010/
- Adminer: http://localhost:8020/

## XDebug

XDebug configuration specifieced for php 7.4 in `configs/php7.4/docker-php-ext-xdebug.ini`
To setup it in VSCode install `PHP Debug` extension and specify for each store the next settings in `www/<app_name>/.vscode/launch.json`

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9003,
      "pathMappings": {
        "/var/www/html/<app_name>": "${workspaceFolder}"
      }
    }
  ]
}
```
