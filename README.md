# Valheim Helm Chart

Helm chart for orchestration of the `lloesche/valheim-server` Valheim docker image.

NOTE: This is a proof of concept currently. Many k8s/helm best practices need to be applied and there are hardcoded values throughout this repository. Attempted to use the `mbround18/valheim` image but it refused to run on my cluster without `privileged: true`.

## Usage

```bash
git clone https://github.com/brandtkeller/helm-valheim.git
helm install valheim ../helm-valheim/ -n <namespace>
```

## Configuration

# Environment Variables
| Name | Default | Purpose |
|----------|----------|-------|
| `config.SERVER_NAME` | `My Server` | Name that will be shown in the server browser |
| `config.SERVER_PORT` | `2456` | UDP start port that the server will listen on |
| `config.WORLD_NAME` | `Dedicated` | Name of the world without `.db/.fwl` file extension |
| `config.SERVER_PASS` | `secret` | Password for logging into the server - min. 5 characters! |
| `config.SERVER_PUBLIC` | `true` | Whether the server should be listed in the server browser (`true`) or not (`false`) |
| `config.SERVER_ARGS` |  | Additional Valheim server CLI arguments |
| `config.UPDATE_CRON` | `*/15 * * * *` | [Cron schedule](https://en.wikipedia.org/wiki/Cron#Overview) for update checks (disabled if set to an empty string or if the legacy `UPDATE_INTERVAL` is set) |
| `config.UPDATE_IF_IDLE` | `true` | Only run update check if no players are connected to the server (`true` or `false`) |
| `config.RESTART_CRON` | `0 3 * * *` | [Cron schedule](https://en.wikipedia.org/wiki/Cron#Overview) for server restarts (disabled if set to an empty string) |
| `config.TZ` | `Etc/UTC` | Container [time zone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) |
| `config.BACKUPS` | `true` | Whether the server should create periodic backups (`true` or `false`) |
| `config.BACKUPS_CRON` | `0 */2 * * *` | [Cron schedule](https://en.wikipedia.org/wiki/Cron#Overview) for world backups (disabled if set to an empty string or if the legacy `BACKUPS_INTERVAL` is set) |
| `config.BACKUPS_DIRECTORY` | `/config/backups` | Path to the backups directory |
| `config.BACKUPS_MAX_AGE` | `3` | Age in days after which old backups are flushed |
| `config.PERMISSIONS_UMASK` | `022` | [Umask](https://en.wikipedia.org/wiki/Umask) to use for backups, config files and directories |
| `config.STEAMCMD_ARGS` | `validate` | Additional steamcmd CLI arguments |
| `config.VALHEIM_PLUS` | `false` | Whether [ValheimPlus](https://github.com/valheimPlus/ValheimPlus) mod should be loaded (config in `/config/valheimplus`) |

There are a few undocumented environment variables that could break things if configured wrong. They can be found in [`defaults`](defaults).

## Persistence

This will create two PV's of 10GB each using the clusters default StorageClass unless a non-default StorageClass is specified.

### Using a Persistent Volume
. Once you spin up the game pod you should see the following files created:
```bash
$ ls /data/valheim
adminlist.txt  backups  bannedlist.txt  permittedlist.txt  prefs  worlds
```

## TODO
- Revise NOTES.TXT
- Determine applicable PV sizes