## Azure
#### What is Azure?
**Answer:**
Azure is Microsoft's cloud computing platform, providing a wide range of services, including computing power, storage, and networking, to help organizations build, deploy, and manage applications through Microsoft's global data centers.
#### What are some key services provided by Azure?
**Answer:**
Key services include Azure Virtual Machines, Azure App Services, Azure Storage, Azure SQL Database, Azure Kubernetes Service (AKS), Azure Functions, and Azure Logic Apps.
#### What are Azure Resource Groups?
**Answer:**
Azure Resource Groups are containers that hold related resources for an Azure solution. Resources within a resource group share the same lifecycle and can be managed collectively.
#### What is the Azure Resource Manager (ARM)?
**Answer:**
Azure Resource Manager is the deployment and management service for Azure. It provides a management layer that allows you to create, update, and delete resources in your Azure account.
#### Explain the concept of Azure regions and availability zones
**Answer:**
Azure regions are geographical areas containing multiple data centers. Availability zones are physically separate locations within an Azure region, providing high availability and resilience by allowing replication of resources across zones.
#### What is Azure Virtual Machine (VM)?
**Answer:**
Azure Virtual Machines are on-demand, scalable computing resources that provide virtualized hardware to run applications, just like a physical computer.
#### What are Azure App Services?
**Answer:**
Azure App Services are a fully managed platform for building, deploying, and scaling web apps, mobile app backends, and RESTful APIs.
#### What is Azure Functions?
**Answer:**
Azure Functions is a serverless compute service that allows you to run event-driven code without having to explicitly provision or manage infrastructure.
#### What is Azure Kubernetes Service (AKS)?
**Answer:**
Azure Kubernetes Service is a managed Kubernetes service that simplifies the deployment, management, and operations of Kubernetes clusters in Azure.
#### What are Azure Logic Apps?
**Answer:**
Azure Logic Apps is a cloud service that automates workflows and integrates applications, data, and services across enterprises or organizations.
#### What are the different types of storage services available in Azure?
**Answer:**
The main types of storage services in Azure are Blob Storage, Table Storage, Queue Storage, and File Storage.
#### Explain Azure Blob Storage.
**Answer:**
Azure Blob Storage is a service for storing large amounts of unstructured data, such as text or binary data. It is ideal for serving images or documents directly to a browser, storing files for distributed access, and streaming video and audio.
#### What is Azure Table Storage?
**Answer:**
Azure Table Storage is a NoSQL key-value store for rapid development using massive semi-structured datasets. It is ideal for storing structured, non-relational data.
#### What is Azure Queue Storage?
**Answer:**
Azure Queue Storage is a service for storing large numbers of messages that can be accessed from anywhere via authenticated calls using HTTP or HTTPS. It is used for decoupling components in cloud applications.
#### What is Azure File Storage?
**Answer:**
Azure File Storage provides fully managed file shares in the cloud that are accessible via the industry-standard SMB protocol. It is ideal for shared storage for applications using the standard file system APIs.
#### What are Azure Managed Disks?
**Answer:**
Azure Managed Disks are block-level storage volumes managed by Azure and used with Azure Virtual Machines. They offer high availability and durability, simplifying the creation and management of disks.
#### What is a Virtual Network (VNet) in Azure?
**Answer:**
A Virtual Network (VNet) is the fundamental building block for private networks in Azure. It allows many types of Azure resources, such as Azure VMs, to communicate securely with each other, the internet, and on-premises networks.
#### What is a Network Security Group (NSG)?
**Answer:**
A Network Security Group (NSG) contains security rules that allow or deny inbound and outbound network traffic to and from Azure resources. NSGs can be associated with subnets or individual network interfaces.
#### What is Azure Load Balancer?
**Answer:**
Azure Load Balancer distributes incoming network traffic across multiple VMs, providing high availability and reliability by spreading the load.
#### What is Azure Application Gateway?
**Answer:**
Azure Application Gateway is a web traffic load balancer that enables you to manage traffic to your web applications. It includes features such as SSL termination, URL-based routing, and Web Application Firewall (WAF).
#### What is Azure VPN Gateway?
**Answer:**
Azure VPN Gateway is used to send encrypted traffic between an Azure virtual network and an on-premises location over the public internet. It provides a secure connection to your Azure VNet.
#### Explain the concept of Azure Traffic Manager.
**Answer:**
Azure Traffic Manager is a DNS-based traffic load balancer that distributes traffic optimally to services across global Azure regions, improving availability and responsiveness.
#### What is Azure Active Directory (Azure AD)?
**Answer:**
Azure Active Directory (Azure AD) is a cloud-based identity and access management service that helps employees sign in and access resources in external resources such as Microsoft 365, the Azure portal, and other SaaS applications.
#### What is Multi-Factor Authentication (MFA) in Azure?
**Answer:**
Multi-Factor Authentication (MFA) is an additional security layer for user verification. It requires users to provide more than one form of identification, such as a password and a verification code sent to their phone.
#### What is Role-Based Access Control (RBAC) in Azure
**Answer:**
Role-Based Access Control (RBAC) in Azure helps manage who has access to Azure resources, what they can do with those resources, and what areas they have access to. It provides fine-grained access management for Azure resources.
#### What is Azure Security Center?
**Answer:**
Azure Security Center is a unified infrastructure security management system that strengthens the security posture of your data centers and provides advanced threat protection across your hybrid workloads in the cloud and on-premises.
#### What is Elastic Search?
**Answer:**
“Elasticsearch is a distributed, open-source search and analytics engine built on top of Apache Lucene. It stores data as JSON documents and uses inverted indexes to provide near real-time full-text search, filtering, and analytics at scale. It’s widely used for application search, log analytics, monitoring, and real-time dashboards, often as part of the ELK Stack.”
-   Elasticsearch is an open-source search and analytics engine built on top of Apache Lucene.
-   It is part of the ELK Stack (Elasticsearch, Logstash, Kibana).
-   It is designed for full-text search, structured/unstructured data search, real-time analytics, and log monitoring.
#### Explain azure key vault and how to use/integrate in .net core application?
**Answer:**
-   **Azure Key Vault** is a cloud service for **secrets management**.
-   It securely stores and manages **secrets, keys, and certificates**.
-   Typical use cases:
    -   Store **connection strings, API keys, passwords** (instead of hardcoding in config).
    -   Manage **encryption keys** (for data-at-rest encryption).
    -   Manage and auto-rotate **TLS/SSL certificates**.</br>

**Why use it?**
-   **Centralized secrets management** → no secrets in code or configs.
-   **Secure access** via Azure AD authentication and RBAC.
-   **Audit logging** → track who accessed what and when.
-   **Automated rotation** → rotate secrets/certs without code changes.
-   **Compliance** → meets enterprise security standards.</br>

**🛠️ How to Integrate Azure Key Vault with .NET Core App**
In .NET Core, you integrate by adding Key Vault to your app configuration (using `AddAzureKeyVault`) with `DefaultAzureCredential`. From then, you can access secrets as normal config values, keeping your app secure and compliant.
