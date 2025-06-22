The backend system has three major components:

1. **REST API Server** - Flask-based web server providing HTTP REST endpoints for system configuration and status
2. **Monitor Service** - Core monitoring daemon handling hardware I/O, real-time clock, GSM communication, and system state management  
3. **PostgreSQL Database** - Persistent storage for configurations, user data, alerts, and system logs


## Source code

The source code of the backend system:
 [arpi_server](https://github.com/ArPIHomeSecurity/arpi_server).
It is a sub-module of the arpi_management project:
[arpi_management](https://github.com/ArPIHomeSecurity/arpi_management.git)

You find how to get the source code [here](index.md#getting-the-code)!

## Architecture

```mermaid
erDiagram
  NGINX }|--|{ WEBAPP-SOURCE : "static files"
  NGINX }|--|| SERVER : "REST API"
  NGINX }|--|| MONITOR : SOCKET-IO
  SERVER ||--|| MONITOR : IPC-SOCKET
  SERVER {
    type flask
  }
  MONITOR }|--|| DATABASE : psycopg2
  MONITOR {
    type python-threading
    server socket-io
  }
  SERVER }|--|| DATABASE : psycopg2
  DATABASE {
    type postgresql
  }
```

## Port Configuration

| Connection | Development | Production |
|------------|-------------|------------|
| NGINX communication | 4200 | 80, 443 |
| SERVER REST API | 8080 | file socket |
| MONITOR socket-io | 8081 | 8081 |
| DATABASE psycopg2 | 5432 | 5432 |

## Preparing the database for development

When you want to run the system on your local machine you have to prepare the database content first.
The database needs a password for the service user (called argus). You have to update the value 
for DB_PASSWORD in server/etc/secrets.env.

```bash
# start the database
./scripts/start_database.sh
# prepare the users and tables
pipenv run flask init-db
pipenv run flask migrate
pipenv run flask upgrade
# prepare a configuration
pipenv run src/data.py -d -c test_01
```

## Starting the backend services in development mode

You can run the backend services in development mode locally with mock adapters.

```bash
# go to the server folder
cd server
# start the database
./scripts/start_database.sh
# start the REST API
pipenv run flask run
# or
pipenv run start-server

# in another terminal start the monitoring service
pipenv run python -d -s -m monitor
# or
pipenv run start-monitor
```

REST API is available on: http://localhost:8080

## Deploying the backend services to Raspberry

```bash
# go to the arpi_management project
pipenv run ./install.py -vpe prod server
pipenv run ./install.py -vpe prod monitor
```

## Starting the backend services in production mode

On the Raspberry PI the backend services can be managed as systemd services.

```bash
sudo systemctl start argus_server
sudo systemctl start argus_monitor
```
