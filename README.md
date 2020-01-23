# Unifi Controller for Kubernetes

This goal of this yaml is to be able to quickly and easily deploy the unifi controller to kubernetes.  I did not create the docker image
and there might be similar (and better) yaml files out there for this.

# Assumptions

This assumes you have a load balancer installed and that you are using iSCSI for storage

# Issues

LoadBalancers do not support exposing multiple protocols, because of this only the TCP ports are exposed.  I am still trying to figure out
a good way to expose the UDP ports on the same IP address.  If you know how to do this please make a pull request!

# Installing

```
git clone ...
```

Open unifi-controller.yaml and make the appropriate changes for the PV and PVC for your enviornment.

```
cd unifi-controller-k8s-deployment
kubectl create -f ./unifi-controller.yaml
```

# Usage

Open your browser and navigate to http://YOUR K8S IP:8080

# Ports exposed

```
8080 (tcp)	required for Unifi to function
8081 (tcp)	Unifi communication port
8443 (tcp)	Unifi communication port
8843 (tcp)	Unifi communication port
8880 (tcp)	Unifi communication port
6789 (tcp)	For throughput test
```

# Ports that need to be exposed

These ports are required but as mentioned above you cannot mix protocols with type LoadBalancer

```
3478  (udp)	Unifi communication port
10001 (udp)	required for AP discovery
```

# My enviornment

* Four node Raspberry Pi4b 4GB cluster
* Ubuntu 18.04 arm64
* MetalLB
* Flannel
* Kubernetes 1.17.0
