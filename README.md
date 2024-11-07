# Reachability Demo

This demo deploys a container image with reachable vulnerabilities from [Damn Vulnerable GraphQL Application](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application). 

# Table of Contents
* [Prerequisites](#prerequisites)
* [Azure DevOps Configuration](#azure-devops-configuration)
* [GitHub Configuration](#github-configuration)
* [Disclaimer](#disclaimer)
* [License](#license)
/
# Prerequisites 
* Azure Kubernetes Service (AKS) Cluster to run the container in.
* Azure Container Registry (ACR) with an [admin account](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-authentication?tabs=azure-cli#admin-account). 
* [Connection between AKS cluster and ACR](https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration?tabs=azure-cli#configure-acr-integration-for-an-existing-aks-cluster).
* Endor Labs license.
* Defender CSPM license.
* Connector for Endor Labs in Defender for Cloud.
  
# Azuure DevOps Configuration
1. Clone this repository in Azure DevOps.
2. Create a service connection in Azure DevOps to Docker. Select 'Other' when you have to specify the type of connection. Here you must specify the container registry login server, username, and password that come from access keys in Azure Container Registry. 
![image](https://github.com/user-attachments/assets/a1535e01-9d22-4df8-8bf0-e83cf070ba34)
3. Create a service connection in Azure DevOps to Azure Resource Manager. Ensure that you give the service connection permissions to the relevant subscription and resource group that hosts your Kubernetes cluster. 
4. Create a variable group in Azure Pipelines called 'tenant-variables'. This is where you should store your ENDOR_API_CREDENTIALS_KEY, ENDOR_API_SECRET, and NAMESPACE information.
![image](https://github.com/user-attachments/assets/57d10b39-4af0-43a3-af16-9359e287bc48)
5. Create a new pipeline using the existing file located at AzurePipeline/azure-pipelines.yml.
6. Add the following variables to the pipeline: clusterName (name of the Kubernetes cluster to deploy the container on), containerRegistry (login server name for the Azure Container Registry, e.g., reachability.azurecr.io), dockerConnection (name of the service connection to Docker to push image to Azure Container Registry), resourceGroup (resource group that hosts the Kubernetes cluster), and subscription (name of the service connection name to Azure Resource Manager).
![image](https://github.com/user-attachments/assets/fd265dee-fbc5-4933-8b12-07e7ff76fefc)
7. Save and run the pipeline.
   
# GitHub Configuration
1. Clone this repository in GitHub.
2. Navigate to Settings > Secrets and Variables > Actions in the GitHub repository.
3. Create secrets for your ACR_USERNAME and ACR_PASSWORD. These come from Access Keys in ACR.
![image](https://github.com/user-attachments/assets/cc263e0c-b031-4a0d-acfb-7ea10719c634)
4. Create a variable for the ACR login server name (e.g., reachability.azurecr.io).
5. Create a new workflow using the existing file located at .github/workflows/containermapping.yml.
6. Save and run the workflow.
7. Deploy the container image from ACR to your AKS cluster in the Azure Portal. The easiest way to do this is to navigate to the AKS cluster and select Create > Create a quickstar application. Note that your registry and Kubernetes cluser must be [linked](https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration?tabs=azure-cli#configure-acr-integration-for-an-existing-aks-cluster) for this to work. To see the attack path, the container should be exposed via a service in Kubernetes. It is not recommended to do this in production tenants. 
![image](https://github.com/user-attachments/assets/74bb2699-1e89-4f34-9140-03bba0b75fae)
 

# Disclaimer

This container image is highly insecure, and as such, should not be deployed on internet facing servers in production environments. By default, the application is listening on 127.0.0.1 to avoid misconfigurations.

The container image is intentionally flawed and vulnerable, as such, it comes with no warranties. By using it, you take full responsibility for using it.

# License

It is distributed under the MIT License. See LICENSE for more information.
