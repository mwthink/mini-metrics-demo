# mini-metrics-demo
Showing off metrics with Minikube. 

We will start with a fresh minikube, then install a prometheus stack via
the prometheus operator.

## Prerequisites
- minikube
- kubectl
- helm 3

## Quick Start
Start minikube
```sh
minikube start --cpus=2 --memory=4096
```

Configure Helm repo and install prometheus-operator chart
```sh
# setup stable repo
helm repo add stable https://kubernetes-charts.storage.googleapis.com
helm repo update

# install chart
helm install prometheus-operator stable/prometheus-operator --namespace kube-system --set prometheusOperator.createCustomResource=false --set prometheus.service.type=NodePort --set grafana.service.type=NodePort --set grafana.adminPassword=password
```

To access web UIs
```sh
# grafana
# credentials = admin / password
minikube service -n kube-system prometheus-operator-grafana

# prometheus
minikube service -n kube-system prometheus-operator-prometheus
```


## Useful Queries
```
sum(kube_pod_labels{namespace="default",label_user_id="100"})
```
