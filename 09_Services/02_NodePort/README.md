# Service: NodePort
The NodePort Service is a way to expose your application to external clients. An external client is anyone who is trying to access your application from outside of the Kubernetes cluster.

It exposes the Service on each Node's IP at a static port (the *NodePort*). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of *type: ClusterIP*.

A NodePort service builds on top of the ClusterIP service, exposing it to a port accessible from outside the cluster. If you do not specify a port(*NodePort*) number, Kubernetes automatically chooses a free port (between 30000–32767). The kube-proxy component on each node is responsible for listening on the node’s external ports and forwarding client traffic from the NodePort to the ClusterIP.

Note that a NodePort Service builds on top of the ClusterIP Service type. What this means is that when you create a NodePort Service, Kubernetes automatically creates a ClusterIP Service for it as well. The node receives the request, the NodePort Service picks it up, it sends it to the ClusterIP Service, and this, in turn, sends it to one of the Pods behind it (External Client -> \<NodeIP>:\<NodePort> -> \<ClusterIP>:\<Port> -> Pod).

By creating a NodePort service, you make Kubernetes reserve a port on all its nodes (the same port number is used across all of them) and forward incoming connections to the pods that are part of the service.

A connection received on port <NodePort> of the first node might be forwarded either to the pod running on the first node or to one of the pods running on the other nodes.

You can contact the NodePort Service, from outside the cluster, by requesting
**\<NodeIP>:\<NodePort>** (anyone who has access to the node) or **\<ClusterIP>:\<Port>** (within cluster)

## Create a NodePort service using a yaml file
```bash
$ kubectl create -f <NodePort_Service>.yaml
```

## Get the list of services in a cluster
```bash
$ kubectl get svc
```

*Note*: When using Minikube, you can easily access your NodePort services
through your browser by running 
```bash
$ minikube service <service-name> [-n <namespace>].
```

**Note**:

- If you only point your clients to the specific node, when that specific node fails, your clients can’t access the service anymore. That’s why it makes sense to put a load balancer in front of the nodes to make sure you’re spreading requests across all healthy nodes and never sending them to a node that’s offline at that moment.
- But if you only point your clients to the first node, when that node fails, your clients can’t access the service anymore. That’s why it makes sense to put a load balancer in front of the nodes to make sure you’re spreading requests across all healthy nodes and never sending them to a node that’s offline at that moment.

## Usecase
Use this Service type when you want to expose your application on a specific port on each worker node in the cluster, making it accessible to external connections (coming from outside the cluster). NodePort Services are often used for development and testing purposes.