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

- Apache web-server:
  - http://localhost/phpinfo.php
  - https://localhost/phpinfo.php
- Mailhog: http://localhost:8025/
- PhpMyAdmin: http://localhost:8010/
- Adminer: http://localhost:8020/

## XDebug

Настройки XDebug для php 8.2 - `configs/php8.2/docker-php-ext-xdebug.ini`
Для работы с VSCode нужно установить расширение `PHP Debug` и указать следующие параметры в `www/.vscode/launch.json`

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "hostname": "127.0.0.1",
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}"
            }
        }
    ]
}
```
