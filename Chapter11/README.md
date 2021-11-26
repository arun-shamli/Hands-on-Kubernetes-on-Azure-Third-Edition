```
az aks delete -n handsonaks -g rg-handsonaks -y

az group create -l eastus -n rg-handsonaks

az network vnet create -o table \
  --resource-group rg-handsonaks \
  --name vnet-handsonaks \
  --address-prefixes 192.168.0.0/16 \
  --subnet-name akssubnet \
  --subnet-prefix 192.168.0.0/24

VNET_SUBNET_ID=$(az network vnet subnet show   --resource-group rg-handsonaks   --vnet-name vnet-handsonaks   --name akssubnet --query id -o tsv)

az identity create --name handsonaks-mi --resource-group rg-handsonaks

IDENTITY_CLIENTID=$(az identity show --name handsonaks-mi \
  --resource-group rg-handsonaks \
  --query clientId -o tsv)

az role assignment create --assignee $IDENTITY_CLIENTID --scope $VNET_SUBNET_ID --role Contributor

IDENTITY_ID=$(az identity show --name handsonaks-mi   --resource-group rg-handsonaks   --query id -o tsv)


az aks create \
  --resource-group rg-handsonaks \
  --name handsonaks \
  --vnet-subnet-id $VNET_SUBNET_ID \
  --enable-managed-identity \
  --assign-identity $IDENTITY_ID \
  --enable-private-cluster \
  --node-count 1 \
  --node-vm-size Standard_DS2_v2 \
  --ssh-key-value /home/ak8017/.ssh/arun.shamli.id_rsa.pub


az aks get-credentials -n handsonaks -g rg-handsonaks
```

## Creating the VM and private link
```
az network vnet subnet create \
--resource-group rg-handsonaks \
--vnet-name vnet-handsonaks \
--name vmsubnet \
--address-prefix 192.168.1.0/24

VM_SUBNET_ID=$(az network vnet subnet show \
--resource-group rg-handsonaks \
--vnet-name vnet-handsonaks \
--name vmsubnet --query id -o tsv)

az group create -l eastus --name rg-handsonaks-vm

USERID=ak8017
SSH_PUBLIC_KEY=/home/ak8017/.ssh/arun.shamli.id_rsa.pub

az vm create --name vm-handsonaks \
--resource-group rg-handsonaks-vm \
--image UbuntuLTS \
--admin-username $USERID \
--ssh-key-values $SSH_PUBLIC_KEY \
--subnet $VM_SUBNET_ID \
--size Standard_D2_v2
PUBLIC_IP="40.121.242.78"
scp -i arun.shamli.id_rsa ~/.kube/config ak8017@4$PUBLIC_IP:~
ssh -i arun.shamli.id_rsa ak8017@$PUBLIC_IP
```

