# Lab 02 – Compute and Virtual Machines
This lab expands Tremols Tech’s Azure environment into the compute layer as part of the cloud modernization project for ClearView Dental Associates. It covers the full spectrum of Azure compute services used by modern MSPs, from traditional virtual machines to autoscaling VMSS, Infrastructure‑as‑Code deployments, PaaS web hosting, and serverless containers.

This lab establishes the compute foundation ClearView Dental Associates will rely on as their clinical, imaging, and practice management workloads begin migrating into Azure.

## 📘 Lab Overview
Tremols Tech is building a flexible, scalable compute environment to support ClearView Dental Associates’ future cloud workloads. This includes imaging systems, clinical applications, and practice management software. Before these workloads can be migrated, Tremols Tech must establish:
- Resilient virtual machines
- Autoscaling VM Scale Sets
- Infrastructure‑as‑Code deployment pipelines
- PaaS web hosting for application modernization
- Serverless container hosting for lightweight workloads

###### This lab mirrors the exact workflow used by real cloud administrators and MSPs when designing compute architectures for healthcare clients.

## 🔧 Part 1 – Virtual Machines & VM Scale Sets (IaaS Compute)
This section focuses on Azure’s infrastructure‑based compute services.

### Scenario
ClearView Dental Associates is preparing to migrate several on‑premises workloads into Azure, including imaging servers, practice management software, and internal administrative systems. Tremols Tech must evaluate Azure’s IaaS compute options to determine how ClearView’s workloads will be hosted, scaled, and protected in the cloud.

This requires deploying resilient VMs, testing scaling operations, and validating VM Scale Sets for future imaging workloads.

### Tasks Completed

#### 1. Deployed Zone‑Resilient Virtual Machines
To simulate ClearView’s imaging and clinical workloads, I deployed two Windows Server VMs across Availability Zones 1 and 2 to achieve Azure’s 99.99% SLA.
Configured:
- Premium SSD OS disk
- No public inbound ports (HIPAA‑aligned security)
- Standard_D2s_v5 VM size
- Zone redundancy

#### 2. Scaled VM Compute & Storage
To model ClearView’s workload growth such as an imaging storage expansion, VM compute was scaled from D2s_v5 → D4s_v5, doubling CPU and memory.
Storage operations included:
- Adding a data disk
- Detaching the disk
- Converting Standard HDD → Standard SSD
- Reattaching the disk
###### These operations simulate ClearView’s future imaging storage lifecycle.

#### 3. Created a Virtual Machine Scale Set (VMSS)
I deployed a VMSS across Zones 1, 2, and 3 with:
- Uniform orchestration
- Windows Server 2025 image
- Custom VNet + NSG
- Public load balancer
- Autoscale‑ready configuration

#### 4. Configured Autoscaling Rules
Autoscaling rules were configured to simulate ClearView’s peak imaging hours:
- Scale‑out: +50% instances when CPU > 70% for 10 minutes
- Scale‑in: −20% instances when CPU < 30% for 10 minutes
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
ClearView Dental Associates requires consistent, repeatable deployments for imaging servers, clinical applications, and administrative workloads. Tremols Tech must implement Infrastructure‑as‑Code (IaC) to ensure ClearView’s environments can be deployed reliably across development, test, and production.

### Tasks Completed

#### 1. Exported an ARM Template
Exported a managed disk template to demonstrate how ClearView’s storage resources can be automated.

#### 2. Modified and Redeployed the Template
I updated:
- Disk name
- Parameter names
- Deployment values
Then redeployed using Custom Deployment to simulate ClearView’s future automated provisioning pipeline.

#### 3. Deployed ARM Template via PowerShell
###### New-AzResourceGroupDeployment -ResourceGroupName az104-rg3 -TemplateFile template.json -TemplateParameterFile parameters.json

#### 4. Deployed ARM Template via CLI
###### az deployment group create --resource-group az104-rg3 --template-file template.json --parameters parameters.json

#### 5. Deployed a Bicep Template
###### az deployment group create --resource-group az104-rg3 --template-file azuredeploydisk.bicep


## 🌐 Part 3 – Web Apps (App Service)
This section focuses on Azure’s PaaS web hosting platform.

### Scenario
ClearView Dental Associates plans to modernize several internal web applications, including patient portals and administrative dashboards. Tremols Tech must evaluate Azure Web Apps as a PaaS hosting option to reduce operational overhead and improve reliability.

### Tasks Completed

#### 1. Created a Web App
Configured:
- PHP 8.2 runtime (matching ClearView’s legacy web apps)
- Linux App Service Plan (Premium V3)
- Zone redundancy

#### 2. Created a Staging Deployment Slot
Used deployment slots to simulate ClearView’s safe testing workflow before promoting updates to production.

#### 3. Configured GitHub Deployment
Connected staging slot to a GitHub repo, demonstrating CI/CD workflows ClearView will adopt.
<!-- (INPUT LINK HERE) -->

#### 4. Swapped Staging → Production
Performed a slot swap to simulate ClearView’s production release process.

#### 5. Configured Autoscaling
Configured autoscaling to handle ClearView’s peak patient portal usage hours. 
Set:
- Minimum instances: 1
- Maximum burst: 2
Then performed a load test to validate scaling behavior.

## 🐳 Part 4 – Containers: ACI & ACA
This section focuses on serverless container hosting.

### Scenario
ClearView Dental Associates uses several lightweight vendor applications that do not require full VMs. Tremols Tech must evaluate Azure Container Instances (ACI) and Azure Container Apps (ACA) as serverless hosting options for ClearView’s microservices and imaging processing utilities.

### Tasks Completed

#### 1. Deployed Azure Container Instance (ACI)
Used quickstart Docker image:
- mcr.microsoft.com/azuredocs/aci-helloworld:latest
Configured DNS label and verified public endpoint.

#### 2. Reviewed Container Logs
Validated HTTP GET logs from browser requests.

#### 3. Deployed Azure Container App (ACA)
Next, I deployed an ACA environment to evaluate long‑running microservices.
Configured:
- Dedicated ACA environment
- A container app simulating a vendor microservice
- Ingress enabled for controlled public access
- Autoscaling rules ready for future configuration

###### ACA is ideal for ClearView's appointment synchronization microservices, imaging metadata processors, and patient portal background services

#### 4. Verified ACA Deployment
Opened the ACA endpoint and confirmed the container responded correctly, validating ACA as a viable hosting platform for ClearView’s future microservices.

## 📝 Notes & Observations
- Azure Compute spans IaaS, PaaS, and serverless containers.
- VMSS autoscaling is ideal for fluctuating workloads.
- ARM/Bicep templates ensure consistent deployments.
- Web Apps simplify hosting without managing servers.
- ACI is perfect for short lived container tasks.
- ACA provides serverless microservices without Kubernetes complexity.

## 🎯 Why This Lab Matters
Compute is the backbone of application hosting in Azure.
This lab establishes Tremols Tech’s compute foundation for ClearView Dental Associates:
- How workloads are deployed
- How compute scales automatically
- How infrastructure is automated
- How applications are hosted
- How containers run without servers
- 
###### Everything else (networking, storage, backup, analytics) depends on compute being deployed cleanly and consistently.

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
