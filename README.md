# Nextcloud Helm Charts

[Helm](https://helm.sh) repo for different charts related to Nextcloud which can be installed on [Kubernetes](https://kubernetes.io)

### Add Helm repository

To install the repo just run:

```bash
helm repo add nextcloud https://iraangeles.github.io/helm-nextcloud/
helm repo update
```

### Helm Charts

* [nextcloud](https://iraangeles.github.io/helm-nextcloud/)

  ```bash
  helm install my-release nextcloud/nextcloud
  ```

For more information, please checkout the chart level [README.md](./helm/charts/nextcloud/README.md).

### Support and Contribution
Please also review the official [NextCloud Code of Conduct](https://nextcloud.com/contribute/code-of-conduct/) before contributing.

#### Questions and Discussions
[GitHub Discussion](https://github.com/nextcloud/helm/discussions)

#### Bugs and other Issues
If you have a bug to report or a feature to request, you can first search the [GitHub Issues](https://github.com/nextcloud/helm/issues), and  if you can't find what you're looking for, feel free to open an issue.

<<<<<<< HEAD
#### Contributing to the Code
We're always happy to review a pull request :) Please just be sure to check the pull request template to make sure you fufill all the required checks, most importantly the [DCO](https://probot.github.io/apps/dco/).
=======
```console
$ helm install --name my-release stable/nextcloud
```

The command deploys nextcloud on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the nextcloud chart and their default values.

|              Parameter              |                Description                |                   Default                               |
|-------------------------------------|-------------------------------------------|-------------------------------------------------------- |
| `image.repository`                  | nextcloud Image name                       | `nextcloud`                                      |
| `image.tag`                         | nextcloud Image tag                        | `{VERSION}`                                             |
| `image.pullPolicy`                  | Image pull policy                         | `Always` if `imageTag` is `latest`, else `IfNotPresent` |
| `image.pullSecrets`                 | Specify image pull secrets                | `nil`                                                   |
| `ingress.enabled`                   | Enable use of ingress controllers         | `false`                                                 |
| `ingress.servicePort`               | Ingress' backend servicePort              | `http`                                                  |
| `ingress.annotations`               | An array of service annotations           | `nil`                                                   |
| `ingress.tls`                       | Ingress TLS configuration                 | `[]`                                                    |
| `nextcloud.host`                     | nextcloud host to create application URLs  | `nextcloud.kube.home`                                                   |
| `nextcloud.username`                 | User of the application                   | `admin`                                                  |
| `nextcloud.password`                 | Application password                      | `changeme`                                    |
| `internalDatabase.enabled`         | Whether to use internal sqlite database    | `true`                                      |
| `internalDatabase.database`         | Name of the existing database             | `nextcloud`                                      |
| `externalDatabase.enabled`          | Whether to use external database          | `false`                                                   |
| `externalDatabase.host`             | Host of the external database             | `nil`                                                   |
| `externalDatabase.database`         | Name of the existing database             | `nextcloud`                                      |
| `externalDatabase.user`             | Existing username in the external db      | `nextcloud`                                           |
| `externalDatabase.password`         | Password for the above username           | `nil`                                                   |
| `mariadb.enabled`                   | Whether to use the MariaDB chart          | `false`                                                  |
| `mariadb.db.name`           | Database name to create                   | `nextcloud`                                      |
| `mariadb.db.password`           | Password for the database                 | `changeme`                                                   |
| `mariadb.db.user`               | Database user to create                   | `nextcloud`                                           |
| `mariadb.rootUser.password`       | MariaDB admin password                    | `nil`                                                   |
| `service.type`                      | Kubernetes Service type                   | `ClusterIp`                                          |
| `service.loadBalancerIP`            | LoadBalancerIp for service type LoadBalancer                   | `nil`                                          |
| `persistence.enabled`     | Enable persistence using PVC              | `false`                                                  |
| `persistence.storageClass` | PVC Storage Class for nextcloud volume     | `nil` (uses alpha storage class annotation)             |
| `persistence.existingClaim`| An Existing PVC name for nextcloud volume  | `nil` (uses alpha storage class annotation)             |
| `persistence.accessMode`   | PVC Access Mode for nextcloud volume       | `ReadWriteOnce`                                         |
| `persistence.size`         | PVC Storage Request for nextcloud volume   | `8Gi`                                                   |
| `resources`                         | CPU/Memory resource requests/limits       | `{}`                 |

> **Note**:
>
> For nextcloud to function correctly, you should specify the `nextcloud.host` parameter to specify the FQDN (recommended) or the public IP address of the nextcloud service.
>
> Optionally, you can specify the `service.loadBalancerIP` parameter to assign a reserved IP address to the nextcloud service of the chart. However please note that this feature is only available on a few cloud providers (f.e. GKE).
>
> To reserve a public IP address on GKE:
>
> ```bash
> $ gcloud compute addresses create nextcloud-public-ip
> ```
>
> The reserved IP address can be associated to the nextcloud service by specifying it as the value of the `service.loadBalancerIP` parameter while installing the chart.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set nextcloud.username=admin,nextcloud.password=password,mariadb.rootUser.password=secretpassword \
    stable/nextcloud
```

The above command sets the nextcloud administrator account username and password to `admin` and `password` respectively. Additionally, it sets the MariaDB `root` user password to `secretpassword`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml stable/nextcloud
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

The [Nextcloud](https://hub.docker.com/_/nextcloud/) image stores the nextcloud data and configurations at the `/var/www/html` paths of the container.

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube.
See the [Configuration](#configuration) section to enable persistence and configuration of the PVC.
>>>>>>> 3eb7266 (Fix doc for default persistance value (#12041))
