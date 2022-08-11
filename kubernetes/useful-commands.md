# The official cheatsheet is here
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
```
# List all services in the current namespace
kubectl get all

# List all services in all namespaces
kubectl get all --all-namespaces

# Edit a service
kubectl edit <type> <name>

# Change CLI to a different namespace
kubectl config set-context $(kubectl config current-context) --namespace <name_of_your_namespace>

# Generating quick files
kubectl create deployment --image=nginx nginx --dry-run -o yaml
```
