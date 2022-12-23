# helm-valheim

![Version: 0.0.4](https://img.shields.io/badge/Version-0.0.4-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.0](https://img.shields.io/badge/AppVersion-1.0.0-informational?style=flat-square)

A Helm chart for Hosting a Dedicated Valheim Server

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install helm-valheim chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"lloesche/valheim-server"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| fullnameOverride | string | `""` |  |
| secrets.SERVER_PASS | string | `"somerandompassword"` |  |
| secrets.SUPERVISOR_HTTP_PASS | string | `""` |  |
| config.SERVER_NAME | string | `"My Server"` |  |
| config.SERVER_PORT | string | `"2456"` |  |
| config.WORLD_NAME | string | `"Dedicated"` |  |
| config.SERVER_PUBLIC | string | `"true"` |  |
| config.SERVER_ARGS | string | `""` |  |
| config.ADMINLIST_IDS | string | `""` |  |
| config.BANNEDLIST_IDS | string | `""` |  |
| config.PERMITTEDLIST_IDS | string | `""` |  |
| config.UPDATE_CRON | string | `"*/15 * * * *"` |  |
| config.IDLE_DATAGRAM_WINDOW | string | `"3"` |  |
| config.IDLE_DATAGRAM_MAX_COUNT | string | `"30"` |  |
| config.UPDATE_IF_IDLE | string | `"true"` |  |
| config.RESTART_CRON | string | `"0 3 * * *"` |  |
| config.RESTART_IF_IDLE | string | `"true"` |  |
| config.TZ | string | `"America/Los_Angeles"` |  |
| config.BACKUPS | string | `"true"` |  |
| config.BACKUPS_CRON | string | `"0 */2 * * *"` |  |
| config.BACKUPS_DIRECTORY | string | `"/config/backups"` |  |
| config.BACKUPS_MAX_AGE | string | `"3"` |  |
| config.BACKUPS_MAX_COUNT | string | `"0"` |  |
| config.BACKUPS_IF_IDLE | string | `"true"` |  |
| config.BACKUPS_IDLE_GRACE_PERIOD | string | `"3600"` |  |
| config.BACKUPS_ZIP | string | `"true"` |  |
| config.PERMISSIONS_UMASK | string | `"022"` |  |
| config.STEAMCMD_ARGS | string | `"validate"` |  |
| config.VALHEIM_PLUS | string | `"false"` |  |
| config.BEPINEX | string | `"false"` |  |
| config.SUPERVISOR_HTTP | bool | `false` |  |
| config.SUPERVISOR_HTTP_PORT | int | `9001` |  |
| config.SUPERVISOR_HTTP_USER | string | `"admin"` |  |
| config.STATUS_HTTP	false | string | `""` |  |
| config.STATUS_HTTP_PORT | int | `80` |  |
| config.STATUS_HTTP_CONF | string | `"/config/httpd.conf"` |  |
| config.STATUS_HTTP_HTDOCS | string | `"/opt/valheim/htdocs"` |  |
| config.SYSLOG_REMOTE_HOST | string | `""` |  |
| config.SYSLOG_REMOTE_PORT | int | `514` |  |
| config.SYSLOG_REMOTE_AND_LOCAL | bool | `true` |  |
| config.PUID | int | `0` |  |
| config.PGID | int | `0` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.name | string | `""` |  |
| persistence.enabled | bool | `true` |  |
| persistence.labels | object | `{}` |  |
| persistence.annotations | object | `{}` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.size | string | `"10Gi"` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.type | string | `"NodePort"` |  |
| service.port | int | `2456` |  |
| service.nodePort | int | `31000` |  |
| resources | string | `nil` |  |
| nodeSelector | object | `{}` |  |
| tolerations | list | `[]` |  |
| affinity | object | `{}` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
