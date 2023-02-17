# Nextcloud Helm Charts

[Helm](https://helm.sh) repo for different charts related to Nextcloud which can be installed on [Kubernetes](https://kubernetes.io)

### Add Helm repository

To install the repo just run:

```bash
helm repo add nextcloud https://github.com/IraAngeles/helm-nextcloud.git
helm repo update
```

### Helm Charts

* [nextcloud](https://github.com/IraAngeles/helm-nextcloud.git)

  ```bash
  helm install my-release nextcloud/nextcloud
  ```
