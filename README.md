# ykubernetes

### TLDR

Wow, try to capture kubernetes(k8s) in a couple fo lines, man this is hard, some things are complex. In a nutshell, k8s is a system used to automate the configuration and deployment of another system.


### Longer Story

Is the line above enough to understand k8s, no! But it is a start (started a sentence with *but*, my first grade teacher is cringing). 

[Definition taken from their documentation](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/):

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

`So this is more specific and captures the intended direction of k8s. But I am not feeling it. Like most things, you will have to live k8s for a while for it to sink in. In addition, k8s aims to address the following feature areas (compounding the problem):`


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


`Truth be told, I started this page to help me grok k8s, and created the following section called Object Definitions with good intentions. I was copying the style of the k8s documentation and may as well posted a link or better never created this page. Reviewing the documentation has led me to a different choice, commenting on the content as I review. To access the list, I mean the long list of so called objects (use the link to the more accurately named` [Resource Types](https://kubernetes.io/docs/reference/kubectl/overview/#resource-types)`). I leave the following list here to remain in shame.`

### Object Defintions

[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

A Deployment defines a desired state for the application or workload it manages, and continuously works to reconcile the current state with the desired state. If the current state does not match the desired state, the Deployment controller automatically creates or deletes replicas to achieve the desired state.

Deployments also provide rollback functionality to enable the user to roll back to a previous deployment revision if needed. This feature allows you to quickly and easily revert to a previous version of your application in case a new version introduces issues or bugs.

In addition, Deployments support rolling updates, which allow you to update your application or workload with zero downtime. This is achieved by creating a new replica set with the updated version of the application, and gradually scaling it up while scaling down the old replica set.

Deployments are a core building block in Kubernetes, and are used extensively to manage the lifecycle of applications and workloads in a Kubernetes cluster.


[Service](https://kubernetes.io/docs/concepts/services-networking/service/)

In Kubernetes, a Service is an object that provides a stable network endpoint for accessing a set of pods in a cluster. It acts as an abstraction layer over the underlying pods, providing a single DNS name and IP address that can be used to access the pods.

Services allow you to decouple the internal network topology of your application from the external network, and provide a way to access your application from within the cluster or from outside the cluster.

When you create a Service, Kubernetes automatically assigns it a stable IP address and DNS name that can be used to access the pods. The Service then uses labels and selectors to identify which pods it should route traffic to.

There are several types of Services in Kubernetes, including:

- ClusterIP: The default type, which exposes the Service on a cluster-internal IP address.
- NodePort: Exposes the Service on a port on each node in the cluster.
- LoadBalancer: Exposes the Service externally using a cloud provider's load balancer.
- ExternalName: Maps the Service to an external DNS name.

Services can also be combined with other Kubernetes objects, such as Deployments and ReplicaSets, to provide a complete solution for managing the lifecycle of your application in a Kubernetes cluster.

[Selector](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

In Kubernetes, a Selector is a field used to match objects in the Kubernetes API based on a set of criteria. It is commonly used to select a subset of objects that meet specific requirements, such as pods that belong to a particular service or deployment.

Selectors are used to specify the criteria for selecting objects based on their labels. Labels are key-value pairs that are attached to Kubernetes objects, such as pods, services, and deployments, to provide metadata that can be used for grouping and filtering.

Selectors can be used in several places in Kubernetes, including:

Services: A Service in Kubernetes selects a set of pods based on their labels. The Service provides a stable IP address and DNS name that can be used to access the pods.
Deployments and ReplicaSets: A Deployment or ReplicaSet in Kubernetes creates and manages a set of pods based on a desired state. The desired state is specified using a label selector, which selects the pods that should be managed by the Deployment or ReplicaSet.
Jobs and CronJobs: A Job or CronJob in Kubernetes creates and manages one or more pods to perform a specific task. The pods are selected based on a label selector.
Selectors are a powerful feature in Kubernetes that allow users to group and manage objects based on their labels. They provide a flexible and scalable way to select objects and perform operations on them, such as scaling, updating, or deleting.

[Node](https://kubernetes.io/docs/concepts/architecture/nodes/)

In Kubernetes, a Node is a worker machine that runs containerized applications. It can be either a physical or virtual machine, and is managed by the Kubernetes control plane.

Each Node in a Kubernetes cluster runs a container runtime, such as Docker, and runs one or more pods. A pod is the smallest deployable unit in Kubernetes, and can contain one or more containers that share the same network namespace and storage volumes.

Nodes are responsible for running the actual workloads in the form of containers. They communicate with the Kubernetes control plane to receive instructions on what containers to run and how to manage them. The control plane schedules containers onto Nodes based on resource availability and other factors, and monitors the health of the containers and Nodes.

Nodes have several components that enable them to run containers, including:

Container runtime: A software that runs containers, such as Docker, containerd, or CRI-O.
Kubelet: An agent that runs on each Node and communicates with the Kubernetes control plane. It is responsible for starting, stopping, and monitoring the containers on the Node.
kube-proxy: A network proxy that runs on each Node and enables the Service abstraction in Kubernetes. It maintains network rules on the Node that allow communication to the pods.
Nodes are a fundamental building block in Kubernetes, and are used to provide compute resources for running containerized applications. They can be added or removed from a cluster dynamically to scale up or down the capacity of the cluster.


[Pod](https://kubernetes.io/docs/concepts/workloads/pods/)

what is a pod in kubernetes?
In Kubernetes, a Pod is the smallest deployable unit that represents a single instance of a running process in a cluster. It is a logical host for one or more tightly-coupled containers that share the same network namespace and storage volumes.

Pods are used to deploy, run, and scale containerized applications in a Kubernetes cluster. They provide an abstraction layer that isolates the application from the underlying infrastructure, and make it easier to manage the application lifecycle.

Each Pod in a Kubernetes cluster is assigned a unique IP address, and can communicate with other Pods in the cluster using that IP address. Pods can also be exposed to the outside world using a Service, which provides a stable IP address and DNS name that can be used to access the Pod.

Pods are usually managed by a higher-level object, such as a Deployment or ReplicaSet, which defines the desired state of the Pod and ensures that the specified number of replicas are running. When a Pod is created or deleted, the Kubernetes control plane automatically handles the scheduling and rescheduling of the Pods to ensure that the desired state is achieved.

Each Pod in Kubernetes is designed to be ephemeral, meaning that it can be created, destroyed, and replaced as needed without affecting the overall application. This makes it easier to scale and manage containerized applications in a dynamic environment.


[ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/)

In Kubernetes, a ConfigMap is an object that stores configuration data as key-value pairs. It provides a way to decouple configuration data from the container image, and manage it separately from the application code.

ConfigMaps are often used to store configuration data for applications running in a Kubernetes cluster, such as environment variables, command-line arguments, or configuration files. This allows the application to be easily configured and customized without needing to rebuild the container image.

ConfigMaps can be created from literal values, files, or directories, and can be mounted as volumes in a pod. This makes it easy to provide configuration data to applications running in containers, and to update the configuration data without having to rebuild or redeploy the container image.

ConfigMaps can also be used to provide configuration data to other Kubernetes objects, such as Deployments or StatefulSets. This allows the configuration data to be shared across multiple pods or replicas, and to be updated in a centralized location.

ConfigMaps are a powerful feature in Kubernetes that make it easy to manage configuration data for containerized applications. They provide a flexible and scalable way to manage configuration data in a dynamic and distributed environment.


[Custom Resources (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)

In Kubernetes, a Custom Resource Definition (CRD) is a way to extend the Kubernetes API by creating a new resource type. It allows users to define their own custom resources and define how they are stored, validated, and managed by the Kubernetes control plane.

CRDs are used to add new objects to the Kubernetes API, which can be used to manage custom applications or services. They allow users to define their own specifications for the new resource, which can be used to provide additional functionality or features beyond what is provided by the built-in Kubernetes objects.

To create a CRD, a user defines the custom resource schema in a YAML file and uses the Kubernetes API to create the new resource type. Once the CRD is created, it can be used to create new instances of the custom resource, which can be managed like any other Kubernetes object.

CRDs are a powerful feature in Kubernetes that allow users to extend the Kubernetes API to meet their specific needs. They provide a flexible and scalable way to manage custom resources and applications in a Kubernetes cluster.


[Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)

A Kubernetes Operator is a custom controller that extends the Kubernetes API to manage complex applications or services. It is a software pattern that uses the Kubernetes API to automate the deployment, scaling, and management of complex applications or services that have specialized requirements beyond what can be handled by the default Kubernetes controllers.

Operators are typically used for stateful applications that require complex deployment and management operations. Examples of such applications include databases, message queues, and big data processing engines. In essence, an operator is an intelligent controller that understands the application it is managing and can perform tasks such as backup and recovery, data migration, and configuration management.

Operators are built using the Kubernetes API, and they use custom resource definitions (CRDs) to define new objects that can be managed by the operator. The operator watches for changes to these objects and performs the necessary operations to ensure that the desired state of the application is maintained. This allows operators to automate complex management tasks that would otherwise require manual intervention.

Operators can be written in any language, and they are typically packaged and distributed as Docker containers. There are also many open-source operators available for popular applications, such as PostgreSQL, Apache Kafka, and Prometheus, which can be deployed in a Kubernetes cluster to manage these applications with ease.

---

`We now realize that there is a lot to this and has spurred on the creation of many tools that help tame the tasks involved with k8s. For example:` [helm charts](/helm.md)





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

