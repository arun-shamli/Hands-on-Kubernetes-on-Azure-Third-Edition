

#### increase the number of pods
kubectl scale deployment redis-replica --replicas 5

---
#### autoscale the cluster
az aks nodepool update --enable-cluster-autoscaler \
  -g rg-handsonaks --cluster-name handsonaks \
  --name agentpool --min-count 1 --max-count 2
  
```
  kubectl delete -f guestbook-all-in-one.yaml

  az aks nodepool update --disable-cluster-autoscaler \
  -g rg-handsonaks --cluster-name handsonaks --name agentpool

  az aks nodepool scale --node-count 2 -g rg-handsonaks \
  --cluster-name handsonaks --name agentpool

```

kubectl get replicaset

kubectl rollout history deployment frontend


