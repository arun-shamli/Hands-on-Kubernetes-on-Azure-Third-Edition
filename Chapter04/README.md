

#### increase the number of pods
kubectl scale deployment redis-replica --replicas 5

---
#### autoscale the cluster

  
```
az aks nodepool update --enable-cluster-autoscaler \
  -g rg-handsonaks --cluster-name handsonaks \
  --name agentpool --min-count 1 --max-count 2
  
  kubectl delete -f guestbook-all-in-one.yaml

  az aks nodepool update --disable-cluster-autoscaler \
  -g rg-handsonaks --cluster-name handsonaks --name agentpool001

  az aks nodepool scale --node-count 2 -g rg-handsonaks \
  --cluster-name handsonaks --name agentpool001

```

kubectl get replicaset

kubectl rollout history deployment frontend

kubectl rollout undo deployment frontend

kubectl patch deployment frontend \
--patch "$(cat frontend-image-patch.yaml)"


## Helm update
```



kubectl get secret wp-mariadb -o yaml
Mariadb
username:LoWRY3vhQt
password:Rwp13fqMHU

kubectl get secret wp-wordpress -o yaml
mEufX7a77X

helm upgrade wp bitnami/wordpress \
  --set mariadb.image.tag=10.5.13-debian-10-r12\
  --set mariadb.auth.password="LoWRY3vhQt" \
  --set mariadb.auth.rootPassword="Rwp13fqMHU" \
  --set wordpressPassword="mEufX7a77X" \
&& kubectl get pods -w
  
```
