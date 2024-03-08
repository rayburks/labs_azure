
# Voraussetzungen

az --version
az extension add --upgrade --name azure-iot-ops

# Systemanforderungen

**AKS Edge Essentials Single-Machine K3S-Cluster** für Linux einzurichten. 
- mindestens über 10 GB RAM
- 4 vCPUs und 
- 40 GB freien Speicherplatz 

# Installation unter Linux

## K3s-Installationsskript

```
sudo curl -sfL https://get.k3s.io | sh -
```

## K3s Konfiguration

```bash
mkdir ~/.kube
sudo KUBECONFIG=~/.kube/config:/etc/rancher/k3s/k3s.yaml kubectl config view --flatten > ~/.kube/merged
mv ~/.kube/merged ~/.kube/config
chmod  0600 ~/.kube/config
export KUBECONFIG=~/.kube/config
#switch to k3s context
kubectl config use-context default
```

## NFS-Common

```
sudo apt-get update
sudo apt install nfs-common
```

## Grenzwerte für die Überwachung zu erhöhen

```bash
echo fs.inotify.max_user_instances=8192 | sudo tee -a /etc/sysctl.conf
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
echo fs.file-max = 100000 | sudo tee -a /etc/sysctl.conf

sudo sysctl -p
```

## Verbindung zum Cluster

az login
export SUBSCRIPTION_ID=<SUBSCRIPTION_ID>
export SUBSCRIPTION_ID=0f9ae2bf-d8f0-4c62-b655-d635a28fca2f
export LOCATION="westeurope"
export RESOURCE_GROUP="azureiot-rg"
export CLUSTER_NAME="azureiot-playground-aks"

az account set -s $SUBSCRIPTION_ID

az provider register -n "Microsoft.ExtendedLocation"
az provider register -n "Microsoft.Kubernetes"
az provider register -n "Microsoft.KubernetesConfiguration"
az provider register -n "Microsoft.IoTOperationsOrchestrator"
az provider register -n "Microsoft.IoTOperationsMQ"
az provider register -n "Microsoft.IoTOperationsDataProcessor"
az provider register -n "Microsoft.DeviceRegistry"

az group create --location $LOCATION --resource-group $RESOURCE_GROUP --subscription $SUBSCRIPTION_ID

az connectedk8s connect -n $CLUSTER_NAME -l $LOCATION -g $RESOURCE_GROUP --subscription $SUBSCRIPTION_ID

az ad sp show --id bc313c14-388c-4e7d-a58e-70017303ee3b --query id -o tsv

export OBJECT_ID=<objectID from the previous step>

export OBJECT_ID=63f407ac-0048-4fe9-bf73-57d05a47ad1a
az connectedk8s enable-features -n $CLUSTER_NAME -g $RESOURCE_GROUP --custom-locations-oid $OBJECT_ID --features cluster-connect custom-locations

az iot ops verify-host

## Keyvault erzeugen für AzureIot Operations (Access-Policies)

az keyvault create --enable-rbac-authorization false --name "azureiot-kv" --resource-group $RESOURCE_GROUP

## AzureIot Operations in Cluster bereitstellen

az iot ops init --cluster azureiot-playground-aks -g azureiot-rg --kv-id /subscriptions/0f9ae2bf-d8f0-4c62-b655-d635a28fca2f/resourceGroups/azureiot-rg/providers/Microsoft.KeyVault/vaults/azureiot-kv

## Zugriff auf azure-arc basierten Cluster per Token

[Reference]([https://](https://learn.microsoft.com/de-de/azure/azure-arc/kubernetes/cluster-connect?tabs=azure-cli%2Cagent-version#service-account-token-authentication-option))

kubectl create serviceaccount demo-user -n default
kubectl create clusterrolebinding demo-user-binding --clusterrole cluster-admin --serviceaccount default:demo-user
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: demo-user-secret
  annotations:
    kubernetes.io/service-account.name: demo-user
type: kubernetes.io/service-account-token
EOF
TOKEN=$(kubectl get secret demo-user-secret -o jsonpath='{$.data.token}' | base64 -d | sed 's/$/\n/g')
echo $TOKEN

Payload Token
{
  "iss": "kubernetes/serviceaccount",
  "kubernetes.io/serviceaccount/namespace": "default",
  "kubernetes.io/serviceaccount/secret.name": "demo-user-secret",
  "kubernetes.io/serviceaccount/service-account.name": "demo-user",
  "kubernetes.io/serviceaccount/service-account.uid": "815b5957-d103-4a24-9562-d1082121c4d1",
  "sub": "system:serviceaccount:default:demo-user"
}









