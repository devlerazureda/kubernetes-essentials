#### Pod Affinity
```bash
kubectl apply -f 02-podaffinity.yaml
kubectl describe pod with-pod-affinity
```

```
Events:
  Type     Reason             Age              From                Message
  ----     ------             ----             ----                -------
  Warning  FailedScheduling   6s (x2 over 6s)  default-scheduler   0/7 nodes are available: 7 node(s) didn't match pod affinity rules, 7 node(s) didn't match pod affinity/anti-affinity.
  Normal   NotTriggerScaleUp  5s               cluster-autoscaler  pod didn't trigger scale-up (it wouldn't fit if a new node is added): 1 node(s) didn't match pod affinity/anti-affinity, 1 node(s) didn't match pod affinity rules
```

```bash
kubectl run nginx --image=nginx --labels=security=S1 --restart=Never
watch -n2 kubectl get pods 
```

#### Taints and Tolerations
NoSchedule | PreferNoSchedule  | NoExecute

```bash
kubectl taint node aks-nodepool1-17949986-vmss000013 os=windows:NoSchedule
kubectl label node aks-nodepool1-17949986-vmss000013 cpu=kotu
kubectl apply -f 03-tolerated-pod.yaml
kubectl taint node aks-nodepool1-17949986-vmss000013 os:NoExecute-
```

#### Cordon/Drain
```bash
kubectl apply -f 04-single-pod.yaml
kubectl cordon node aks-nodepool1-17949986-vmss000013
kubectl drain node aks-nodepool1-17949986-vmss000013  --ignore-daemonsets
kubectl delete pod nginx
kubectl drain node aks-nodepool1-17949986-vmss000013  --ignore-daemonsets
kubectl get pods
kubectl uncordon aks-nodepool1-17949986-vmss000013
```
