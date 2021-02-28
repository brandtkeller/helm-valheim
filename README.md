# Valheim Helm Chart

Helm chart for orchestration of the `lloesche/valheim-server` Valheim docker image.

NOTE: This is a proof of concept currently. Many k8s/helm best practices need to be applied and there are hardcoded values throughout this repository. Attempted to use the `mbround18/valheim` image but it refused to run on my cluster without `privileged: true`.

## Usage

```bash
git clone https://github.com/brandtkeller/helm-valheim.git
helm install valheim ../helm-valheim/ -n <namespace>
```

## Configuration

| Parameter                                  | Description                                                | Default                           |
|:-------------------------------------------|:-----------------------------------------------------------|:----------------------------------|
| `config.password`                                 | Server password                                            | `password`                        |

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
- Establish a readiness/liveness probe
- Enable use of all environment variables the image exposes
- Fix password secret bug
- Determine applicable PV sizes

## Bugs
Unable to use password through a secret properly.