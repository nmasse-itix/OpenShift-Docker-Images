# Minio Docker images based on RHEL7 for OpenShift

## Description

This project proposes ready-to-use templates to deploy Minio
on OpenShift.

## Deployment

### Pre-requisites

```
oc import-image -n openshift rhel7 --from registry.access.redhat.com/rhel7:latest --confirm
```

### Deploy Minio on OpenShift

```
oc process -f minio.yaml -p MINIO_ROUTE_HOSTNAME=minio.openshift.test | oc create -f -
```
