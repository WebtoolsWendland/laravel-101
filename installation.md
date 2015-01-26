# Installation

## Environment Configuration

Laravel 5 now utilise `.env` file to store environment configuration, instead of cascading filesystem approach for Configuration. 

> Read <http://12factor.net/config>

## Predefined .env

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=QyI6BKDLCkhus6x5VQ5QNAeHaOo16weK

DB_HOST=127.0.0.1
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

CACHE_DRIVER=file
SESSION_DRIVER=file
```

> `.env` is using `.ini` style configuration setting (similar to `php.ini`) and managed using <https://github.com/vlucas/phpdotenv>.

