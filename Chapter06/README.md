

**Switiching from Staging to production**
```
kubectl create -f certificate-issuer-prod.yaml
kubectl apply -f ingress-with-tls-prod.yaml

#cleanup
kubectl delete -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.yaml

az aks disable-addons -n handsonaks -g rg-handsonaks -a ingress-appgw

```
