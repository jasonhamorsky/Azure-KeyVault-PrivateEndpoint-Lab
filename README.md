# Azure-KeyVault-PrivateEndpoint-Lab
Azure Key Vault secured with Private Endpoint, RBAC, and public network disabled. Zero trust PaaS
Overview
This project demonstrates how to secure Azure Key Vault using a Private Endpoint and RBAC-based access control.
Because Azure for Students does not support virtual machines, the lab focuses on identity and networking behaviors that still fully validate the private endpoint:
• 	Key Vault creation
• 	RBAC vs Access Policies
• 	Private Endpoint configuration
• 	Firewall behavior
• 	Secret creation
• 	Zero Trust access validation
The goal is to show how Key Vault behaves when public access is disabled and only private network traffic is allowed.
Architecture (ASCII Diagram)
+---------------------------+ |       Azure Portal        | |  Public Client (Blocked)  | +-------------+-------------+ | | Public Traffic (Denied) v +-----------------------------------------+ |           Azure Key Vault               | |  - RBAC Mode                            | |  - Public Access Disabled               | |  - Private Endpoint Required            | +-----------------+-----------------------+ | | Private Link v +-----------------------------------------+ |     Private Endpoint (pep-kv-private)   | |     Subnet: vnet-azure-vm-nsg-bastion2 | |     State: Approved                     | +-----------------------------------------+
What I Built
Key Vault (RBAC Mode)
• 	Created a Key Vault using Azure role-based access control
• 	Assigned myself Key Vault Administrator to enable secret creation
• 	Demonstrated the difference between control-plane roles (Owner/Contributor) and data-plane roles (Secrets User, Secrets Officer, Administrator)
Private Endpoint
• 	Created a private endpoint targeting the "vault" sub-resource
• 	Verified the connection state as Approved
• 	Confirmed the endpoint is mapped to the correct VNet/subnet
Firewall & Network Isolation
• 	Switched between Allow public access (for secret creation) and Disable public access (for Zero Trust isolation)
• 	Observed expected behavior:
• 	When public access is disabled, the Azure Portal cannot read secrets
• 	When public access is enabled, the portal can read secrets
Secret Creation
• 	Created a secret named "testsecret"
• 	Verified versioning and status
• 	Observed how RBAC permissions affect secret creation
Key Learning Points
RBAC vs Access Policies
• 	RBAC mode ignores Access Policies
• 	Control-plane roles do not grant secret-level permissions
• 	A data-plane role is required to manage secrets
Private Endpoint Behavior
• 	The Azure Portal is not a trusted Microsoft service
• 	The portal does not use the private endpoint
• 	When public access is disabled, the portal cannot read or write secrets
• 	This is expected Zero Trust behavior
Azure for Students Constraints
• 	No VMs available
• 	Cannot test private endpoint access from inside the VNet
• 	Lab is still valid by demonstrating:
• 	Private endpoint creation
• 	Firewall enforcement
• 	Portal access failure
• 	Secret creation and versioning
Screenshots to Include
• 	Key Vault Overview
• 	Networking → Private Endpoint (Approved)
• 	Networking → Public Access Disabled
• 	Secret Created (testsecret)
• 	Secret Version screen
• 	Portal access failure message when public access is disabled
Why This Project Matters
This lab demonstrates practical understanding of:
• 	Azure identity and access management
• 	Data-plane vs control-plane permissions
• 	Private endpoint architecture
• 	Zero Trust network boundaries
• 	Key Vault security hardening
• 	Real-world troubleshooting
These are core skills for cloud operations, identity, and security roles.
Conclusion
This project shows how to secure Azure Key Vault using private endpoints and RBAC, even within the limitations of Azure for Students. It highlights the ability to configure secure services, diagnose access issues, and document a clean, professional workflow.
