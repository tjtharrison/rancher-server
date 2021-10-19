# rancher-server

Configuration for Rancher Management Server 


## Configuration

The Kubernetes and Docker deployments of Rancher are ready to deploy from this repository.

## Installation

### Docker

To run the Rancher server on a docker host, simply run the below to start the container listening on port 443.

```
sudo docker-compose up -d
```

### Kubernetes

To deploy the configuration on a Kubernetes host, create a new clusterrolebinding for Rancher before deploying the manifest files from this repository as such:

```
kubectl create clusterrolebinding permissive-binding --clusterrole=cluster-admin --user=admin --user=kubelet --user=kube-system --user=default --user=rancher --group=system:serviceaccounts
```

```
kubectl apply -f kubernetes/
```

Your Rancher server will now be deployed with a LoadBalancer service type - You can get the allocated IP Address and begin configuring Rancher:

```
kubectl get svc -n rancher --output jsonpath='{.status.loadBalancer.ingress[0].ip}'
```