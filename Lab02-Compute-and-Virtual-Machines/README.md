# Lab 02 – Compute and Virtual Machines
This lab expands Tremols Tech’s Azure environment into the compute layer. It covers the full spectrum of Azure compute services, from traditional virtual machines to modern PaaS and serverless container platforms. This lab establishes Tremols Tech’s compute foundation, combining VM deployment, scaling, automation, web hosting, and containerized workloads into a single unified workflow.

## 📘 Lab Overview
Tremols Tech is preparing a flexible and scalable compute environment capable of hosting:
- Virtual machines for traditional workloads
- VM Scale Sets for horizontal scaling
- Infrastructure‑as‑Code for repeatable deployments
- Web Apps for PaaS hosting
- Container Instances for lightweight workloads
- Container Apps for microservices and serverless containers
##### This lab walks through the exact steps used by real cloud administrators and MSPs to deploy, scale, automate, and host applications across Azure’s compute ecosystem.

## 🔧 Part 1 – Virtual Machines & VM Scale Sets (IaaS Compute)
This section focuses on Azure’s infrastructure‑based compute services.

### Scenario
Tremols Tech wants to deploy resilient virtual machines, explore VM scaling, and evaluate Virtual Machine Scale Sets for automated horizontal scaling.

### Tasks Completed

#### 1. Deployed Zone‑Resilient Virtual Machines
I deployed two Windows Server VMs across Availability Zones 1 and 2 to achieve the 99.99% SLA.
Configured:
- Premium SSD OS disk
- No public inbound ports
- Standard_D2s_v5 VM size
- Zone redundancy

#### 2. Scaled VM Compute & Storage
I resized VM compute from D2s_v5 → D4s_v5, doubling CPU and memory.
I also:
- Added a data disk
- Detached it
- Converted it from Standard HDD → Standard SSD
- Reattached it to the VM

#### 3. Created a Virtual Machine Scale Set (VMSS)
I deployed a VMSS across Zones 1, 2, and 3 with:
- Uniform orchestration
- Windows Server 2025 image
- Custom VNet + NSG
- Public load balancer
- Autoscale‑ready configuration

#### 4. Configured Autoscaling Rules
I created:
- Scale‑out rule: Increase instances by 50% when CPU > 70% for 10 minutes
- Scale‑in rule: Decrease instances by 20% when CPU < 30% for 10 minutes
- Instance limits: Min 2, Max 10

#### 5. Created a VM Using PowerShell
New-AzVM `
 -ResourceGroupName 'az104-rg8' `
 -Name 'myPSVM' `
 -Location 'East US' `
 -Image 'Win2019Datacenter' `
 -Zone '1' `
 -Size 'Standard_D2s_v5' `
 -Credential (Get-Credential)

#### 6. Created a VM Using Azure CLI
Used CLI to deploy a Linux VM:
###### az vm create --name myCLIVM --resource-group az104-rg8 --image UbuntuLTS --admin-username localadmin --generate-ssh-keys

## 📦 Part 2 – Infrastructure‑as‑Code: ARM Templates & Bicep
This section focuses on automating compute deployments.

### Scenario
Tremols Tech wants consistent, repeatable deployments using ARM templates and Bicep.

### Tasks Completed

#### 1. Exported an ARM Template
I created a managed disk and exported its ARM template + parameters.

#### 2. Modified and Redeployed the Template
I updated:
- Disk name
- Parameter names
- Deployment values
Then redeployed using Custom Deployment.

#### 3. Deployed ARM Template via PowerShell
### PowerShell
###### New-AzResourceGroupDeployment -ResourceGroupName az104-rg3 -TemplateFile template.json -TemplateParameterFile parameters.json

#### 4. Deployed ARM Template via CLI
###### az deployment group create --resource-group az104-rg3 --template-file template.json --parameters parameters.json

#### 5. Deployed a Bicep Template
###### az deployment group create --resource-group az104-rg3 --template-file azuredeploydisk.bicep


## 🌐 Part 3 – Web Apps (App Service)
This section focuses on Azure’s PaaS web hosting platform.

### Scenario
Tremols Tech wants to migrate on‑premises PHP websites to Azure Web Apps.

### Tasks Completed

#### 1. Created a Web App
Configured:
- PHP 8.2 runtime
- Linux App Service Plan (Premium V3)
- Zone redundancy

#### 2. Created a Staging Deployment Slot
Used deployment slots for safe testing before production swaps.

#### 3. Configured GitHub Deployment
Connected staging slot to:
- Code
https://github.com/Azure-Samples/php-docs-hello-world

#### 4. Swapped Staging → Production
Performed a slot swap to promote tested code.

#### 5. Configured Autoscaling
Set:
- Minimum instances: 1
- Maximum burst: 2
Then performed a load test to validate scaling behavior.

## 🐳 Part 4 – Containers: ACI & ACA
This section focuses on serverless container hosting.

### Scenario
Tremols Tech wants lightweight container hosting without managing Kubernetes clusters.

### Tasks Completed

#### 1. Deployed Azure Container Instance (ACI)
Used quickstart Docker image:
- Code
mcr.microsoft.com/azuredocs/aci-helloworld:latest
Configured DNS label and verified public endpoint.

#### 2. Reviewed Container Logs
Validated HTTP GET logs from browser requests.

#### 3. Deployed Azure Container App (ACA)
Created:
- ACA environment
- “my-app” container app
- Hello World quickstart image
- Public ingress

#### 4. Verified ACA Deployment
Opened the ACA URL and confirmed the Hello World response.

## 📝 Notes & Observations
- Azure Compute spans IaaS, PaaS, and serverless containers.
- VMSS autoscaling is ideal for fluctuating workloads.
- ARM/Bicep templates ensure consistent deployments.
- Web Apps simplify hosting without managing servers.
- ACI is perfect for short‑lived container tasks.
- ACA provides serverless microservices without Kubernetes complexity.

## 🎯 Why This Lab Matters
Compute is the backbone of application hosting in Azure.
This lab establishes Tremols Tech’s compute foundation:
- How workloads are deployed
- How compute scales automatically
- How infrastructure is automated
- How applications are hosted
- How containers run without servers
Everything else (networking, storage, backup, analytics) depends on compute being deployed cleanly and consistently.

## 🧹 Cleanup
Portal
- Delete the resource groups
- Delete VMSS
- Delete Web Apps
- Delete Container Apps
- Delete Container Instances

### PowerShell
###### Remove-AzResourceGroup -Name az104-rg8
###### Remove-AzResourceGroup -Name az104-rg3
###### Remove-AzResourceGroup -Name az104-rg9

### CLI
###### az group delete --name az104-rg8
###### az group delete --name az104-rg3
###### az group delete --name az104-rg9

## 📈 Next Lab
[➡️ Networking & Connectivity](https://github.com/JTremols-Cloud/Azure-AZ104-Labs/tree/106304e209dfa7b6a45a4be615253a480ba4ce9f/Lab03-Networking-and-Connectivity)
