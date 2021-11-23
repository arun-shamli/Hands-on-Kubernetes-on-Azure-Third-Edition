## ACR

```
az acr login --name ak8017acr

az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table

az acr repository list --name ak8017acr --output table

az acr repository show-tags --name ak8017acr --repository azure-vote-front --output table
```

## AKS

```
az aks create \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --node-count 2 \
    --generate-ssh-keys 

az aks update -n myAKSCluster -g myResourceGroup --attach-acr $(az acr show -n ak8017acr --query "id" -o tsv) 

az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

az aks show --resource-group myResourceGroup --name myAKSCluster --query kubernetesVersion --output table

```

kubectl scale --replicas=3 deployment/azure-vote-front

kubectl set image deployment azure-vote-front azure-vote-front=ak8017acr.azurecr.io/azure-vote-front:v2
