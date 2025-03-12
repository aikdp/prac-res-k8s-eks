# Taints ans Tolerations
## Taints:
```
kubectl taint nodes node1 key1=value1:NoSchedule

kubectl taint nodes <node-ip> hardware=gpu:Noschedule
```

* Untaint: at last put hyphen (-)
```
kubectl taint nodes node1 key1=value1:NoSchedule-

kubectl taint nodes <node-ip> hardware=gpu:Noschedule-
```
