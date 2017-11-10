# OpenLDAP

## Description

## Build in OpenShift

```
oc new-build https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir openldap --name openldap --to openldap
```

## Deploy in OpenShift

```
oc new-app https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir openldap --name openldap 
oc volume dc openldap --add --overwrite --name=openldap-volume-1 -t pvc --claim-size=512Mi --claim-name=openldap-logs
oc volume dc openldap --add --overwrite --name=openldap-volume-2 -t pvc --claim-size=512Mi --claim-name=openldap-data
```

