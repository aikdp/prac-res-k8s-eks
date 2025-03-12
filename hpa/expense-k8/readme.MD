# HPA Horizontal Pod Autosacler
HPA should directs or selects only deployments, not directly to pod. because deploymets does replicas.
1. HPA need metrics server should installed
2. Resource requests and limits should provide inside pods to measure cpu utilisation of pods.

* metrics server
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

* Delete Metric Server
```
kubectl delete -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```