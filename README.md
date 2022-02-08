# ykubernetes

[Definition taken from their documentation](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/):

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

Features
--------
<details>
<summary>Service discovery and load balancing</summary>
Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
</details>
  
  
<details>
<summary>Storage orchestration</summary>
Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.
Automated rollouts and rollbacks You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.
</details>
<details>
<summary>Automatic bin packing</summary>
You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
</details>
<details>
<summary>Self-healing</summary>
Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.
</details>
<details>
<summary>Secret and configuration management</summary>
Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.
</details>

Kubernetes component

[<img src="https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg" width="600">](https://kubernetes.io/docs/concepts/overview/components/)


Object Defintions

|Object Type| Function |
-------------|:-----------|
|[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)|an object that can represent an application running on your cluster (governed by a spec)|
|[Service](https://kubernetes.io/docs/concepts/services-networking/service/)|is an abstraction which defines a logical set of Pods and a policy by which to access them (sometimes this pattern is called a micro-service). The set of Pods targeted by a Service is usually determined by a selector|
|[Node](https://kubernetes.io/docs/concepts/architecture/nodes/)|may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods|
|[Pod](https://kubernetes.io/docs/concepts/workloads/pods/)|the smallest deployable units of computing that you can create and manage in Kubernetes, a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers|
|[ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/)|an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume|
|[Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)|an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation|

Sample deployment spec

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
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

Workload Resources

- Deployments
- ReplicaSet
- StatefulSets
- DaemonSet
- Jobs
- TTL Controller for Finished Resources
- CronJob
- ReplicationController

