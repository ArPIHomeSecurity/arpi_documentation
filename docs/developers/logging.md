
Currently the services generate logs only to the standard output. In local development mode you can see all the logs on
the screen. The deployed services are executed with [`systemd`](https://systemd.io/).


## Backend 

The components of the backend system send the logs into different loggers.
You can change the logging levels in the `constans.py`.

```python
LOGGING_MODULES = [
    (LOG_SERVICE, INFO),
    (LOG_MONITOR, INFO),
    (LOG_IPC, INFO),
    (LOG_ALERT, INFO),
    (LOG_SOCKETIO, INFO),
    (LOG_NOTIFIER, INFO),
    (LOG_ADSENSOR, INFO),
    (LOG_ADRELAYS, INFO),
    (LOG_ADGSM, INFO),
    (LOG_ADKEYPAD, INFO),
    (LOG_SECCON, INFO),
    (LOG_SC_CERTBOT, INFO),
    (LOG_SC_DYNDNS, INFO),
    (LOG_SC_ACCESS, INFO),
    (LOG_CLOCK, INFO),
]
```

By default everything is configured to send only the `INFO` messages. If you want to get more detailed logging of a
component change it to `DEBUG` level.

!!! warning
    `DEBUG` level logs can be very verbose depending on the component.


## Server

The server component is a simple Flask application. It uses the default Flask logger. In local development mode the
default log level is `DEBUG`. In the deployed service the default log level is `INFO` and you can change it in the
systemd service file (/etc/systemd/system/argus_server.service).
