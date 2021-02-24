The user interface of the security system is implemented in angular. This web application
can be used in different modes.

1. Normal mode: the application uses the backend services
2. Demo mode: the application uses the mock services replacing the backend

The demo mode is for running on Gihub pages ([demo](https://demo.arpi-security.info)).

## Normal mode

In normal mode you can only build the web application and you need the backend system to use it.
[See running the backend system!](/developers/backend/#starting-the-backend-services-in-development-mode)

### Building for development

```bash
# setting the environment
export DIST=dist-development
# building the application
ng build --localize
# move default language to the root of the output folder
npm run postbuild
```

### Building for production

```bash
# setting the environment
export DIST=dist-production
# building the application
ng build --configuration=production --localize
# compress the files
npm run compress
# move default language to the root of the output folder
npm run postbuild
```

## Demo mode

In the demo mode the application can be run as a standalone application.

### Running in demo development mode

This mode is for running the web application in demo development mode locally with
a mock REST API.

```bash
# setting the environment
export DIST=dist-demo-dev
# building the application
ng build --configuration=demo-dev --localize
# move default language to the root of the output folder
npm run postbuild
# start serving the web application on http://localhost:4200
npm run serve
```

### Running in demo production mode

This mode is for running the web application in demo mode on Github pages with
a mock REST API.

```bash
# setting the environment
export DIST=dist-demo
# building the application
ng build --configuration=demo --localize
# move default language to the root of the output folder
npm run postbuild
# start serving the web application on http://localhost:4200
npm run serve
```

## Translations

You can translate the application with the following command.

```bash
npm run extract-i18n
```

The translations are stored in webapplication/src/locales

Use [POEDIT](https://poedit.net/) to manage translations.