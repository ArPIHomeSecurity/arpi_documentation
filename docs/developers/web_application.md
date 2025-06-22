The user interface is built with modern web technologies providing a responsive, cross-platform experience:

## Technology Stack

- **Angular 18.x** - Modern TypeScript-based frontend framework
- **Angular Material** - Material Design component library  
- **Ionic Framework** - Cross-platform mobile development
- **Capacitor** - Native mobile app capabilities
- **RxJS** - Reactive programming for real-time updates
- **Socket.IO Client** - Real-time bidirectional communication
- **Angular i18n** - Internationalization support

## Application Modes

The application supports multiple deployment modes:

### 1. Production Mode
Full-featured application connecting to backend services on Raspberry Pi

### 2. Development Mode  
Local development with live reload and debugging tools

### 3. Demo Mode
Standalone application with mock services for demonstrations

### 4. Mobile App Mode
Native mobile application using Capacitor framework

## Source code

The source code of the backend system: [arpi_webapplication](https://github.com/ArPIHomeSecurity/arpi_webapplication).
It is a sub-module of the arpi_management project: [arpi_management](https://github.com/ArPIHomeSecurity/arpi_management.git)

You find how to get the source code [here](index.md#getting-the-code)!

## Normal mode

In normal mode you can build the web application and you can host localized version with Nginx.

### Development

Building and running:
```bash
# building the application with locales
ng build --localize
# start serving the web application on http://localhost:4200
npm run serve-dev
```

```bash
# building the application with auto update in terminal 1
ng build --localize --watch --poll 2000

# after the application is built first starting the webserver in terminal 2
npm run serve-dev
```

### Production


Building locally:
```bash
# building the application with locales
ng build --configuration=production --localize
```

Deploying to Raspberry:
```bash
# go to the arpi_management project
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
npm run serve-demo-dev
```

```bash
# building the application with auto update in terminal 1
ng build --configuration=demo-dev --localize --watch --poll 2000

# after the application is built first starting the webserver in terminal 2
npm run serve-demo-dev
```

### Production

This mode is for running the web application in demo mode on GitHub pages.

```bash
# building the application with locales
ng build --configuration=demo --localize
# start serving the web application on http://localhost:4200
npm run serve-demo
```

## Translations

You can update the translations of the application with the following command.

```bash
npm run extract-i18n
```

This command will extract the translations from the source code and update the translation files.
The translations are stored in "webapplication/src/locales".

You can use tools like [POEDIT](https://poedit.net/) to manage the translations.

After the translations are updated you can build the application with the new translations
and deploy it.

* [build production web application](#production_1)
* [deploy to raspberry pi](deployment.md#deploying-components)


!!! todo
    Document adding new translations
