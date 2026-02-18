# spedge-fleet-manifests

Rancher Fleet GitOps manifests for SP Edge devices.

## Structure

```
base/               # Deployed to every registered edge cluster
  00-namespace.yaml
  01-configmaps.yaml
  02-storage.yaml   (Node-RED + Redis PVCs)
  03-redis.yaml
  04-nodered.yaml
  fleet.yaml

packages/           # Optional add-ons, deployed per cluster label
  netbird/          # label: package-netbird=true
  alarms/           # label: package-alarms=true      (coming soon)
  controls/         # label: package-controls=true    (coming soon)
```

## Adding a package to a device

In Rancher, add the corresponding label to the cluster:

```
package-netbird=true
package-alarms=true
```

Fleet detects the label and deploys the bundle. Remove the label to undeploy.

## Secrets

Secrets (`redis-credentials`, `netbird-credentials`) are populated on the device
during first-boot provisioning by `populate-k8s-secrets.sh` in the lilBro repo.
They are not managed by Fleet.
