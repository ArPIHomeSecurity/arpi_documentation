The backend system has two major components:

1. The server provides the REST API to communicate with the web application
2. The monitor implements the main functionality (IO handling, RTC, GSM...)

## The server

## The monitor

## Preparing the database for development

When you want to run the system on your local machine you have to prepare the database content first.
The database needs a password for the service user (called argus). You have to update the value 
for DB_PASSWORD in server/etc/secrets.env.

```bash
# start the database
./scripts/start_database.sh dev
# prepare the users and tables
./scripts/update_database_struct.sh dev
# prepare a configuration
./scripts/update_database_data.sh dev test_01
```

## Starting the backend services in development mode

You can run the backend services in development mode locally with mock adapters.

```bash
# go the server folder
cd server
# start the database
./scripts/start_server.sh dev
# start the REST API (it also serves the web application)
./scripts/start_server.sh dev
# start the monitoring service
./scripts/start_monitor.sh dev
```

## Starting the backend services in production mode

On the Raspberry PI the backend service can be managed as systemd services.

```bash
sudo systemctl start argus_monitor
```
