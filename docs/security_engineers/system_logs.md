
Currently you can check the logs of the system through ssh connection only on the host directly.
The different services will generate the logs into systemd. The logs can be investigated with the `journalctl` command.

## Monitoring


```bash
$ sudo journalctl -fu argus_monitor
-- Journal begins at Sat 2023-07-22 09:17:02 CEST. --
Sep 23 17:36:15 arpi-test.local python3[22577]: 2023-09-23 17:36:15,045-[   Monitor|  Monitor]  INFO: Monitoring stopped
Sep 23 17:36:15 arpi-test.local python3[22577]: INFO:Monitor:Monitoring stopped
Sep 23 17:36:15 arpi-test.local python3[22577]: 2023-09-23 17:36:15,070-[       IPC|      IPC]  INFO: IPC server stopped
Sep 23 17:36:15 arpi-test.local python3[22577]: INFO:IPC:IPC server stopped
Sep 23 17:36:15 arpi-test.local python3[22577]: 2023-09-23 17:36:15,071-[MainThread|  Service]  INFO: All threads stopped
Sep 23 17:36:15 arpi-test.local python3[22577]: INFO:Service:All threads stopped
Sep 23 17:36:15 arpi-test.local systemd[1]: argus_monitor.service: Succeeded.
Sep 23 17:36:15 arpi-test.local systemd[1]: Stopped Argus monitoring service.
Sep 23 17:36:15 arpi-test.local systemd[1]: argus_monitor.service: Consumed 5min 57.393s CPU time.
Sep 23 17:36:15 arpi-test.local systemd[1]: Started Argus monitoring service.
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,002-[MainThread|SC.Access]  INFO: Starting SSH
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,083-[MainThread|  Monitor]  INFO: Monitoring created
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,084-[   Monitor|  Monitor]  INFO: Monitoring started
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,085-[MainThread| Notifier]  INFO: Notifier created
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,087-[  Notifier| Notifier]  INFO: Notifier started...
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,095-[MainThread|      IPC]  INFO: Socket permissions fixed
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,096-[MainThread|      IPC]  INFO: IPC server created
Sep 23 17:36:21 arpi-test.local python3[22958]: 2023-09-23 17:36:21,097-[       IPC|      IPC]  INFO: IPC server started
```

## Server

```bash
$ sudo journalctl -fu argus_server 
-- Journal begins at Sat 2023-07-22 09:17:02 CEST. --
Sep 21 15:32:26 arpi-test.local python3[434]: [2023-09-21 15:32:26 +0200] [434] [INFO] Shutting down: Master
Sep 21 15:32:27 arpi-test.local systemd[1]: argus_server.service: Succeeded.
Sep 21 15:32:27 arpi-test.local systemd[1]: Stopped Argus webapplication.
Sep 21 15:32:27 arpi-test.local systemd[1]: argus_server.service: Consumed 1min 56.540s CPU time.
-- Boot 1ce4fedd02eb4d37a83ba54f3cebaa7e --
Sep 21 15:32:46 arpi-test.local systemd[1]: Started Argus webapplication.
Sep 21 15:32:49 arpi-test.local python3[436]: [2023-09-21 15:32:49 +0200] [436] [INFO] Starting gunicorn 20.1.0
Sep 21 15:32:49 arpi-test.local python3[436]: [2023-09-21 15:32:49 +0200] [436] [INFO] Listening at: unix:/run/argus/argus_server.sock (436)
Sep 21 15:32:49 arpi-test.local python3[436]: [2023-09-21 15:32:49 +0200] [436] [INFO] Using worker: gthread
Sep 21 15:32:49 arpi-test.local python3[486]: [2023-09-21 15:32:49 +0200] [486] [INFO] Booting worker with pid: 486
Sep 21 15:32:49 arpi-test.local python3[487]: [2023-09-21 15:32:49 +0200] [487] [INFO] Booting worker with pid: 487
```

## Dyndns service

