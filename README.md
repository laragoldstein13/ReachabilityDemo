# Reachability Demo

This demo deploys a container image with reachable vulnerabilities from [Damn Vulnerable GraphQL Application](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application). 

# Table of Contents
* [Prerequisites](#prerequisites)
* [Azure DevOps Configuration](#azure-devops-configuration)
* [GitHub Configuration](#github-configuration)
* [Disclaimer](#disclaimer)
* [License](#license)

# Prerequisites 
* Azure Kubernetes Service Cluster to run the container in
* Azure Container Registry
  
# Azuure DevOps Configuration

DVGA supports Beginner and Expert level game modes, which will change the exploitation difficulty.

# GitHub Configuration


# Disclaimer

This container image is highly insecure, and as such, should not be deployed on internet facing servers in production environments. By default, the application is listening on 127.0.0.1 to avoid misconfigurations.

The container image is intentionally flawed and vulnerable, as such, it comes with no warranties. By using it, you take full responsibility for using it.

# License

It is distributed under the MIT License. See LICENSE for more information.
