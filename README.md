# Web-App-DevOps-Project

Welcome to the Web App DevOps Project repo! This application allows you to efficiently manage and track orders for a potential business. It provides an intuitive user interface for viewing existing orders and adding new ones. The technolgies used to deploy this application include the follwoing:

- Azure Cloud
- Azure devOps
- Python 3.8
- Flask
- Docker
- Kubernetes
- Terraform
- Visual studio code
  

## Table of Contents

- [Features](#features)
- [Getting Started](#getting-started)
- [Technology Stack](#technology-stack)
- [Contributors](#contributors)
- [License](#license)

## Features

- **Order List:** View a comprehensive list of orders including details like date UUID, user ID, card number, store code, product code, product quantity, order date, and shipping date.
  
![Screenshot 2023-08-31 at 15 48 48](https://github.com/maya-a-iuga/Web-App-DevOps-Project/assets/104773240/3a3bae88-9224-4755-bf62-567beb7bf692)

- **Pagination:** Easily navigate through multiple pages of orders using the built-in pagination feature.
  
![Screenshot 2023-08-31 at 15 49 08](https://github.com/maya-a-iuga/Web-App-DevOps-Project/assets/104773240/d92a045d-b568-4695-b2b9-986874b4ed5a)

- **Add New Order:** Fill out a user-friendly form to add new orders to the system with necessary information.
  
![Screenshot 2023-08-31 at 15 49 26](https://github.com/maya-a-iuga/Web-App-DevOps-Project/assets/104773240/83236d79-6212-4fc3-afa3-3cee88354b1a)

- **Data Validation:** Ensure data accuracy and completeness with required fields, date restrictions, and card number validation.

## Getting Started

### Prerequisites

For the application to succesfully run, you need to install the following packages:

- flask (version 2.2.2)
- pyodbc (version 4.0.39)
- SQLAlchemy (version 2.0.21)
- werkzeug (version 2.2.3)

### Usage

To run the application, you simply need to run the `app.py` script in this repository. Once the application starts you should be able to access it locally at `http://127.0.0.1:5000`. Here you will be meet with the following two pages:

1. **Order List Page:** Navigate to the "Order List" page to view all existing orders. Use the pagination controls to navigate between pages.

2. **Add New Order Page:** Click on the "Add New Order" tab to access the order form. Complete all required fields and ensure that your entries meet the specified criteria.

## Technology Stack

- **Backend:** Flask is used to build the backend of the application, handling routing, data processing, and interactions with the database.

- **Frontend:** The user interface is designed using HTML, CSS, and JavaScript to ensure a smooth and intuitive user experience.

- **Database:** The application employs an Azure SQL Database as its database system to store order-related data.

### Infrastructure Architecture


![](https://github.com/chyjuls/Web-App-DevOps-Project/blob/fde7a76d4d1968ea171987e49ecc5495a8941495/DevOps%20Pipeline%20Architecture.png)



## Docker:

Details are within the dockerfile, docker image is built using   

``` Docker build ```
   

## Terraform 

**Overview**  

Terraform by HashiCorp is an Infrastructure as Code (IaC) tool used for building, changing, and versioning infrastructure safely and efficiently. It supports various cloud providers like Azure, AWS, and Google Cloud. Terraform uses declarative configuration files that describe the desired state of your infrastructure.

**Key Concepts**  

Infrastructure as Code (IaC): Manage infrastructure using configuration files rather than through manual processes.

Providers: Plugins that interact with APIs of cloud providers, services, or other tools (e.g., Azure, AWS).
Resources: Components of your infrastructure such as virtual networks, compute instances, or higher-level components like DNS records.
Modules: Reusable, encapsulated Terraform configurations for creating sets of resources that are used together.
State: Terraform records information about what infrastructure is created in a state file, allowing for consistent management of resources.

 **Modules**
 
 - networking-module:provisions infrastructure for an Azure Kubernetes Service (AKS) cluster, typically contains Terraform configuration files that define and manage the necessary networking resources within Azure. These resources are essential for the AKS cluster to function correctly and securely within the Azure cloud environment. The resources include azure Vnet, subnets, route table etc.
   
 - aks-cluster-module: defines and manages an Azure Kubernetes Service (AKS) cluster. This module encapsulates all the configurations needed to set up the AKS cluster in a way that aligns with best practices, desired customisations, and the specific requirements of the application or environment. It contains the ask-cluster resource, node pools, service principal and managed identies, etc.
 

### Inputs and Outputs

**Input Variables**  

aks_cluster_name: Name of the AKS cluster.
cluster_location: Azure region where the AKS cluster will be deployed.
dns_prefix: DNS prefix for the AKS cluster.
kubernetes_version: Version of Kubernetes for the AKS cluster.
service_principal_client_id: Client ID for the service principal.
service_principal_secret: Client Secret for the service principal.
Additional networking-related variables.  

**Output Variables**  

aks_cluster_name: The name of the provisioned AKS cluster.
aks_cluster_id: The ID of the provisioned AKS cluster.
aks_kubeconfig: Kubernetes configuration file for the AKS cluster.



Terraform Workflow

Initialize:

``` Terraform init ```

This command sets up Terraform's working directory, downloads providers, and prepares the backend for state storage.
Writing Configuration:

Define your infrastructure in configuration files (.tf).
Resources, variables, outputs, and provider configurations are declared here.

Planning:
Execute terraform plan.
``` Terrsform plan ```
Terraform reads configuration files and creates an execution plan, detailing what actions it will perform to reach the desired state.
Applying:

```terraform apply```

Terraform will execute the plan to create, update, or delete resources as per the configuration.

To remove all resources managed by Terraform, use  ``` Terraform destroy```.

**Best Practices**  

Version Control: Keep your Terraform configurations in a version control system (like Git).
Modularization: Use modules to organize and reuse code.
Secrets Management: Avoid hardcoding sensitive information. Use environment variables or secret management tools.
Review Plans: Carefully review execution plans before applying changes.


# Infrastructure Provisioning with Terraform

**Overview**  

This project utilizes Terraform for the automated provisioning of infrastructure in Azure, specifically focusing on setting up an Azure Kubernetes Service (AKS) cluster and associated networking resources.

**Infrastructure Components**  

Azure Resource Group: Serves as a logical container for grouping related resources.
Virtual Network (VNet): Provides networking for AKS, including control plane and worker node subnets.
Subnets: Two subnets, one for the control plane and one for the worker nodes.
Network Security Group (NSG): Manages network security rules for secure access to the AKS cluster.
AKS Cluster: The central Kubernetes cluster managed by Azure.
Setup and Configuration
Terraform is used to define and manage the above resources.
The configuration is divided into modules for better organization and reusability.
Variables are used to ensure configurability and flexibility of the setup.
Troubleshooting Steps Undertaken
Throughout the setup, several issues were encountered and resolved:

Service Principal Authentication: Initially faced issues with Azure Service Principal permissions. Resolved by assigning the appropriate roles to the Service Principal.

Resource Provider Registration: Encountered a MissingSubscriptionRegistration error. This was fixed by manually registering the Microsoft.ContainerService provider with the Azure subscription.

Permission Issues for Resource Group Creation: Faced AuthorizationFailed errors when attempting to create resource groups. This was resolved by ensuring the Service Principal had sufficient permissions.

Namespace Registration: Addressed errors related to the subscription not being registered to use certain Azure services (namespaces).

Conclusion
The project demonstrates the power of Infrastructure as Code (IaC) using Terraform, showcasing how complex infrastructure can be provisioned, managed, and troubleshooted systematically.

# Kubernetes Deployment   

### Deployment and Service Manifests

This application is deployed on Azure Kubernetes Service (AKS) using Kubernetes manifests. These manifests define the desired state of our application's deployment and service in the cluster.

### Key Components:
Deployment Manifest: The deployment manifest (deployment.yaml) specifies our application's deployment configuration. It includes the following key settings:

**Pod Template**: Defines the container image to use (chyjuls/web-delivery:v1) and necessary environment variables.
**Replicas**: Sets the number of pod replicas for high availability.
**Resource Requests/Limits**: Configures CPU and memory resources for each pod.
**Readiness and Liveness Probes**: Ensures that the application is running correctly and is ready to receive traffic.
**Service Manifest**: The service manifest (service.yaml) defines how the application's pods are exposed within the cluster. It includes:
**Type**: Determines how the service is exposed. For internal use, we use ClusterIP; for external access, LoadBalancer can be used.
**Port Mapping**: Maps the port from the pod to the service.

### Deployment Strategy  

For our application, we've chosen a rolling update deployment strategy. This approach ensures zero downtime during updates, gradually replacing instances of the older version of our application with the new version.

**Benefits**:
Zero Downtime: Ensures that the application remains available to users during deployment.
Rollback Capabilities: Allows for easy rollback to the previous version if issues arise.
Testing and Validation
Post-deployment, we conducted several tests to ensure the application's functionality and reliability:

**Connectivity Test**: Verified that the application's pods are accessible and running as expected using ```sh kubectl get pods```.
**Functionality Test**: Used port forwarding (```kubectl port-forward```) to temporarily access the application and test its core functionalities, including the orders table and Add Order feature.  

### Internal and External Access  

**Internal Access**:
For internal users, the application can be accessed through an internal load balancer or ingress controller within the AKS cluster. This approach allows employees to access the application without exposing it to the public internet.  

We plan to set up an ingress controller that routes internal traffic to the application based on URL paths.  

**External Access**:

To make the application accessible to external users, we can expose it through an external load balancer or ingress controller with proper security measures in place.  

**Key considerations for external access include**:
- TLS/SSL Certificates: For secure HTTPS access.
- Authentication and Authorization: To control access to the application.
- Monitoring and Logging: To track usage and potential security incidents.



# CI/CD Pipeline Setup

## Overview
This project includes a Continuous Integration/Continuous Deployment (CI/CD) pipeline, which automates the process of testing, building, and deploying the application. The pipeline is defined in the azure-pipeline.yaml file and utilizes Azure DevOps for execution.

### azure-pipeline.yaml**  

The azure-pipeline.yaml file defines the pipeline's stages, jobs, and steps. It is structured as follows:

**Trigger**: Specifies the branch(es) that will trigger the pipeline.
**Variables**: Defines the variables used across the pipeline.
**Stages**: Organizes the pipeline into distinct stages such as Build, Test, and Deploy.
**Build Stage**: Compiles the code, runs tests, and builds the Docker image. The image is then pushed to a Docker registry.  
**Deploy Stage**: Handles the deployment of the built image to the Kubernetes cluster.  

### Kubernetes Manifest File  

The Kubernetes manifest file, located at [path-to-manifest-file], is crucial for the deployment process. It defines the desired state of the application in the Kubernetes cluster. Key components include:

**Deployment**: Specifies the container image to use, the number of replicas, and configuration like environment variables and resource limits.
**Service**: Defines how the application is exposed within the Kubernetes cluster or to the outside world, like LoadBalancer or NodePort services.  

### CI/CD Pipeline Flow  

**Code Commit**: A commit to the specified branch triggers the pipeline.
**Build**: The application is built, and a Docker image is created.
**Test**: Automated tests are run to ensure code reliability.
**Docker Push**: The Docker image is pushed to the registry.
**Deployment**: The application is deployed to the AKS cluster using the Kubernetes manifest file.
**Post-Deployment**: The pipeline performs any post-deployment steps like health checks or notifications.  

### Conclusion
The CI/CD pipeline ensures that every code change is automatically tested and deployed, maintaining the reliability and stability of the application. This automation streamlines the development process, reduces manual errors, and ensures quicker delivery of features and fixes.


    
# Monitoring Strategy for AKS Cluster    


## Metrics Explorer Charts
The AKS cluster monitoring utilizes Azure Monitor's Metrics Explorer to visualize key performance indicators. Below are the specific charts utilized, their significance, and interpretation guidelines:

1. Average Node CPU Usage
   
**Significance**: This chart tracks the CPU usage across all nodes, providing insights into the computational load and identifying potential bottlenecks.
**Metrics Tracked**: CPU utilization percentage.
Interpretation: Values nearing 100% indicate high CPU load, suggesting the need for scaling or optimization.

2. Average Node Memory Usage
   
**Significance**: Monitors memory consumption, crucial for ensuring applications have sufficient resources and for detecting memory leaks.
**Metrics Tracked**: Memory utilization percentage.
Interpretation: High memory usage close to the node capacity may require scaling or investigating potential memory leaks.

3. Pod Count by Phase
   
**Significance**: Offers a snapshot of pod distribution by their lifecycle phase, useful for understanding cluster workload and deployment health.
**Metrics Tracked**: Count of pods in phases like Running, Pending, Failed, etc.
Interpretation: An unusual increase in Pending or Failed pods may indicate issues with scheduling or application errors.

## Log Analytics  

Azure Log Analytics is used  to parse and analyze logs from the AKS cluster. Key logs include:

1. Node and Pod Logs
**Content**: Include metrics on operations, performance, and errors at both the node and pod levels.
**Relevance**: Helps in diagnosing system-level and application-level issues.

2. Container Logs
**Content**: Capture stdout and stderr from containers, including application logs.
**Relevance**: Critical for troubleshooting application-specific issues.


## Alarm Configurations

1. CPU Usage Alarm
**Condition**: Triggered when CPU usage exceeds 80% for over 5 minutes.
**Threshold**: >80% CPU utilization.
**Response Strategy**: Investigate running pods and services for optimization or scale up the cluster.

2. Memory Usage Alarm
**Condition**: Fires when memory usage surpasses 80% for a continuous 5-minute window.
**Threshold**: >80% memory utilization.
**Response Strategy**: Check for memory-intensive applications, consider scaling or optimizing pod configurations.


# AKS Integration with Azure Key Vault

This section outlines the integration process between Azure Kubernetes Service (AKS) and Azure Key Vault, aimed at enhancing the security and management of sensitive application configurations such as secrets, keys, and certificates.

## Azure Key Vault Setup and Permissions

Azure Key Vault is utilised to securely store and manage sensitive information such as passwords, database connection strings, and API keys.

### Setup

**Key Vault Creation**: A Key Vault instance was provisioned in Azure, ensuring geographic proximity to the AKS cluster for optimized performance.
**Secrets Storage**: Critical application secrets, including database connection strings and external API keys, were stored in the Key Vault.  


### Assigned Permissions  
To ensure secure and efficient management, the Key Vault Administrator role was assigned to responsible personnel, enabling them to manage vault access policies and secrets. A Managed Identity for the AKS cluster was created and assigned the Key Vault Secrets User role, granting it permission to read secrets as needed by the application.

### Application Secrets in Key Vault

Each secret stored within the Key Vault is critical for application functionality:

**Database Connection String**: Enables secure database access without hardcoding sensitive details in the application code.  

**API Keys**: Used for authentication when integrating with external services, ensuring that each service can be securely accessed.  

### AKS Integration with Key Vault 

Integration between AKS and Key Vault was achieved through the following steps:

**Managed Identity for AKS**
A Managed Identity was created for the AKS cluster, providing an Azure AD identity that the cluster uses to interact with Azure services.  

The Managed Identity was granted the Key Vault Secrets User role on the Key Vault, ensuring it has read access to the necessary secrets.

**Application Code Modifications**   
The application code was modified to leverage the Managed Identity for secure secret retrieval:
**SDK Integration**: The Azure SDK was integrated into the application, allowing it to authenticate using the Managed Identity.
**Secret Retrieval**: Code changes were made to fetch database connection strings and other configurations directly from Key Vault at runtime.
Architecture Overview






## Contributors 

- [Maya Iuga]([https://github.com/yourusername](https://github.com/maya-a-iuga))
- C.Ugorji

## License

This project is licensed under the MIT License. For more details, refer to the [LICENSE](LICENSE) file.
