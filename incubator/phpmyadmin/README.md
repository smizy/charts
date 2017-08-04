# phpMyAdmin

[phpMyAdmin](https://www.phpmyadmin.net) is a free software tool written in PHP, intended to handle the administration of MySQL over the Web.


## TL;DR;

```bash
$ helm repo add smizy https://smizy.github.io/charts
$ helm install smizy/phpmyadmin
```

## Introduction

This chart bootstraps a phpMyAdmin deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled


## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release smizy/phpmyadmin
```

The command deploys phpMyAdmin on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the phpMyAdmin chart and their default values.

|         Parameter          |                Description                 |                   Default                   |
|----------------------------|--------------------------------------------|---------------------------------------------|
| `image`                    | phpMyAdmin image                            | `smizy/phpmyadmin:{VERSION}`                   |
| `imagePullPolicy`          | Image pull policy.                         | `IfNotPresent`                              |
| `resources`                | CPU/Memory resource requests/limits        | Memory: `100Mi`, CPU: `50m`                |

The above parameters map to the env variables defined in [smizy/phpmyadmin](http://github.com/smizy/docker-phpmyadmin). For more information please refer to the [smizy/docker-phpmyadmin](http://github.com/smizy/docker-phpmyadmin) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set imagePullPolicy=Always smizy/phpmyadmin
```

The above command sets the phpmyadmin imagePullPolicy to `Always`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml smizy/phpmyadmin
```

> **Tip**: You can use the default [values.yaml](values.yaml)