```bash
$ sudo journalctl -ft argus_dyndns    
-- Journal begins at Sat 2023-07-22 09:17:02 CEST. --
Sep 23 17:25:04 arpi-test.local argus_dyndns[22751]: 2023-09-23 17:25:04,963 No IP update necessary
Sep 23 17:30:04 arpi-test.local argus_dyndns[22803]: 2023-09-23 17:30:04,759 Update dynamics DNS provider with options: {'username': 'user@email.com', 'hostname': 'arpi-test.dynamic-dns.net', 'provider': 'noip', 'restrict_host': '', 'force': False}
Sep 23 17:30:06 arpi-test.local argus_dyndns[22803]: 2023-09-23 17:30:06,476 IP: '1.2.3.4' == '1.2.3.4'
Sep 23 17:30:06 arpi-test.local argus_dyndns[22803]: 2023-09-23 17:30:06,476 No IP update necessary
Sep 23 17:35:05 arpi-test.local argus_dyndns[22903]: 2023-09-23 17:35:05,297 Update dynamics DNS provider with options: {'username': 'user@email.com', 'hostname': 'arpi-test.dynamic-dns.net', 'provider': 'noip', 'restrict_host': '', 'force': False}
Sep 23 17:35:05 arpi-test.local argus_dyndns[22903]: 2023-09-23 17:35:05,945 IP: '1.2.3.4' == '1.2.3.4'
Sep 23 17:35:05 arpi-test.local argus_dyndns[22903]: 2023-09-23 17:35:05,946 No IP update necessary
Sep 23 17:40:04 arpi-test.local argus_dyndns[22997]: 2023-09-23 17:40:04,709 Update dynamics DNS provider with options: {'username': 'user@email.com', 'hostname': 'arpi-test.dynamic-dns.net', 'provider': 'noip', 'restrict_host': '', 'force': False}
Sep 23 17:40:06 arpi-test.local argus_dyndns[22997]: 2023-09-23 17:40:06,040 IP: '1.2.3.4' == '1.2.3.4'
Sep 23 17:40:06 arpi-test.local argus_dyndns[22997]: 2023-09-23 17:40:06,040 No IP update necessary
```

## Certbot

Service logs:
```bash
$ sudo journalctl -ft argus_certbot
-- Journal begins at Sat 2023-07-22 09:17:02 CEST. --
Sep 23 16:00:04 arpi-test.local argus_certbot[22094]: 2023-09-23 16:00:04,835 Certbot certificate exists
Sep 23 16:00:04 arpi-test.local argus_certbot[22094]: 2023-09-23 16:00:04,836 Renew certbot certificate
Sep 23 16:00:08 arpi-test.local argus_certbot[22094]: 2023-09-23 16:00:08,355 Certificate renewed
Sep 23 16:00:08 arpi-test.local argus_certbot[22094]: 2023-09-23 16:00:08,355 Restarting NGINX
Sep 23 16:00:08 arpi-test.local argus_certbot[22094]: 2023-09-23 16:00:08,410 Using certbot certificates
Sep 23 17:00:04 arpi-test.local argus_certbot[22534]: 2023-09-23 17:00:04,197 Certbot certificate exists
Sep 23 17:00:04 arpi-test.local argus_certbot[22534]: 2023-09-23 17:00:04,198 Renew certbot certificate
Sep 23 17:00:09 arpi-test.local argus_certbot[22534]: 2023-09-23 17:00:09,754 Certificate renewed
Sep 23 17:00:09 arpi-test.local argus_certbot[22534]: 2023-09-23 17:00:09,756 Restarting NGINX
Sep 23 17:00:09 arpi-test.local argus_certbot[22534]: 2023-09-23 17:00:09,812 Using certbot certificates
```

Letsencrypt logs:
```bash
➜  server sudo tail -f /var/log/letsencrypt/letsencrypt.log          
2023-09-23 17:00:09,360:DEBUG:certbot.ocsp:OCSP certificate status for /etc/letsencrypt/archive/arpi/cert2.pem is: OCSPCertStatus.GOOD
2023-09-23 17:00:09,405:INFO:certbot._internal.renewal:Cert not yet due for renewal
2023-09-23 17:00:09,408:DEBUG:certbot._internal.plugins.selection:Requested authenticator webroot and installer None
2023-09-23 17:00:09,409:DEBUG:certbot.display.util:Notifying user: 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
2023-09-23 17:00:09,409:DEBUG:certbot.display.util:Notifying user: The following certificates are not due for renewal yet:
2023-09-23 17:00:09,409:DEBUG:certbot.display.util:Notifying user:   /etc/letsencrypt/live/arpi/fullchain.pem expires on 2023-11-01 (skipped)
2023-09-23 17:00:09,410:DEBUG:certbot.display.util:Notifying user: No renewals were attempted.
2023-09-23 17:00:09,410:DEBUG:certbot.display.util:Notifying user: - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
2023-09-23 17:00:09,411:DEBUG:certbot._internal.renewal:no renewal failures
```
