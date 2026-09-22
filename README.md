# AZ-104 Azure Administration Journey

This repository documents my hands-on Azure administration journey through a series of real world infrastructure labs built around a simulated cloud modernization engagement.

Rather than approaching Azure as isolated technical exercises, each lab is designed as part of a multi-phase cloud adoption project where Tremols Tech, an emerging Managed Service Provider (MSP), is responsible for onboarding ClearView Dental Associates, a mid-size healthcare organization, into Microsoft Azure.

The objective is to build a secure, scalable, and production-ready Azure environment while applying the same governance, operational, and architectural practices used by enterprise cloud teams and MSPs.

## ☁️ Project Scenario
ClearView Dental Associates operates multiple dental clinics and employs approximately 180 staff members across administrative, clinical, and imaging departments.

As ClearView begins migrating workloads to Azure, Tremols Tech must design and implement a complete cloud foundation that supports:
- Identity and access management
- Governance and compliance controls
- Compute and application hosting
- Secure networking
- Storage and backup strategies
- Monitoring and operational visibility

###### Each lab represents a major phase of that cloud adoption journey.

## Lab 01 - Identity & Access Management  
Establishes the governance and security foundation for the Azure environment. 
- Microsoft Entra ID users and guest accounts
- Security groups and membership management
- Management Groups
- Role-Based Access Control (RBAC)
- Custom Azure roles
- Azure Policy
- Resource tagging strategies
- Resource locks and governance enforcement

###### Outcome: Created a secure identity and governance baseline that future Azure resources can inherit.

## Lab 02 - Compute & Virtual Machines  
Builds the compute foundation required to host clinical and business workloads.
- Azure Virtual Machines
- Availability Zones
- VM storage management
- Azure VM Scale Sets (VMSS)
- Autoscaling configurations
- ARM Templates
- Bicep deployments
- Azure App Service
- Azure Container Instances (ACI)
- Azure Container Apps (ACA)
- PowerShell and Azure CLI deployments

###### Outcome: Deployed scalable compute infrastructure supporting traditional servers, web applications, and containerized workloads.

## Lab 03 - Networking & Connectivity  
Focuses on secure communication between Azure resources and external environments.
- Virtual Networks (VNets)
- Subnets
- Network Security Groups (NSGs)
- VNet Peering
- VPN Gateways
- Private Endpoints
- Load Balancers
- DNS and connectivity services

###### Outcome: Establish secure and reliable network architecture for cloud hosted workloads.

## Lab 04 - Storage & Backup 
Implements data protection, lifecycle management, and business continuity strategies.
- Azure Storage Accounts
- Blob Storage
- Azure Files
- Lifecycle Management
- Recovery Services Vaults
- Azure Backup
- Snapshot Management
- Disaster Recovery concepts

###### Outcome: Ensure organizational data remains secure, recoverable, and compliant.

## Lab 05 - Analytics & Logs  
Provides operational visibility and monitoring capabilities across the Azure environment.
- Azure Monitor
- Log Analytics
- Metrics and Alerts
- Diagnostic Settings
- Workbooks and Dashboards
- Kusto Query Language (KQL)
- Operational Reporting

###### Outcome: Enable proactive monitoring and troubleshooting of Azure workloads.

## 🔧 What Each Lab Includes:
Each lab is fully documented and contains:
- Real world business scenario
- Step-by-step implementation walkthrough
- Azure Portal procedures
- PowerShell examples
- Azure CLI examples
- Infrastructure-as-Code examples where applicable
- Screenshots and validation steps
- Notes and observations
- Cleanup procedures
- MSP focused operational context

###### The goal is not simply to deploy Azure resources, but to understand why they are deployed, how they fit together, and how they support business objectives.

## 🎯 Purpose of This Repository
- Demonstrate practical Azure administration skills
- Apply AZ-104 concepts through hands-on implementation
- Build a professional cloud portfolio
- Document Tremols Tech operational standards
- Develop repeatable deployment and governance practices
- Create reference material for future Azure projects
- Support progression toward Azure Administrator and Cloud Engineer roles

###### Every lab is written from the perspective of an administrator designing and operating Azure environments, not simply completing a certification exercise.

## 📈 Future Enhancements
As the project evolves, additional content will be added including:
- Advanced PowerShell automation
- Azure CLI deployment workflows
- Bicep and Infrastructure-as-Code templates
- Governance baselines and policy initiatives
- Monitoring dashboards and operational reporting
- Backup and disaster recovery strategies
- Networking architecture diagrams
- Security hardening procedures
- Azure landing zone design patterns

###### This repository represents the ongoing Azure cloud journey of Tremols Tech as it develops a complete cloud foundation for ClearView Dental Associates using industry standard administration, governance, and operational practices.
