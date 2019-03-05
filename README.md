Docker for OpenWebAnalytics
===========================

# OWA

Opensource version of Google Analytics. See: http://www.openwebanalytics.com/

# How to

### Build

```
$ docker-compose build owa
```

Changing `OWA` version in `docker-compose.yml`, if needed.

### Run

```
$ docker-compose up -d percona
$ docker-compose up -d owa
```

# Change OWA configuration

Change configuration with the `env` variables:

```
ENV OWA_DB_TYPE        "mysql"
ENV OWA_DB_HOST        "localhost:3306"
ENV OWA_DB_NAME        "owa"
ENV OWA_DB_USER        "owa"
ENV OWA_DB_PASSWORD    "owa"
ENV OWA_PUBLIC_URL     "http://localhost:80/"
ENV OWA_NONCE_KEY      "owanoncekey"
ENV OWA_NONCE_SALT     "owanoncesalt"
ENV OWA_AUTH_KEY       "owaauthkey"
ENV OWA_AUTH_SALT      "owaauthsalt"
ENV OWA_ERROR_HANDLER  "development"
ENV OWA_LOG_PHP_ERRORS "false"
ENV OWA_CACHE_OBJECTS  "true"
```

Change these variables in `Dockerfile` (need to rebuild image) or add to `docker-compose.yml` (need to restart container)
* Caution: `OWA_PUBLIC_URL` should be ended with `/`
