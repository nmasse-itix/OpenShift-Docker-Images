# rtorrent Docker images for OpenShift

## Description

This project proposes ready-to-use templates to deploy rtorrent
on OpenShift.

## Deployment

### Base Image

If you are on OpenShift Origin, import the `centos` image in the `openshift` namespace:

```sh
oc import-image -n openshift centos7 --from docker.io/centos:7 --confirm --scheduled
```

If you are on OpenShift Container Platform, import the `rhel` image in the `openshift` namespace:

```sh
oc import-image -n openshift rhel7 --from registry.access.redhat.com/rhel7:7.4 --confirm --scheduled
```

### Pre-requisites

Open the bittorrent ports, as explained [in the OpenShift documentation](https://docs.openshift.com/container-platform/3.9/architecture/core_concepts/pods_and_services.html#service-nodeport).

Namely, you will have to add to your `/etc/origin/master/master-config.yaml`:

```yaml
kubernetesMasterConfig:
  servicesNodePortRange: '6880-6900'
```

And then restart with:

```sh
sudo systemctl restart atomic-openshift-master-controllers
sudo systemctl restart atomic-openshift-master-api
```

On each node that will run `rtorrent`, you will have to add an exception in the
`iptables` chain `OS_FIREWALL_ALLOW`.

To add them permanently, use:

```sh
firewall-cmd --permanent --direct --add-rule ipv4 filter IN_public_allow 1 -m udp -p udp -m conntrack --ctstate NEW --dport 6881 -j ACCEPT
firewall-cmd --permanent --direct --add-rule ipv4 filter IN_public_allow 1 -m udp -p udp -m conntrack --ctstate NEW -m multiport --dports 6890:6899 -j ACCEPT
firewall-cmd --permanent --direct --add-rule ipv4 filter IN_public_allow 1 -m tcp -p tcp -m conntrack --ctstate NEW -m multiport --dports 6890:6899 -j ACCEPT
firewall-cmd --reload
```

### Deploy rtorrent

Create all the Kubernetes objects:

```sh
oc new-project rtorrent
oc process -f rtorrent.yaml -p NODE_IP_ADDRESS=1.2.3.4 | oc create -f -
```

Give an additional role to our service account to allow the oauth proxy 
to authenticate users.

```sh
oc adm policy add-cluster-role-to-user system:auth-delegator -z rtorrent -n rtorrent
```