# Services
Pods need a way of finding other pods if they want to consume the services they
provide. In Kubernetes,
- *Pods are ephemeral*: They may come and go at any time.
- *Kubernetes assigns an IP address to a pod after the pod has been scheduled to a node and before it’s started*- Clients thus can’t know the IP address of the server pod.
- *Horizontal scaling means multiple pods may provide the same service* - Each of those pods has its own IP address. Clients shouldn’t care how many pods are backing
the service and what their IPs are. They shouldn’t have to keep a list of all the
individual IPs of pods. Instead, all those pods should be accessible through a
single IP address.

To solve these problems, Kubernetes also provides another resource type: **Services**

A Kubernetes **Service** is a resource you create to make a single, constant point of entry to a group of pods providing the same service. Each service has an IP address and port that never change while the service exists.

The Service API, part of Kubernetes, is an abstraction to help you expose groups of Pods over a network. Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible

It enables communication between nodes, pods, and users of app, both internal and external, to the cluster. Service also provides load balancing when you have Pod replicas. The set of Pods targeted by a Service is usually determined by a **selector** that you define.

For some parts of your application (for example, frontends) you may want to expose a Service onto an external IP address, one that's accessible from outside of your cluster.Kubernetes Service types allow you to specify what kind of Service you want.

The available type values and their behaviors are:
1. ClusterIP
2. NodePort
3. LoadBalancer




