# verify k8s rbac installed 
kubectl api-versions | grep rbac

# create namespace 
kubectl create namespace rahasak

# create service account
kubectl apply -f rahasak-service-account.yaml

# view service accounts
# service account created in rahasak namespace
kubectl get serviceaccounts -n rahasak

# create role
kubectl apply -f rahasak-role.yaml

# list roles in rahasak namespace
kubectl get roles -n rahasak

# describe role permissions
kubectl describe role pod-reader -n rahasak

# create role binding
kubectl apply -f rahasak-role-binding.yaml

# list role binding
kubectl get rolebindings -n rahasak

# describe role binding
kubectl describe rolebindings pod-reader-binding -n rahasak

### Test Permissions

# deploy pod with kubectl
kubectl apply -f rahasak-kubectl.yaml

# list pods
kubectl get pods -n rahasak

# connect to kubectl pod
kubectl exec -it --namespace=rahasak rahasak-kubectl -- /bin/bash

# check list pod permission in rahasak
# permission should be there
root@debug-kubectl:/# kubectl get pods -n rahasak

# check list pod permission in kube-system
# give forbidden error
root@debug-kubectl:/# kubectl get pods -n kube-system

