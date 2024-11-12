
The code can be deployed to a Raspberry PI system with the help of the arpi_managment project.
The full installation process is described [here](installation.md)! You can also update an
existing system by deploying the software components from the source code.

You find how to get the source code [here](index.md#getting-the-code)!


## Prerequisites

1. Source code
2. Existing running security system accessible with SSH


## Deployment configuration

The project contains a template file for creating configurations.

[Configuration template on GitHub!](https://github.com/ArPIHomeSecurity/arpi_management/blob/master/install.yaml)


1. Create a copy of the template.
```bash
cp install/install.yaml install/test.yaml
```
2. Update the configuration in the file.
3. Use the new file.
```bash
pipenv run ./install.py -e test {component}
```
The '-e' argument will select the new configuration file.

Configuration file name template: 'install/[.< environment >].yaml'

## Deploying components

```bash
# deploying
pipenv run ./install.py server
pipenv run ./install.py monitor
pipenv run ./install.py database
pipenv run ./install.py webapplication
```

The install script has different option for deploying the components.

1. Restarting the component after deployment
2. Updating the python virtual environment of server and monitoring components

```bash
# deploying and restart
pipenv run ./install.py -r server
pipenv run ./install.py -r monitor
```

```bash
# deploying, update (python virtual environment) and restart
pipenv run ./install.py -ur server
pipenv run ./install.py -ur monitor
```
