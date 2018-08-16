# Quickstart

## Requirements

- ansible 2.4
- oc locally installed

## Configure before you start

Create `roles/openshift/defaults/main.yml` based on the `main.example.yml`.
You should at least change these variables in the `main.yml`:

```yml
# URL to your OpenShift Cluster Console
oc_cluster_url: https://localhost:8443
# Login credentials
oc_username: MY-USERNAME
oc_token: MY-TOKEN
```

Create a `.dockercfg` in `roles/openshift/files/`.
You can base the structure of the file based on the `.dockercfg.example`. This file should contain credentials to access the docker registries.

## How to run the ansible playbook

Run in your CLI:

```sh
$ ansible-playbook site.yml --connection=local
```

## Links

https://blog.openshift.com/remotely-push-pull-container-images-openshift/
http://v1.uncontained.io/playbooks/continuous_delivery/external-docker-registry-integration.html#accessing-secure-registrises
