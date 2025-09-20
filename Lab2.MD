# Iaas application deployment in the cloud workflow: 

# IaaS Application Deployment in the Cloud Workflow

### Mermaid Code (for lab requirement)
```mermaid
flowchart TD
    A[INTERNET / User] --> B["IAAS CLOUD ENVIRONMENT\n(AWS / AZURE / GCP)"]
    B --> C["Load Balancer\nPublic IP"]
    C --> D["VM 1: React UI Frontend\nReact App"]
    D --> E["VM 2: Flask Web Server\nFlask App"]
    E --> F["VM 3: PostgreSQL Database\nPostgres Server"]
    F --> G["Persistent Disk Storage"]

    %% Request path
    C -- "UI Access / API Request" --> D
    D -- "API Request (internal)" --> E
    E -- "DB Query / Update (internal)" --> F
    F -- "Data Read / Write" --> G

    %% Response path
    G -- "Data Response" --> F
    F -- "Query Result" --> E
    E -- "API Response" --> D
    D -- "UI Response" --> C
    C --> A

    %% Security group
    subgraph Security["Firewall / Security Group"]
        D
        E
        F
    end

![alt text](iaas.png)

## Description

The IaaS architectural design will be a complete self-managed infrastructure over the cloud (AWS, Azure, or GCP). In this setup:

- The internet receives user requests that are sent to the load balancer which gives it a public IP and allocates traffic on the virtual machines.

- The React UI application is deployed in the frontend VM and all user interface requests are processed by it.

- Frontend API requests are sent to a Flask web server VM, which handles a logic and application layer.

- A PostgreSQL database VM store and retrieve the data after communication with the backend.

- Persistent disk storage supports all database operations and makes the data durable.

- The compute resources (frontend, backend, and database VMs) are safeguarded by a firewall/security group that determines outbound and inbound traffic.

- Request and response flows are depicted using labeled arrows and they indicate the flow of user queries in the system and the flow of results back.

## Paas application deployment in the cloud workflow: 
 


# mermaid code for paas will generate flowchart  

flowchart TD
    %% User
    A([User / Internet]):::user --> B["CDN\n(CloudFront / Azure CDN / Cloud CDN)"]:::cdn

    %% Frontend
    B --> C["React UI (Frontend)\nHosted on Managed Object Storage + CDN\n(Cloud Storage)"]:::frontend

    %% API Gateway
    C --> D{{"API Gateway\n(Managed Routing & Security)"}}:::gateway

    %% Backend
    D --> E["Flask API\nManaged App Service\n(App Engine / Azure App Service )  "]:::backend

    %% Secrets Manager
    E --> H[/"Secrets Manager\n(DB Credentials, API Keys)"/]:::security

    %% Database
    E --> F[("Managed PostgreSQL DB\n(RDS / Azure Database / Cloud SQL)")]:::database

    %% Object Storage
    E --> G[("Managed Object Storage\n(S3 / Blob / Cloud Storage)\n(Uploads & Assets)")]:::storage

    %% Monitoring / Logging
    E --> I[["Monitoring & Logging\n(CloudWatch / Azure Monitor ) "]]:::monitoring
    F --> I
    G --> I

    %% Response flow
    F -- "Query Result" --> E
    G -- "File/Data Response" --> E
    E -- "API Response" --> D
    D --> C
    C --> B
    B --> A

    %% Styling
    classDef user fill:#f7e7a0,stroke:#444,stroke-width:2px,color:#000
    classDef cdn fill:#c9eaff,stroke:#0366d6,stroke-width:1.5px,color:#000
    classDef frontend fill:#b2f0b2,stroke:#2d7a2d,stroke-width:1.5px,color:#000
    classDef gateway fill:#ffe0b3,stroke:#e67e22,stroke-width:1.5px,color:#000
    classDef backend fill:#ffd699,stroke:#cc7000,stroke-width:1.5px,color:#000
    classDef database fill:#f5c6cb,stroke:#b02a37,stroke-width:1.5px,color:#000
    classDef storage fill:#d5d8dc,stroke:#5d6d7e,stroke-width:1.5px,color:#000
    classDef security fill:#d4e6f1,stroke:#2471a3,stroke-width:1.5px,color:#000
    classDef monitoring fill:#e8daef,stroke:#76448a,stroke-width:1.5px,color:#000

![alt text](paas.png)
## Description

The PaaS model illustrates how it is easier to deploy applications with the help of fully managed cloud services. In this setup:

- The user requests are sent via the internet and passed on through a Content Delivery Network (CDN), which enhances the performance and global availability.

- The React UI is hosted on the object storage which is managed and served through the CDN so as to eliminate the management of servers serving the static content.

- The requests pass through API Gateway that ensures secure routing, validation of the requests, and controlled access to services at the backside.

- Flask API is deployed on a managed application service (e.g., App Engine or Azure App Service), which does not require any virtual machines to be deployed or maintained.


- The application is linked to a PostgreSQL database service (RDS, Azure Database or Cloud SQL) which is managed and structured to store data.It also builds file uploads and assets on managed object storage (S3, Blob, or Cloud Storage).



- Monitoring and logging services ( CloudWatch, Azure Monitor, etc.) are used to gather the operational data and assist in maintaining the stability of the system.

- The arrows reflect request-response cycle, and how the actions of users go through the frontend, backend, and data layers and the outcomes are sent back to the user.

