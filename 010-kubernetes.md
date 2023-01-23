## Kubernetes

Kubernetes is an open-source container orchestration system for automating the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

Kubernetes uses a declarative approach to manage the desired state of an application. This means that you define what you want your application to look like, and Kubernetes makes sure that the actual state of the application matches your desired state.

One of the key features of Kubernetes is its ability to automatically scale and manage the number of replicas of an application. This allows for horizontal scaling, which means that the application can automatically scale to handle more traffic by adding more replicas of the application.

Kubernetes also provides self-healing capabilities. If a container or a node fails, Kubernetes automatically replaces it with a new one. This helps to ensure that the application is always available and running.

Kubernetes provides service discovery and load balancing. A Kubernetes service is a logical abstraction over a set of pods, providing a stable endpoint for external clients to access the application. Kubernetes automatically load balances traffic across the available replicas of an application.

Kubernetes runs on a cluster of machines and is made up of several components including the Kubernetes Master, which is responsible for the overall management of the cluster, and the Kubernetes Nodes, which are the worker machines that run the containerized applications. Kubernetes also provides a command-line interface (CLI) and an API for interacting with the cluster.

Kubernetes is often used in conjunction with container orchestration systems such as Docker, as well as other technologies such as Prometheus for monitoring and Grafana for visualization. Kubernetes can also be used with various cloud providers such as AWS, Azure and GCP.

---

### Architecture

The Kubernetes architecture is composed of several main components:

!['components-of-kubernetes'](./assets/components-of-kubernetes.svg)

1. `API server` is the core component that exposes the Kubernetes API and handles all API requests. It is responsible for maintaining the desired state of the cluster, such as creating, updating, and deleting resources.

2. `Controller manager` is a daemon that runs on the master node and manages the state of the cluster. It runs various controllers, such as the replication controller, which ensures that the desired number of replicas of a pod are running.

3. `etcd` is a distributed key-value store that is used to store the configuration data of the Kubernetes cluster, such as the desired state of the resources. It is a critical component of the control plane and is used by the API server to store and retrieve data.

4. `Kubelet` is a daemon that runs on each worker node and is responsible for maintaining the state of the pods on that node. It communicates with the API server to ensure that the desired number of replicas of a pod are running and that the containers within the pods are healthy.

5. `kube-proxy` is a daemon that runs on each worker node and is responsible for networking and service discovery within the cluster. It forwards traffic to the correct pods based on the service definition and also load balances the traffic between the pods.

6. `Scheduler` is a component that runs on the master node and is responsible for scheduling pods to run on worker nodes. It takes into account factors such as available resources, network topology, and constraints defined by the user.

7. `Control plane` is the set of components that run on the master node and are responsible for maintaining the desired state of the cluster. This includes the API server, controller manager, and etcd.

8. `Node` is a worker machine in a Kubernetes cluster. It can be a physical or virtual machine that runs pods and is managed by the control plane. Each node runs the kubelet and kube-proxy daemons.

---

### Workloads

#### Pod

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled. In non-cloud contexts, applications executed on the same physical or virtual machine are analogous to cloud applications executed on the same logical host.

Example:

```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

---

#### ReplicaSet

A ReplicaSet in Kubernetes is an object that ensures a specified number of replicas of a pod are running and available at all times. It is responsible for creating and managing the pods, and it automatically replaces any pods that fail or are terminated.

A ReplicaSet is defined by a pod template, which specifies the configuration for the pods it creates, including the container image, resource requirements, and environment variables. It also has a selector, which is used to determine which pods it should manage.

When a ReplicaSet is created, it creates the desired number of replicas of the pods according to the pod template. It also continuously monitors the pods and ensures that the desired number of replicas are running. If a pod fails or is terminated, the ReplicaSet replaces it with a new one.

A ReplicaSet also allows for scaling the number of replicas up or down as needed. This can be done manually by updating the replica count in the ReplicaSet or automatically by using a Horizontal Pod Autoscaler.

ReplicaSets are often used in conjunction with Deployments, which are higher-level objects that provide a way to declaratively update and roll back changes to the pods. Deployments create and manage Replica Sets and use them to ensure that the desired number of replicas are running and available at all times.

Example:

```bash
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: gcr.io/google_samples/gb-frontend:v3
```

---

#### Deployment

In Kubernetes, a Deployment is an object that represents a desired state for a set of pods. The Deployment object creates and manages Replica Sets, which in turn create and manage Pods.

When a Deployment is created, it specifies the desired number of replicas for a set of Pods. The Deployment then creates a Replica Set to ensure that the desired number of replicas are running and available at all times.

The Replica Set is responsible for creating and managing the Pods. It ensures that the specified number of replicas are running, and it automatically replaces any Pods that fail or are terminated.

When an update to the pods is needed, the Deployment updates the replicas by creating a new Replica Set. It does this by modifying the pod template in the Replica Set, and then scaling the number of replicas up or down as needed. The Deployment then gradually rolls out the update to the replicas, while ensuring that the desired number of replicas are running at all times.

The Deployment also provides a way to roll back changes to the pods in case of errors or problems. By keeping multiple Replica Sets, the Deployment can roll back to a previous version of the pods by scaling down the replicas in the current Replica Set and scaling up the replicas in a previous Replica Set.

In summary, a Deployment object creates and manages Replica Sets, which in turn create and manage Pods. The Deployment ensures that a specified number of replicas of a pod are running and available at all times, and it provides a way to update and roll back changes to the pods in a controlled manner.

Example:

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
