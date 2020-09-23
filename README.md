# Binder cluster

## Install jupyter binder

TL;DR: <https://binderhub.readthedocs.io/en/latest/zero-to-binderhub/setup-binderhub.html>

### Install

Configure `config.yaml` and `secret.yaml`.

```bash
helm repo add jupyterhub https://jupyterhub.github.io/helm-chart

helm repo install/upgrade

# Version https://jupyterhub.github.io/helm-chart/#development-releases-binderhub
helm upgrade binder jupyterhub/binderhub --install --version=0.2.0-n219.hbc17443 --namespace=my-binder --create-namespace -f secret.yaml -f config.yaml
```

### Public IP

```bash
kubectl --namespace=my-binder get svc proxy-public

NAME           TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
proxy-public   LoadBalancer   10.0.244.145   12.130.208.28    443:32687/TCP,80:30046/TCP   17d
```

Edit `config.yaml` and add EXTERNAL-IP (or DNS name) and upgrade installation.

### Access

```bash
kubectl --namespace=my-binder get svc binder
NAME     TYPE           CLUSTER-IP   EXTERNAL-IP     PORT(S)        AGE
binder   LoadBalancer   10.0.24.30   45.123.210.78   80:31969/TCP   6m36s
```

### DNS

Add a DNS record to:

```bash
binder.your-host.com 45.123.210.78
hub.your-host.com 12.130.208.28
```

### Start

Navigate to: <http://binder.your-host.com>

### References

* https://binderhub.readthedocs.io/en/latest/authentication.html
* https://zero-to-jupyterhub.readthedocs.io/en/v0.5-doc/reference.html
* https://oauthenticator.readthedocs.io/en/latest/getting-started.html#general-setup
* https://zero-to-jupyterhub.readthedocs.io/en/stable/administrator/authentication.html
