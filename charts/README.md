# Install CSI driver with Helm 3

## Prerequisites
 - [install Helm](https://helm.sh/docs/intro/quickstart/#install-helm)

## install latest version
```console
helm repo add azuredisk-csi-driver https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/charts
helm install azuredisk-csi-driver azuredisk-csi-driver/azuredisk-csi-driver --namespace kube-system
```

## install on Azure Stack
```console
helm install azuredisk-csi-driver azuredisk-csi-driver/azuredisk-csi-driver --namespace kube-system --set cloud=AzureStackCloud
```

### install a specific version
```console
helm repo add azuredisk-csi-driver https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/charts
helm install azuredisk-csi-driver azuredisk-csi-driver/azuredisk-csi-driver --namespace kube-system --version v1.2.0
```

### search for all available chart versions
```console
helm search repo -l azuredisk-csi-driver
```

## uninstall CSI driver
```console
helm uninstall azuredisk-csi-driver -n kube-system
```

## latest chart configuration

The following table lists the configurable parameters of the latest Azure Disk CSI Driver chart and default values.

| Parameter                                         | Description                                                | Default                                                      |
| ------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| `image.azuredisk.repository`                      | azuredisk-csi-driver docker image                          | mcr.microsoft.com/k8s/csi/azuredisk-csi                      |
| `image.azuredisk.tag`                             | azuredisk-csi-driver docker image tag                      | latest                                                       |
| `image.azuredisk.pullPolicy`                      | azuredisk-csi-driver image pull policy                     | IfNotPresent                                                 |
| `image.csiProvisioner.repository`                 | csi-provisioner docker image                               | mcr.microsoft.com/oss/kubernetes-csi/csi-provisioner         |
| `image.csiProvisioner.tag`                        | csi-provisioner docker image tag                           | v1.5.0                                                       |
| `image.csiProvisioner.pullPolicy`                 | csi-provisioner image pull policy                          | IfNotPresent                                                 |
| `image.csiAttacher.repository`                    | csi-attacher docker image                                  | mcr.microsoft.com/oss/kubernetes-csi/csi-attacher            |
| `image.csiAttacher.tag`                           | csi-attacher docker image tag                              | v2.2.0                                                       |
| `image.csiAttacher.pullPolicy`                    | csi-attacher image pull policy                             | IfNotPresent                                                 |
| `image.csiResizer.repository`                     | csi-resizer docker image                                   | mcr.microsoft.com/oss/kubernetes-csi/csi-resizer             |
| `image.csiResizer.tag`                            | csi-resizer docker image tag                               | v0.5.0                                                       |
| `image.csiResizer.pullPolicy`                     | csi-resizer image pull policy                              | IfNotPresent                                                 |
| `image.livenessProbe.repository`                  | liveness-probe docker image                                | mcr.microsoft.com/oss/kubernetes-csi/livenessprobe           |
| `image.livenessProbe.tag`                         | liveness-probe docker image tag                            | v1.1.0                                                       |
| `image.livenessProbe.pullPolicy`                  | liveness-probe image pull policy                           | IfNotPresent                                                 |
| `image.nodeDriverRegistrar.repository`            | csi-node-driver-registrar docker image                     | mcr.microsoft.com/oss/kubernetes-csi/csi-node-driver-registrar |
| `image.nodeDriverRegistrar.tag`                   | csi-node-driver-registrar docker image tag                 | v1.2.0                                                       |
| `image.nodeDriverRegistrar.pullPolicy`            | csi-node-driver-registrar image pull policy                | IfNotPresent                                                 |
| `imagePullSecrets`                                | Specify docker-registry secret names as an array           | [] (does not add image pull secrets to deployed pods)        |                                       |
| `serviceAccount.create`                           | whether create service account of csi-azuredisk-controller | true                                                         |
| `rbac.create`                                     | whether create rbac of csi-azuredisk-controller            | true                                                         |
| `controller.replicas`                             | the replicas of csi-azuredisk-controller                   | 2                                                            |
| `controller.metricsPort`                          | metrics port of csi-azuredisk-controller                   |29604                                                        |
| `controller.runOnMaster`                          | run csi-azuredisk-controller on master node                | false                                                        |
| `controller.logLevel`                             | controller driver log level                                                          |`5`                                                           |
| `node.metricsPort`                                | metrics port of csi-azuredisk-node                         |29605                                                        |
| `node.logLevel`                                   | node driver log level                                                          |`5`                                                           |
| `snapshot.enabled`                                | whether enable snapshot feature                            | false                                                        |
| `snapshot.image.csiSnapshotter.repository`        | csi-snapshotter docker image                               | mcr.microsoft.com/oss/kubernetes-csi/csi-snapshotter         |
| `snapshot.image.csiSnapshotter.tag`               | csi-snapshotter docker image tag                           | v2.0.1                                                       |
| `snapshot.image.csiSnapshotter.pullPolicy`        | csi-snapshotter image pull policy                          | IfNotPresent                                                 |
| `snapshot.image.csiSnapshotController.repository` | snapshot-controller docker image                           | mcr.microsoft.com/oss/kubernetes-csi/snapshot-controller     |
| `snapshot.image.csiSnapshotController.tag`        | snapshot-controller docker image tag                       | v2.1.1                                                       |
| `snapshot.image.csiSnapshotController.pullPolicy` | snapshot-controller image pull policy                      | IfNotPresent                                                 |
| `snapshot.snapshotController.replicas`            | the replicas of snapshot-controller                        | 1                                                            |
| `snapshot.snapshotController.serviceAccount`      | whether create service account of snapshot-controller      | true                                                         |
| `snapshot.snapshotController.rbac`                | whether create rbac of snapshot-controller                 | true                                                         |
| `linux.enabled`                                   | whether enable linux feature                               | true                                                         |
| `windows.enabled`                                 | whether enable windows feature                             | true                                                        |
| `windows.image.livenessProbe.repository`          | windows liveness-probe docker image                        | mcr.microsoft.com/oss/kubernetes-csi/livenessprobe           |
| `windows.image.livenessProbe.tag`                 | windows liveness-probe docker image tag                    | v2.0.1-alpha.1-windows-1809-amd64                            |
| `windows.image.livenessProbe.pullPolicy`          | windows liveness-probe image pull policy                   | IfNotPresent                                                 |
| `windows.image.nodeDriverRegistrar.repository`    | windows csi-node-driver-registrar docker image             | mcr.microsoft.com/oss/kubernetes-csi/csi-node-driver-registrar |
| `windows.image.nodeDriverRegistrar.tag`           | windows csi-node-driver-registrar docker image tag         | v1.2.1-alpha.1-windows-1809-amd64                            |
| `windows.image.nodeDriverRegistrar.pullPolicy`    | windows csi-node-driver-registrar image pull policy        | IfNotPresent                                                 |
| `kubelet.linuxPath`                               | configure the kubelet path for Linux node                  | `/var/lib/kubelet`                                                |
| `kubelet.windowsPath`                             | configure the kubelet path for Windows node                | `'C:\var\lib\kubelet'`                                            |
| `cloud`                                           | the cloud environment the driver is running on             | AzurePublicCloud                                                  |

## troubleshooting
 - Add `--wait -v=5 --debug` in `helm install` command to get detailed error
 - Use `kubectl describe` to get more info
