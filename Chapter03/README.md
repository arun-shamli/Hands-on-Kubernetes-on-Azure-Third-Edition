#### log in into a pod and run redis-cli
kubectl exec -it redis-master-766c5cf5c8-7rc58 -- redis-cli

### command to list pods acros all namespaces
kubectl get pod --all-namespaces

```
kubectl get storageclass
kubectl get pvc

helm ls
helm status handsonakswp

helm delete handsonakswp
kubectl delete pvc --all
```
