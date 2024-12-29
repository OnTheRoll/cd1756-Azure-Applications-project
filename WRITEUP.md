# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

# CMS App - VM vs App Service Analysis

| **Analysis Criteria**       | **Virtual Machine (VM)**                                         | **App Service**                                                    |
|-----------------------------|------------------------------------------------------------------|-------------------------------------------------------------------|
| **1. Cost**                  | - Higher upfront cost for VM provisioning                       | - Predictable monthly pricing based on selected tier             |
|                             | - Costs based on VM size, storage, and bandwidth               | - Costs depend on the selected plan (Free, Basic, Standard, Premium) |
|                             | - Additional costs for high availability and disaster recovery | - Lower initial costs for smaller apps                          |
|                             | - Scaling incurs manual setup or requires load balancers       | - Scalable without needing manual VM management                  |
|                             | - Potential cost increases for multi-region deployment        | - Price increases with higher performance tiers and auto-scaling |
| **2. Scalability**          | - Vertical scaling (increase CPU/RAM) limited by VM size       | - Vertical scaling (changing tiers) is straightforward and fast  |
|                             | - Horizontal scaling (manual setup for multiple VMs)          | - Horizontal scaling (auto-scaling with minimal configuration)  |
|                             | - Manual configuration needed for load balancing               | - Auto-scaling based on demand without manual intervention        |
|                             | - Complex scaling with load balancing in large-scale setups    | - Scales easily with little overhead                             |
|                             | - Cost may increase rapidly with more VMs                       | - More cost-effective for variable or moderate traffic apps      |
| **3. Availability**         | - HA requires manual configuration (Availability Sets, Zones) | - Built-in high availability with deployment slots              |
|                             | - Failover setup and monitoring needed                         | - Geo-replication and disaster recovery built-in                |
|                             | - More downtime risk if not configured correctly                | - Minimal downtime due to automatic patching and management     |
|                             | - Requires setup for disaster recovery (e.g., Azure Site Recovery) | - High availability with no manual configuration for failover   |
| **4. Workflow**             | - More complex deployment process (CI/CD, manual setup)       | - Easier deployment with integrated CI/CD support               |
|                             | - Requires custom monitoring and management tools             | - Built-in monitoring and diagnostics                           |
|                             | - More flexible environment, full control over infrastructure | - Less flexibility, but faster and easier updates                |
|                             | - Requires updates and patching to be managed manually        | - Azure manages updates, reducing operational overhead          |
|                             | - Full control over OS and software stack                      | - Simplified environment with predefined OS and stack           |


# Appropriate Solution for CMS App Deployment

Given that the CMS app is small, with minimal hardware requirements and not many users, the **App Service** solution is the most appropriate choice for deployment.

## Justification:

- **Simplicity and Cost-Effectiveness**:  
  Since the CMS app has low hardware demands, the App Service offers a more cost-effective and simplified solution compared to VMs. App Service plans provide built-in scaling options, and the pricing is predictable based on the selected tier, which is ideal for a small app with low resource requirements.

- **Managed Infrastructure**:  
  App Service abstracts away the complexities of infrastructure management. This means you don't need to worry about OS patches, scaling, or load balancing, all of which are automatically handled by Azure. This is a huge benefit for small apps, as it reduces operational overhead and allows developers to focus on the app itself rather than managing servers.

- **Built-in Features**:  
  App Service also includes features like automated backups, integrated monitoring, and seamless deployment pipelines, making it easier to manage and update the app without requiring additional configuration or third-party tools.

For a small app with minimal requirements, the **App Service** provides a faster, more efficient, and lower-maintenance solution compared to the Virtual Machine approach.

### Assess app changes that would change your decision.

## Assessing App Changes That Could Alter the Deployment Decision

There are certain changes in the app's needs that could impact the decision to use **App Service** vs. **Virtual Machine (VM)**. Below are some considerations that might alter the deployment decision depending on the direction the application evolves.

### 1. **Increase in Application Complexity or Resource Demands**

If the CMS app grows in complexity or its resource demands increase (e.g., processing larger media files, handling more concurrent users, or running more computationally intensive features), **App Service** might not be sufficient. For example:
   - If the app needs specific hardware configurations (e.g., specialized CPU/GPU requirements, specific libraries or OS-level customizations), App Service may not provide enough flexibility.
   - **App Service limitations** on resource allocation might force the app to exceed the limits of the chosen tier, leading to potential performance bottlenecks or high costs due to auto-scaling at large traffic spikes.

   **How this could change the decision**:  
   If the app's resource demands grow beyond what App Service can handle efficiently or cost-effectively, **VMs** might be a better choice. VMs provide full control over hardware resources, offering greater flexibility for performance optimization.

### 2. **Need for Custom Infrastructure or More Control**

If the CMS app requires fine-grained control over its environment (e.g., installing specific software, libraries, or running legacy systems), **App Service** may not offer the level of control needed. App Service operates within a predefined environment, meaning you cannot customize the underlying OS, install custom software packages, or tweak low-level configurations.

   **How this could change the decision**:  
   If the CMS app requires a high degree of control over the server environment, the ability to install custom software, or full control over networking and security configurations, switching to a **VM** would provide the necessary flexibility. With VMs, the app can run custom operating systems, and you can configure the server and environment to meet any specific requirements.

### 3. **High Availability and Failover Needs**

If the CMS app scales to a point where **high availability** and **disaster recovery** become critical (e.g., mission-critical, 24/7 operation with zero downtime), more advanced configurations may be needed. While **App Service** offers built-in scaling and some redundancy, if the app needs complex failover strategies, multi-region deployments, or greater control over load balancing and traffic management, these requirements may not be met by App Service’s simplified platform.

   **How this could change the decision**:  
   If the app requires highly sophisticated failover configurations, custom load balancers, or geographical distribution across multiple regions, deploying on a **VM** would give more control over availability and disaster recovery solutions. VMs can be configured in multiple regions or availability zones, and you have more options for network configurations and redundancy.

### 4. **Regulatory and Security Requirements**

If the app must meet specific regulatory or compliance standards (e.g., HIPAA, GDPR, or PCI-DSS), the **security and control** offered by a VM might become a more attractive option. While App Service includes security features like SSL support, managed identities, and built-in encryption, certain compliance standards may require specific configurations or controls that only VMs can provide.

   **How this could change the decision**:  
   If the CMS app needs to meet strict regulatory or security standards requiring a highly customized infrastructure or full control over data storage and access management, **VMs** would be more suitable. VMs allow for more granular control over security configurations, network isolation, and compliance auditing.