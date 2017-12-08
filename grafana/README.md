# Grafana and Prometheus for OpenShift 3.7

## Description

Grafana is a nice webui showing monitoring data that comes from various sources.
One of those sources is Prometheus.

This project proposes ready-to-use templates to deploy Prometheus and Grafana
on OpenShift.

## Deployment

### Deploy Grafana and Prometheus

```
oc process -f grafana-prometheus-storage.yaml -p PVC_SIZE=1Gi |oc create -f -
oc process -f grafana-prometheus.yaml |oc create -f -
oc process -f grafana-base.yaml |oc create -f -
```

### Deploy only Grafana with its vanilla configuration

```
oc process -f grafana-nodatasource.yaml |oc create -f -
oc process -f grafana-base.yaml |oc create -f -
```
