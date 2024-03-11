
# AKS support Local accounts

Download credentials on local machine.
az aks get-credentials --resource-group <RESOURCE GROUP NAME> --name <AKS Cluster Name>

# AKS support LOcal accounts and EntraId integration

But If you got the following error message:

```
kubectl get namespaces
```

```
Error from server (Forbidden): namespaces is forbidden: User "0d35dea9-595a-4cba-9b92-b0ee26b52271" cannot list resource "namespaces" in API group "" at the cluster scope: User does not have access to the resource in Azure. Update role assignment to allow access.
```

## Admin mode (--admin)
az aks get-credentials --resource-group <RESOURCE GROUP NAME> --name <AKS Cluster Name> --admin


