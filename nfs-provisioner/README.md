# nfs-provisioner

[nfs-provisioner](https://github.com/kubernetes-incubator/external-storage/tree/master/nfs)  is an out-of-tree dynamic provisioner for Kubernetes 1.4. You can use it to quickly & easily deploy shared storage that works almost anywhere with accessMode ReadWriteMany. 


## TL;DR;

```bash
$ helm repo add smizy https://smizy.github.io/charts
$ helm install smizy/nfs-provisioner
```

## Introduction

This chart bootstraps a [nfs-provisioner](https://github.com/kubernetes-incubator/external-storage/tree/master/nfs) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release smizy/nfs-provisioner
```

The command deploys nfs-provisioner on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the nfs-provisioner chart and their default values.

|         Parameter          |                Description                 |                   Default                   |
|----------------------------|--------------------------------------------|---------------------------------------------|
| `image`                    | nfs-provisioner image                            | `quay.io/kubernetes_incubator/nfs-provisioner:{VERSION}`                   |
| `imagePullPolicy`          | Image pull policy.                         | `IfNotPresent`                              |
| `persistence.enabled`      | Use a PVC to persist data                  | `true`                                      |
| `persistence.storageClass` | Storage class of backing PVC               | `standard`  |
| `persistence.accessMode`   | Use volume as ReadOnly or ReadWrite        | `ReadWriteOnce`                             |
| `persistence.size`         | Size of data volume                        | `2Gi`                                       |
| `resources`                | CPU/Memory resource requests/limits        | Memory: `100Mi`, CPU: `50m`                |
| `nfs.provisioner`          | nfs provisioner name                       | `example.com/nfs`                | 
| `nfs.storageClass`          | nfs storageClass name                       | `example-nfs`                | 

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set imagePullPolicy=Always smizy/nfs-provisioner
```

The above command sets the nfs-provisioner imagePullPolicy to `Always`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml smizy/nfs-provisioner
```

> **Tip**: You can use the default [values.yaml](values.yaml)


## Persistence

The [nfs-provisioner](https://quay.io/kubernetes_incubator/nfs-provisioner) image stores the nfs-provisioner data at the `/export` path of the container.

The chart mounts a [Persistent Volume](kubernetes.io/docs/user-guide/persistent-volumes/) volume at this location. The volume is created using dynamic volume provisioning.

You can use NFS provisoned storageClass(default: `example-nfs`) that allows you to create volume dynamically with accessMode: ReadWriteMany.

```console
$ kubectl get storageclass
NAME                 TYPE
example-nfs          example.com/nfs            
standard (default)   k8s.io/minikube-hostpath
```