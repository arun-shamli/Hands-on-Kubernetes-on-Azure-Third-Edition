kubectl create -f azure-vote.yaml

kubectl get pods --watch

**kubectl get service azure-vote-front --watch**
get the public IP of the load balancer

**kubectl get all**
To see all the objects in Kubernetes that were created for your application

**kubectl delete -f azure-vote.yaml**
