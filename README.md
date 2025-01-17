
# Kubernetes Architecture

Kubernetes operates with the following key components:

## 1. Master Node
The **Master Node** is responsible for managing the Kubernetes cluster. It runs essential processes required to control and maintain the cluster:

1. **API Server**: Acts as the entry point to the Kubernetes cluster and processes REST API requests.
2. **Controller Manager**: Monitors the state of the cluster, ensuring desired states are maintained (e.g., recreating failed pods or nodes).
3. **Scheduler**: Allocates pods to worker nodes based on workload and resource availability.
4. **etcd**: A distributed key-value store that maintains the clusterâ€™s state. It is critical for disaster recovery and rebuilding the cluster using snapshots.
5. **Virtual Network**: Ensures communication between master and worker nodes.

The **Master Node** is vital for cluster operation. In production, it is recommended to have **at least two master nodes** to provide high availability. If one master node fails, the cluster will continue functioning without disruption.

## 2. Worker Node
A **Worker Node** is a physical or virtual machine that runs application workloads. Each worker node contains:

- **Kubelet**: A process that ensures the worker node communicates with the master node and manages pod deployment on the node.
- **Pods**: Containers encapsulating applications. Multiple applications can run across different pods on the worker node.

Applications run on **Worker Nodes**, which handle high workloads and resource utilization.

---

## Main Kubernetes Components

### 1. **Pod**
- The smallest deployable unit in Kubernetes, representing a single instance of an application.
- Each pod gets a unique, ephemeral internal IP address. These IPs change when pods are recreated, making them unsuitable for long-term connections.
- Pods are **ephemeral**, meaning they can be terminated and lose their data. To address this, **Services** and **Volumes** are used.

### 2. **Service**
- Provides a stable, static IP address to enable communication with pods.
- Service types:
  - **Internal Service**: Accessible only within the cluster (default).
    - **External Service**: Exposes the application to the internet.

    ### 3. **Ingress**
    - Manages HTTP and HTTPS traffic into the cluster.
    - Provides rules for routing requests to specific services.

    ### 4. **ConfigMap**
    - Stores configuration data (e.g., application endpoints) for pods to use during runtime.

    ### 5. **Secret**
    - Stores sensitive information (e.g., passwords, certificates) in Base64-encoded format.

    ### 6. **Volumes**
    - Attach persistent storage to a pod, ensuring data is not lost when the pod is restarted.

    ### 7. **Deployment**
    - Manages the desired state of pods and replicates them across nodes for high availability.
    - Automatically handles pod creation, deletion, and updates.

    ### 8. **StatefulSet**
    - Used for stateful applications, like databases, to maintain data consistency and identity across pods.
    - Note: Hosting databases outside the Kubernetes cluster is recommended, as deploying stateful applications in Kubernetes is complex.

    ### 9. **DaemonSet**
    - Ensures that a copy of a specific pod runs on every node in the cluster.

    ---

    ## Key Points:
    - **Master Nodes** are critical for cluster management; always ensure redundancy.
    - **Worker Nodes** handle high workloads and resource utilization, hosting application pods.
    - Use **Deployments** for stateless applications and **StatefulSets** for stateful ones.
    - Databases are often better hosted outside Kubernetes due to the challenges in maintaining stateful workloads within the cluster.