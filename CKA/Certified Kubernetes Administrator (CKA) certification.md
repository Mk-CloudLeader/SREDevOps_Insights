# Certified Kubernetes Administrator (CKA) Certification
## A Guide to Mastering Kubernetes Administration

# CKA Exam Overview
- **Exam Format:** 2-hour online, performance-based exam.
- **Cost:** Approximately $300 USD.
- **Passing Score:** 66%
- **Exam Content:** Focuses on real-world Kubernetes administration tasks.

# Core Concepts (19%)
- Kubernetes Architecture
- API Primitives: Pods, Deployments, Namespaces, etc.
- Understanding the Kubernetes API and its usage.

### Kubernetes Architecture
- Master Node Components:
  - API Server: Frontend of the Kubernetes control plane.
  - etcd: Distributed key-value store that holds all cluster data.
  - Controller Manager: Ensures the cluster is in the desired state.
  - Scheduler: Assigns pods to nodes based on resource availability.
- Worker Node Components:
  - Kubelet: Agent running on each node that ensures containers are running in pods.
  - Kube-Proxy: Manages networking for pods, including routing and load balancing.
  - Container Runtime: Responsible for running containers (e.g., Docker, containerd).
- Kubernetes API Objects
  - Pods: Smallest deployable units that can contain one or more containers.
  - ReplicaSets: Ensure a specified number of pod replicas are running.
  - Deployments: Provide declarative updates to applications.
  - Namespaces: Provide a way to divide cluster resources between multiple users.
  - ConfigMaps & Secrets: Store configuration data and sensitive information.
- Hands-On Practice
  - Create and manage Kubernetes objects using kubectl.
```
kubectl run nginx --image=nginx
kubectl get pods
kubectl create configmap app-config --from-literal=key=value
```

# Installation, Configuration, and Validation (25%)
- Setting up a Kubernetes cluster (kubeadm, kops, etc.).
- Configuring networking (CNI plugins).
- Verifying the cluster setup and validating node and pod statuses.


#### Setting Up a Cluster
- Using kubeadm:
  - kubeadm init initializes the control plane.
  - kubeadm join adds worker nodes to the cluster.
- Networking:
  - Install a CNI plugin (e.g., Calico, Flannel) after initializing the cluster.
- HA Clusters:
  - Set up a highly available Kubernetes cluster with multiple control planes.
- Validating the Cluster
  - Check the status of nodes and pods
  - Verify that all control plane components are running
 
```
kubectl get nodes
kubectl get pods -A
```
- Access Control
  - RBAC (Role-Based Access Control):
    - Define who can do what within the cluster.
    - Manage access using Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings.

- Hands-On Practice
  - Set up a Kubernetes cluster on a cloud provider or locally using Minikube or Kind.
  - Practice creating roles and managing access

```
kubectl create role pod-reader --verb=get --verb=list --resource=pods
kubectl create rolebinding read-pods --role=pod-reader --user=developer

```
# Workloads & Scheduling (15%)
- Managing deployments, StatefulSets, and DaemonSets.
- Job and CronJob management.
- Understanding and implementing resource requests and limits.

#### Managing Workloads
- Deployments:
  - Deploy stateless applications.
  -  Rolling updates and rollbacks.
  -  Scaling deployments.
- StatefulSets:
  - Deploy stateful applications that require stable storage.
- DaemonSets:
  - Ensure that a pod runs on all or some nodes.
- Scheduling
  - Pod Scheduling:
    - Use node selectors and affinity/anti-affinity rules.
    - Manage taints and tolerations to control pod placement.
- Jobs & CronJobs:
  - Run batch tasks and scheduled jobs.
- Hands-On Practice
  - Deploy and manage applications
```
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=3
kubectl rollout status deployment nginx

```
  - Configure pod scheduling based on labels and node affinity.

# Services & Networking (20%)
- Configuring Services, Endpoints, and Network Policies.
- Ingress Controllers and Ingress Resources.
- Understanding Service types: ClusterIP, NodePort, LoadBalancer.

#### Service Types
  - ClusterIP: Default service type, accessible only within the cluster.
  - NodePort: Exposes the service on a static port on each node.
  - LoadBalancer: Exposes the service externally using a cloud provider's load balancer.
  - Headless Services: Provide direct access to individual pods without load balancing.
- Networking Basics
  - CNI Plugins: Manage pod networking within the cluster.
- Ingress Controllers:
  - Manage external access to services in a cluster.
  - Define rules for routing external traffic to services.
- Network Policies:
  - Control traffic flow between pods and between pods and network endpoints.
- Hands-On Practice
  - Create and expose services
```
kubectl expose deployment nginx --type=NodePort --port=80
kubectl get svc

```
  - Set up an Ingress resource
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx
            port:
              number: 80

```

# Storage (10%)
- Persistent Volumes (PV) and Persistent Volume Claims (PVC).
- StorageClasses and dynamic provisioning.
- Managing Kubernetes storage and volume lifecycle.

#### Persistent Volumes and Claims
- Persistent Volumes (PV):
  -  A piece of storage in the cluster that has been provisioned by an administrator.
- Persistent Volume Claims (PVC):
  - A request for storage by a user.
- Dynamic Provisioning
- StorageClasses:
  - Define different classes of storage.
  - Allow dynamic provisioning of PVs based on the PVC.
- Volume Types
  - emptyDir, hostPath, nfs, cephfs, etc.
- Hands-On Practice
  - Create a PersistentVolume and PersistentVolumeClaim
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-example
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

```
  - Use a PVC in a Pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: storage-pod
spec:
  containers:
  - name: busybox
    image: busybox
    command: [ "sleep", "3600" ]
    volumeMounts:
    - mountPath: "/mnt/data"
      name: mypvc
  volumes:
  - name: mypvc
    persistentVolumeClaim:
      claimName: pvc-example

```

# Troubleshooting (30%)
- Diagnosing and resolving cluster issues.
- Understanding and analyzing pod failures.
- Debugging and investigating network and storage issues.

# Best Practices for Exam Preparation
- **Hands-on Practice:** Set up a local Kubernetes cluster using Minikube or Kind.
- **Use Labs:** Sites like Katacoda, Play with Kubernetes, and Kubernetes the Hard Way.
- **Time Management:** Practice solving problems within a set time limit.
- **Study Resources:** Official Kubernetes documentation, CKA-specific study guides, and community blogs.

# Resources
- **Official Kubernetes Documentation:** https://kubernetes.io/docs/
- **CKA Exam Curriculum:** https://www.cncf.io/certification/cka/
- **Practice Labs:** https://github.com/dgkanatsios/CKAD-exercises
- **Books and Courses:** 
  - "Kubernetes Up & Running" by Kelsey Hightower
  - "Certified Kubernetes Administrator (CKA) with Practice Tests" on Udemy
 
- Killer.sh CKA Simulator: https://killer.sh/cka
 

