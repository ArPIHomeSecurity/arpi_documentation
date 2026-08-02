
# Argus command line tools (SSH)

These scripts are available after you log in with SSH as the `argus` user.

```bash
ssh argus@arpi.local
```

Commands are installed in `~/.local/bin` and can be run directly as `argus-*` commands.

## Certificate management 

### argus-certbot

```bash
usage: argus-certbot [-h] [-g | -r | -d] [-v]

Update the system using certificates, or manage the certificate

options:
  -h, --help      show this help message and exit
  -g, --generate  generate the certificate
  -r, --renew     renew the certificate
  -d, --delete    delete the certificate
  -v, --verbose   increase output verbosity
```

Examples:

```bash
argus-certbot
argus-certbot --renew
argus-certbot --delete
```

## Clock management

### argus-clock

```bash
usage: argus-clock [-h] [-s] [-v]

List or synchronize system clock with HW clock or NTP server

options:
  -h, --help     show this help message and exit
  -s, --sync     synchronize system clock with HW clock or NTP server
  -v, --verbose  increase output verbosity
```

Examples:

```bash
argus-clock
argus-clock --sync
```

## Database seed and cleanup

### argus-data

```bash
usage: argus-data [-h] [-d] [-c environment] [-v]

options:
  -h, --help            show this help message and exit
  -d, --delete          Delete database content
  -c, --create environment
                        Create database content (environments: prod, live_01, test_with_v3, test_with_v2, admin_registration)
  -v, --verbose         Enable verbose logging
```

Examples:

```bash
argus-data --delete
argus-data --create prod
argus-data --delete --create test_with_v3
```

## Dynamic DNS update

### argus-dyndns

```bash
usage: argus-dyndns [-h] [-v] [-f]

Update IP address at DNS provider

options:
  -h, --help     show this help message and exit
  -v, --verbose  increase output verbosity
  -f, --force    force update
```

Examples:

```bash
argus-dyndns
argus-dyndns --force
```

## Hash helper

### argus-hash

```bash
usage: argus-hash [-h] [-c] [input]

Hash text to database format

positional arguments:
  input           Input string to hash

options:
  -h, --help      show this help message and exit
  -c, --check     Check if database uses bcrypt hashes
```

Examples:

```bash
argus-hash 1234
argus-hash --check
```

## Secret generator

### argus-secret

```bash
usage: argus-secret [-h] [--type {rest,mcp}]

Manage secrets for ArPI server.

options:
  -h, --help            show this help message and exit
  --type {rest,mcp}     Type of secret to manage: rest for REST API, mcp for MCP Server
```

Examples:

```bash
argus-secret
argus-secret --type mcp
```

## Simulator UI

### argus-simulator

Starts the Textual-based interactive simulator UI.

```bash
usage: argus-simulator
```

Example:

```bash
argus-simulator
```

## SSH key management

### argus-ssh-keymanager

```bash
usage: argus-ssh-keymanager [-h] [--key_type KEY_TYPE] --key_name KEY_NAME
                            [--passphrase PASSPHRASE] [--public_key PUBLIC_KEY] [-v]
                            {generate,set,remove}

Manage SSH keys.

positional arguments:
  {generate,set,remove}   Command to execute.

options:
  -h, --help              show this help message and exit
  --key_type KEY_TYPE     Type of the key to generate (rsa, ecdsa, ed25519).
  --key_name KEY_NAME     Name of the key.
  --passphrase PASSPHRASE Passphrase for the key.
  --public_key PUBLIC_KEY Public key string to set
  -v, --verbose           Increase output verbosity.
```

Examples:

```bash
argus-ssh-keymanager generate --key_type ed25519 --key_name laptop
argus-ssh-keymanager set --key_name laptop --public_key "ssh-ed25519 AAAA... user@host"
argus-ssh-keymanager remove --key_name laptop
```

## SSH service configuration

### argus-ssh-service

```bash
usage: argus-ssh-service [-h] [--enable-ssh] [--disable-ssh]
                         [--allow-local-networks] [--allow-any-networks]
                         [--get-local-ip] [--enable-password] [--disable-password] [-v]

SSH service

options:
  -h, --help             show this help message and exit
  --enable-ssh           Enable SSH
  --disable-ssh          Disable SSH
  --allow-local-networks Restrict SSH access only from local network
  --allow-any-networks   Allow SSH access from all networks
  --get-local-ip         Get local IP
  --enable-password      Enable password authentication
  --disable-password     Disable password authentication
  -v, --verbose          Increase output verbosity.
```

Examples:

```bash
argus-ssh-service --get-local-ip
argus-ssh-service --allow-local-networks
argus-ssh-service --disable-password
argus-ssh-service --enable-password
argus-ssh-service --enable-ssh
```

Note:

- `--disable-ssh` is currently defined but not applied by the script logic. Use systemd directly if needed:

```bash
sudo systemctl stop ssh
sudo systemctl disable ssh
```

## Hardware adapter tests

### argus-tester

```bash
usage: argus-tester [-h] [-v] [-b {2,3}] {sensor,power,output,keypad}

Testing script for adapters which control the hardware components

positional arguments:
  {sensor,power,output,keypad}

options:
  -h, --help            show this help message and exit
  -v, --verbose
  -b, --board-version {2,3}
                        Board version (2=GPIO/OPTO, 3=SPI/AD)
```

Examples:

```bash
argus-tester sensor --board-version 3
argus-tester output --board-version 2
```

Important:

- Stop `argus_monitor` before running tests:

```bash
sudo systemctl stop argus_monitor
```

## User management helper

### argus-user

```bash
usage: argus-user [-h] [-l] [-r REGISTRATION_CODE] [-a ACCESS_CODE] [-u USER] [-e EXPIRY]

Update the given user with a new registration or access code.

options:
  -h, --help            show this help message and exit
  -l, --list            List all users
  -r, --registration-code REGISTRATION_CODE
                        New registration code
  -a, --access-code ACCESS_CODE
                        New access code
  -u, --user USER       The id of the user
  -e, --expiry EXPIRY   The expiry of the registration code in seconds (or never expires)
```

Examples:

```bash
argus-user --list
argus-user --user 1 --registration-code ABCD --expiry 3600
argus-user --user 2 --access-code 1234
```

## Upgrade tool

### argus-upgrade

```bash
usage: argus-upgrade [-h] [--prerelease] [--board-version BOARD_VERSION] [--use-simulator]

options:
  -h, --help            show this help message and exit
  --prerelease          Use latest prerelease
  --board-version       Board version (2 or 3)
  --use-simulator       Use simulator
```

Examples:

```bash
argus-upgrade
argus-upgrade --prerelease --board-version 3
```

Important:

- This command installs packages and restarts services, so it may request sudo privileges.
