```

az aks create \
--resource-group rg-handsonaks \
--name handsonaks \
--enable-managed-identity \
--node-count 2 \
--node-vm-size Standard_DS2_v2 \
--ssh-key-value /home/ak8017/.ssh/arun.shamli.id_rsa.pub \
--network-plugin azure \
--network-policy azure

az aks update -n handsonaks -g rg-handsonaks --attach-acr ak8017

az ad sp create-for-rbac --name "cicd-pipeline" --sdk-auth --role contributor

```
