# **Core Kubernetes Concepts For Azure Kubernetes Service (AKS)**

### **What is Kubernetes:**

- Kubernetes is a rapidly evolving platform that manages container-based applications and their associated networking and storage components.
- Kubernetes focus on the application workloads and not the underlying infrastructure components.
- Kubernetes provides a declarative approach to deployments, backed by a robust set of APIs for management operations.
- We can build and run modern, portable, microservices-based applications using kubernetes to orchestrate and manage the availability of the application components.
- Kubernetes supports both stateless and stateful applications.
- As an open platform, Kubernetes allow you to build your applications with your preferred programming languages, OS, ibraries or messaging bus.
- Existing continuous integration and continuous delivery (CI/CD) tools can integrate with kubernetes to schedule and deploy releases.
- AKS provides a managed Kubernetes service that reduces the complexity of deployment and core management tasks.
- the Azure platform manage the AKS control plane, and you only pay for the AKS nodes that run your applications.

## **Kubernetes Cluster Architecture:**

A kubernetes cluster is divided into two components:

- The `control plane`, which provides the core kubernetes services and orchestration of application workloads.
- The `nodes`, which run your application workloads.

![kubernetes-cluster-architecture](Images/kubernetes-cluster-architecture.png)

### **Control Plane:**

- When we create an AKS cluster, the Azure platform automatically creates and configures its associated control plane.
- This single-tenant control plane is provided at no cost as a managed Azure resource abstracted from the user.
- We only pay for the nodes attached to the AKS cluster.
- The control plane and its resources reside only in the region where you created the cluster.

**The control plane includes the following core kubernetes components:**

| **Component** | **Description** |
| --------------| ----------------|
| `kube-apiserver`| The API server exposes the underlying Kubernetes APIs and provides the interaction for management tools, such as `kubectl` or the kubernetes dashboard.|
| `etcd`| etcd is a highly available key vault store within Kubernetes that helps maintain the state of your kubernetes cluster and configuration. |
|`kube-scheduler`| When you create or scale applications, the scheduler determines what nodes can run the workload and starts the identified nodes.|
|`kube-controller-manager`| The controller manager oversees a number of smaller controllers that perform actions such as replicating pods and handling node operations|

**NOTE:** Keep in mind that we can't directly access the control plane. Kubernetes control plane and node upgrades are orchestrated through the Azure Portal. To Troubleshoot possible issues, you can review the control plane logs using Azure Monitor.

### **Nodes:**

- To run your applications and supporting services, you need a kubernetes node.
- Each `AKS Cluster` has at least one node, an Azure Virtual Machine(VM) that runs the kubernetes node components and container runtime.

**Nodes include the following core kubernetes components:**

|**Component**| **Description**|
|-------------| ----------------|
|`kubelet`| The kubernetes agent that processes the orchestration requests from the control plane along with scheduling and running the requested containers.|
| `kube-proxy`| The proxy handles virtual networking on each node, routing network traffic and managing IP addressing for services and pods|
| `container runtime`| The container runtime allows containerized applications to run and interact with other resources, such as the virtual network or storage. |

![azure-aks-nodes-components](Images/azure-aks-node.png)

- The Azure VM size for your nodes defines CPUs, memory, size and the storage type available, such as high-performance SSD or regular HDD.
- Plan the node size around whether your applications might require large amounts of CPU and memory or high-performance storage.
- Scale out the number of nodes in your AKS cluster to meet demand.
- In AKS, the VM image for your cluster's nodes is based on Ubuntu Linux, or Windows Server 2022.
- When you create an AKS cluster or scale out the number of nodes, the Azure Platform automatically creates and configures the requested number of VMs.
- Agent Nodes are billed as standard VMs, so any VM size discounts, including Azure reservations, are automatically applied.
- For managed disks, default size and performance are assigned according to the selected VM SKU and vCPU count.
