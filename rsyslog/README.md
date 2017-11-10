# rsyslog

## Description

## Build in OpenShift

```
oc new-build https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir rsyslog --name rsyslog --to rsyslog
```

## Deploy in OpenShift

```
oc new-app https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir rsyslog --name rsyslog 
oc volume dc rsyslog --add --overwrite --name=rsyslog-volume-1 -t pvc --claim-size=512Mi --claim-name=rsyslog-data --mount-path=/var/log/
```

