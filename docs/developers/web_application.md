The user interface of the security system is implemented in angular. This web application
can be used in different modes.

1. Normal mode: the application uses the backend services
2. Demo mode: the application uses the mock services replacing the backend

The demo mode is for running on GitHub pages ([demo](https://demo.arpi-security.info)).

## Source code

The source code of the backend system:
[https://github.com/ArPIHomeSecurity/arpi_webapplication](https://github.com/ArPIHomeSecurity/arpi_webapplication).
It is a sub-module of the arpi_management project:
[https://github.com/ArPIHomeSecurity/arpi_management.git](https://github.com/ArPIHomeSecurity/arpi_management.git)

You find how to get the source code [here](index.md#getting-the-code)!

## Normal mode

In normal mode you can build the web application and you can host localized version with Nginx.

### Development

Building and running:
```bash
# building the application with locales
ng build --localize
# start serving the web application on http://localhost:4200
DIST=dist-development npm run serve

# serve english only
ng serve --watch --poll 2000
```

### Production


Building locally:
```bash
# building the application with locales
ng build --configuration=production --localize
```

Deploying to Raspberry:
```bash
# go the arpi_management project
pipenv run ./install.py -vpe prod webapplication
```

Running on Raspberry:
```bash
sudo systemctl start nginx
```

## Demo mode

In the demo mode the application can be run as a standalone application without backend the service.

### Development

This mode is for running the web application in demo development mode locally with
a mock REST API.

```bash
# building the application with locales
ng build --configuration=demo-dev --localize
# start serving the web application on http://localhost:4200
DIST=dist-demo-dev npm run serve

# serve english only
ng serve --configuration=demo-dev --watch --poll 2000
```

### Production

This mode is for running the web application in demo mode on GitHub pages.

```bash
# building the application with locales
ng build --configuration=demo --localize
# start serving the web application on http://localhost:4200
DIST=dist-demo npm run serve

# serve english only
ng serve --configuration=demo --watch --poll 2000
```

## Translations

You can update the translations of the application with the following command.

```bash
npm run extract-i18n
```

The translations are stored in "webapplication/src/locales".

Use [POEDIT](https://poedit.net/) to manage translations.

!!! todo
    Document adding new translations
