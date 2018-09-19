# Azure Kubernetes Metrics Adapter Add-on

Add this add-on ot your json file as shown below to enable the Azure Kubernetes Metrics Adapter on your new cluster.

```json
{
    "apiVersion": "vlabs",
    "properties": {
      "orchestratorProfile": {
        "orchestratorType": "Kubernetes",
        "kubernetesConfig": {
          "addons": [
            {
              "name": "azure",
              "enabled" : true,
              "config": {
                  "region": "",
                  "name": ""
              }
            }
          ]
        }
      },
      "masterProfile": {
        "count": 1,
        "dnsPrefix": "",
        "vmSize": "Standard_DS2_v2",
      },
      "agentPoolProfiles": [
        {
          "name": "agentpool",
          "count": 3,
          "vmSize": "Standard_DS2_v2",
          "availabilityProfile": "VirtualMachineScaleSets"
        }
      ],
      "linuxProfile": {
        "adminUsername": "azureuser",
        "ssh": {
          "publicKeys": [
            {
              "keyData": ""
            }
          ]
        }
      },
      "servicePrincipalProfile": {
        "clientId": "",
        "secret": ""
      }
    }
  }

```

You can validate that the add-on is running as expected with the following commands:

You should see Azure k8s metrics adapter as `Running` after executing:

```bash
kubectl get pods -n kube-system
```

You should see Azure k8s metrics adapter node after executing:

```bash
kubectl get nodes
```

Follow the README at https://github.com/Azure/azure-k8s-metrics-adapter for examples.

## Configuration

|Name|Required|Description|Default Value|
|---|---|---|---|
|region|no|Azure region|"eastus"|
|name|no|container name|"azure-k8s-metrics-adapter"|
|image|no|Docker image|"mcr.microsoft.com/k8s/metrics/adapter:latest"|

## Supported Orchestrators

Kubernetes