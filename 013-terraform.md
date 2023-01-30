### Terraform

HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features.

![](./images/image14.avif)

The core Terraform workflow consists of three stages:

- `Write`: You define resources, which may be across multiple cloud providers and services. For example, you might create a configuration to deploy an application on virtual machines in a Virtual Private Cloud (VPC) network with security groups and a load balancer.
- `Plan`: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration.
- `Apply`: On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. For example, if you update the properties of a VPC and change the number of virtual machines in that VPC, Terraform will recreate the VPC before scaling the virtual machines.

![](./images/image15.avif)

---

#### Use cases

##### Multi-Cloud Deployment

Provisioning infrastructure across multiple clouds increases fault-tolerance, allowing for more graceful recovery from cloud provider outages. However, multi-cloud deployments add complexity because each provider has its own interfaces, tools, and workflows. Terraform lets you use the same workflow to manage multiple providers and handle cross-cloud dependencies. This simplifies management and orchestration for large-scale, multi-cloud infrastructures.

##### Application Infrastructure Deployment, Scaling, and Monitoring Tools

You can use Terraform to efficiently deploy, release, scale, and monitor infrastructure for multi-tier applications. N-tier application architecture lets you scale application components independently and provides a separation of concerns. An application could consist of a pool of web servers that use a database tier, with additional tiers for API servers, caching servers, and routing meshes. Terraform allows you to manage the resources in each tier together, and automatically handles dependencies between tiers. For example, Terraform will deploy a database tier before provisioning the web servers that depend on it.

##### Self-Service Clusters

At a large organization, your centralized operations team may get many repetitive infrastructure requests. You can use Terraform to build a "self-serve" infrastructure model that lets product teams manage their own infrastructure independently. You can create and use Terraform modules that codify the standards for deploying and managing services in your organization, allowing teams to efficiently deploy services in compliance with your organization’s practices. Terraform Cloud can also integrate with ticketing systems like ServiceNow to automatically generate new infrastructure requests.

##### Parallel Environments

You may have staging or QA environments that you use to test new applications before releasing them in production. As the production environment grows larger and more complex, it can be increasingly difficult to maintain an up-to-date environment for each stage of the development process. Terraform lets you rapidly spin up and decommission infrastructure for development, test, QA, and production. Using Terraform to create disposable environments as needed is more cost-efficient than maintaining each one indefinitely.

##### Software Demos

You can use Terraform to create, provision, and bootstrap a demo on various cloud providers. This lets end users easily try the software on their own infrastructure and even enables them to adjust parameters like cluster size to more rigorously test tools at any scale.

##### Kubernetes

Kubernetes is an open-source workload scheduler for containerized applications. Terraform lets you both deploy a Kubernetes cluster and manage its resources (e.g., pods, deployments, services, etc.). You can also use the Kubernetes Operator for Terraform to manage cloud and on-prem infrastructure through a Kubernetes Custom Resource Definition (CRD) and Terraform Cloud.

#### Terraform Registry

The Terraform Registry is a centralized repository that enables users to find, share, and use Terraform modules. A Terraform module is a package of Terraform code that defines the desired state of infrastructure, such as virtual machines, databases, and networking resources. By using modules from the Terraform Registry, users can speed up the development and deployment of their infrastructure, reduce the risk of human error, and benefit from the experience and expertise of other Terraform users.

For example, suppose you want to deploy a web application with a load balancer, a virtual machine, and a database. You can write the Terraform code for these resources from scratch, but it will take time and may be prone to errors. Instead, you can search for a module that implements this infrastructure pattern in the Terraform Registry and download it to your local machine. Then, you can use the module in your Terraform configuration by referencing its source code, and customize it to meet your specific needs by passing variables to the module.

![](./images/image16.png)
