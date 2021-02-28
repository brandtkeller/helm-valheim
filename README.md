# Valheim Helm Chart

Helm chart for orchestration of the `lloesche/valheim-server` Valheim docker image.

NOTE: This is a proof of concept currently. Many k8s/helm best practices need to be applied and there are hardcoded values throughout this repository.

## Usage

Note: This assumes the node you are running on can use `/data/valheim` mounted as a host volume for persistence.  

```bash
git clone https://github.com/brandtkeller/helm-valheim.git
helm install valheim ../helm-valheim/ -n <namespace>
```

## Configuration

| Parameter                                  | Description                                                | Default                           |
|:-------------------------------------------|:-----------------------------------------------------------|:----------------------------------|
| `config.password`                                 | Server password                                            | `password`                        |

## Persistence

This will create two PV's of 10GB each.

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
- Persistence Options
- Determine applicable PV sizes

## Bugs
Unable to use password through a secret properly.