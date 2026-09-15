# Lab 01 – Identity, Governance & Compliance

This lab marks the start of my AZ‑104 journey. It focuses on Microsoft Entra ID, Azure’s identity and access management platform, and covers the core tasks every cloud administrator must master before touching compute, networking, or storage.

The goal of this lab was to build a clean identity foundation for Tremols Tech’s pre‑production Azure environment. I created internal users, onboarded external collaborators, and organized access using security groups. I also explored how governance features like dynamic membership support scalable identity management.


# Scenario
- Tremols Tech is preparing an Azure environment for upcoming engineering work. Before any virtual machines or services can be deployed, the identity layer must be established. Engineers need accounts, groups must be defined, and access must be structured in a way that scales.
To reduce administrative overhead, group membership should update automatically based on user attributes such as job title. This is where dynamic groups come into play.


# What I Completed
- Created internal user accounts with job titles, departments, and usage locations to simulate real organizational identity data.
- Invited an external guest user and validated the B2B onboarding flow.
- Built a security group for IT Lab Administrators to centralize access.
- Assigned ownership of the group to myself for administrative control.
- Added internal and guest users to the group to complete the access model.
- Reviewed static vs dynamic membership, including where dynamic rules fit into enterprise identity governance.

# Key Observations
- Tenant switching in Entra ID is smoother than expected—useful for MSP scenarios where multiple tenants are common.
- Dynamic groups require P1/P2 licensing, which is important when designing identity governance for clients.
- Guest invites are fast and reliable, making external collaboration easy to manage.
- The Properties tab for users contains extensive metadata fields—helpful for automation, governance, and conditional access policies.

#Why This Lab Matters
- Identity is the backbone of Azure. Every resource, permission, and policy ties back to Entra ID. A clean identity structure prevents misconfigurations, reduces security risk, and sets the stage for scalable governance.
- This lab establishes the foundation for everything that follows in AZ‑104—RBAC, policy, networking, compute, storage, and monitoring.

Screenshots
(Add your screenshots here once you upload them.)

Next Steps
Manage identities and governance

Configure virtual networks


