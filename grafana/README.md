# Grafana and Prometheus for OpenShift 3.9

## Description

Grafana is a nice webui showing monitoring data that comes from various sources.
One of those sources is Prometheus.

This project proposes ready-to-use templates to deploy Prometheus and Grafana
on OpenShift.

## Pre-requisites

Make sure you are cluster-admin on your OpenShift cluster.

## Deploy Prometheus

To deploy prometheus, process the `prometheus.yaml` template with at least the
`NAMESPACE` parameter. This parameter must be the name of the OpenShift
project where you want to deploy Prometheus. This parameter is required
to setup correctly the OpenShift authentication in Prometheus.

For instance, to deploy Prometheus in a project named "my-metrics", use:

```sh
oc process -f prometheus.yaml -p NAMESPACE=my-metrics |oc create -n my-metrics -f -
```

## Deploy Grafana

To deploy grafana, process the `grafana.yaml` template with at least the
`NAMESPACE` parameter. This parameter must be the name of the OpenShift
project where you want to deploy Grafana. This parameter is required
to setup correctly the OpenShift authentication in Grafana.

For instance, to deploy Grafana in a project named "my-metrics", use:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics |oc create -n my-metrics -f -
```

### Choosing the version to deploy

To deploy the latest stable release of Grafana:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics -p GRAFANA_RELEASE=stable |oc create -n my-metrics -f -
```

To deploy the latest beta release of Grafana:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics -p GRAFANA_RELEASE=beta |oc create -n my-metrics -f -
```

To deploy a custom version of Grafana:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics -p GRAFANA_RELEASE=custom -p GRAFANA_CUSTOM_VERSION=4.1.2 |oc create -n my-metrics -f -
```

### Misc. settings

To customize the hostname of the Grafana route, use:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics -p GRAFANA_HOSTNAME=grafana.acme.corp |oc create -n my-metrics -f -
```

By default, a 1Gb volume is reserved for grafana, if you want to use a different size:

```sh
oc process -f grafana.yaml -p NAMESPACE=my-metrics -p GRAFANA_VOLUME_SIZE=10Gi |oc create -n my-metrics -f -
```
