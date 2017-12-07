# grafana

## Description

## Build in OpenShift

```
oc new-build https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir grafana --name grafana --to grafana
```

## Deploy in OpenShift

```
oc new-app https://github.com/nmasse-itix/OpenShift-Docker-Images.git --context-dir grafana --name grafana
oc volume dc grafana --add --overwrite --name=grafana-volume-0 -t pvc --claim-size=512Mi --claim-name=grafana-data --mount-path=/var/lib/grafana/
```

