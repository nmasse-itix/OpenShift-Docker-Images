# Grafana and Prometheus for OpenShift 3.7

## Description

Grafana is a nice webui showing monitoring data that comes from various sources.
One of those sources is Prometheus.

This project proposes ready-to-use templates to deploy Prometheus and Grafana
on OpenShift.

## Deployment

### Pre-requisites

First, make sure the is a `rhel7` imagestream in the `openshift` namespace.
```
oc import-image -n openshift rhel7 --from registry.access.redhat.com/rhel7:latest --confirm
```

Then, make sure you are cluster-admin on your OpenShift cluster.

### Deploy Grafana and Prometheus

```
oc process -f grafana-prometheus-storage.yaml -p PVC_SIZE=1Gi |oc create -f -
oc process -f grafana-prometheus.yaml -p PROMETHEUS_ROUTE_HOSTNAME=prometheus.app.openshift.test -p ALERTS_ROUTE_HOSTNAME=alerts.app.openshift.test |oc create -f -
oc process -f grafana-base.yaml -p GRAFANA_ROUTE_HOSTNAME=grafana.app.openshift.test |oc create -f -
```

### Deploy only Grafana with its vanilla configuration

```
oc process -f grafana-nodatasource.yaml |oc create -f -
oc process -f grafana-base.yaml |oc create -f -
```

## Configuration

Once deployed, connect to Grafana and add a datasource with the following configuration:
- Name: `prometheus`
- Type: `Prometheus`
- URL: `http://prometheus:9090`
- Access: `proxy`

