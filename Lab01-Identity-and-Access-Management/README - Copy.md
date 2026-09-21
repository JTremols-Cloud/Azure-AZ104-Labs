# Lab 01 – Identity and Access Management

This lab marks the start of Tremols Tech’s Azure Cloud Foundation project. As an early‑stage MSP contracted by ClearView Dental Associates, a mid‑size dental organization, Tremols Tech is responsible for modernizing their IT operations by migrating identity, governance, and core workloads into Microsoft Azure.



The dental organization operates multiple clinics, relies heavily on patient management software, imaging systems, and secure data workflows, and needs a compliant, well‑structured cloud foundation before any workloads can be migrated.



This lab establishes Tremols Tech’s identity, access, and governance baseline, forming Phase 1 of a real MSP cloud adoption engagement.



## 📘 Lab Overview

Before compute, networking, storage, or clinical applications can be deployed, Tremols Tech must establish a secure identity and governance layer that ensures: 

* Clean and compliant identity structure
* Role‑based access control aligned with least privilege
* Management group hierarchy for subscription governance
* Azure Policy enforcement for tagging, compliance, and resource hygiene
* Resource protection to prevent accidental deletion



##### This lab walks through the exact steps MSPs take when onboarding dental organizations into Azure, especially those with HIPAA sensitive workloads. 



## 🔐 Part 1 - Identity: Users, Guests \& Groups

This section focuses on core identity objects in Microsoft Entra ID.

### Scenario

* The dental organization is onboarding several IT engineers and external imaging‑software consultants who need access to pre‑production virtual machines and test resources. Tremols Tech must create internal identities, invite external collaborators, and organize access using security groups.

### Tasks Completed

#### 1\. Created Internal User Accounts

I added a new internal user representing an engineer and configured identity metadata such as:

* Display name
* Job title
* Department
* Usage location
Identity metadata is critical for governance, automation, and dynamic group rules.

#### 2\. Invited an External Guest User

I invited an external collaborator to simulate a B2B scenario. The guest appeared in Entra ID and received an email invitation.

#### 3\. Created the "Tremols Tech - Engineering" Security Group

I created a security group to centralize access for lab engineers.

* Assigned myself as owner
* Added internal and external users
* Reviewed static vs dynamic membership
Dynamic membership requires P1/P2 licensing and is extremely useful for MSP environments. For this lab, I used assigned membership instead.



## 🏛 Part 2 - Governance: Management Groups \& RBAC

This section covers subscription organization and role‑based access control (RBAC).

### Scenario

Tremols Tech wants to simplify subscription management and enforce consistent access across all Azure subscriptions. I implemented:

* A management group hierarchy
* Built‑in RBAC role assignments
* A custom RBAC role
* Activity log monitoring

### Tasks Completed

#### 1\. Created a Management Group

I created a management group (tremols-mg-core) to organize subscriptions under a single governance boundary.
Management groups allow:

* Centralized RBAC
* Centralized Azure Policy
* Subscription inheritance
* Directory‑level governance

#### 2\. Assigned a Built-in Role

I assigned the Virtual Machine Contributor role to the Tremols Tech Help Desk group at the management group scope.
This role allows VM management without OS access or network/storage configuration, which is ideal for support teams.

#### 3\. Created a Custom RBAC Role

I cloned the Support Request Contributor role and removed unnecessary permissions to enforce least privilege.
Custom role included:

* Actions for support ticket creation
* NotActions to block provider registration
* Assignable scope limited to the management group

#### 4\. Monitored Role Assignments

I used the Activity Log to confirm role creation and assignment events, which is essential for auditing and compliance.



## 🛡 Part 3 - Governance Enforcement: Azure Policy, Tagging \& Locks

This section enforces governance using Azure Policy, tagging, and resource locks.

### Scenario

During an audit, Tremols Tech discovered resources missing ownership, project, and cost center metadata. To fix this, I implemented:

* Resource tagging
* Tag enforcement \& tag inheritance via Azure Policy
* Resource locks to prevent accidental deletion

### Tasks Completed

#### 1\. Applied Tags to a Resource Group

I created a new resource group (tremols-rg-governance) and applied a CostCenter: 000 tag.
Tags help with:

* Cost management
* Ownership tracking
* Automation
* Reporting

#### 2\. Enforced Tagging with Azure Policy

I assigned a built‑in policy requiring the CostCenter tag on all resources in the resource group.
Attempting to create a storage account without the tag resulted in a policy violation, confirming enforcement.

#### 3\. Applied Tag Inheritance via Azure Policy

I replaced the enforcement policy with a Modify policy that automatically applies the CostCenter tag to child resources.
This required:

* A remediation task
* A managed identity
Creating a new storage account showed the tag automatically applied.

#### 4\. Configured Resource Locks

* I applied a Delete lock to the governance resource group.
* Attempting to delete the group resulted in a lock violation, confirming protection.
* Resource locks override RBAC and prevent accidental deletion or modification.



## 📝 Notes \& Observations

* Management groups are essential for MSP‑style subscription organization.
* RBAC roles should always be assigned to groups, not individuals.
* Custom roles help enforce least privilege.
* Azure Policy is pre‑deployment governance; RBAC and locks are post‑deployment.
* Tagging is critical for cost management and operational clarity.
* Remediation tasks bring existing resources into compliance.
* Locks override user permissions — even owners cannot delete locked resources.



## 🎯 Why This Lab Matters

Identity and governance are the backbone of Azure.
This lab establishes Tremols Tech’s operational foundation:

* Who can access what
* How subscriptions are organized
* How resources are governed
* How metadata is enforced
* How accidental deletion is prevented
Everything else (compute, networking, storage, analytics) depends on this layer being clean and well‑structured.



## 🧹 Cleanup

To remove lab resources:
Portal

* Delete the resource group
* Delete the management group
* Remove policy assignments

### PowerShell

###### Remove-AzResourceGroup -Name tremols-rg-governance

###### Remove-AzManagementGroup -GroupName tremols-mg-core

### CLI

###### az group delete --name tremols-rg-governance

###### az account management-group delete --name tremols-mg-core



## 📈 Next Lab

➡️ [Lab 02 – Compute \& Virtual Machines](https://github.com/JTremols-Cloud/Azure-AZ104-Labs/tree/5f50596f1b5aeac715145ba4ca38617f6cf16911/Lab02-Compute-Virtual-Machines)

