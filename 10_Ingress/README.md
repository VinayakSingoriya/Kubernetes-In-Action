# Kubernetes: Ingress Resource
Kubernetes ingress is a powerful tool for managing external access to your Kubernetes services. It acts as a layer between your services and the outside world, providing load balancing, SSL termination, and routing based on your defined rules.

*Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource.*

Although the ingress is just another way of exposing services outside the cluster, it is not itself considered a service type. It is a separate API object type.

An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type Service.Type=NodePort or Service.Type=LoadBalancer.



## Understand why Ingress are needed
- Each LoadBalancer service requires its own load balancer with its own public IP address, whereas an Ingress only requires one, even when providing access to dozens of services. When a client sends an HTTP request to the Ingress, the host and path in the request determine which service the request is forwarded to.

- Ingresses operate at the application layer of the network stack (HTTP) and can provide features such as cookie-based session affinity and the like, which services can’t.

## How Kubernetes Ingress Works
The way it works at a high level is that you first deploy what is called an **Ingress Controller**. This controller is the actual engine that executes the rules of the ingress by translating them and routing the traffic accordingly.

An ingress controller is like a load balancer which has some forwarding rules. And these rules are passed to this load balancer through an ingress object. Yes, we need both an *ingress controller* and an *ingress resource/object* in Kubernetes.

The first step to enable ingress routing is to install the ingress controller.There are a couple of ingress controller implementations out there, but the most popular are **Nginx** and **HAProxy**.

## Create an Ingress Resource using Yaml file
```bash
$ kubectl create -f <ingress_resource>.yaml
```

## Get the list of Ingress Resources
```bash
$ kubectl get ingresses
```
or 
```bash
$ kubectl get ing
```

*Note*: The shorthand for Ingress is ing.

## Understand Ingress Resource

Inside the ingress resource, we can define:

- The **host** where the rules are applied, e.g., for "example.com" host or "other-example.org"
- A specific **path**, e.g., "example.com/path/to/shop"
- Whether to use HTTP or HTTPS.
- The **service** and the **port** to route the traffic to when it matches these rules.

---

The ingress controller makes it possible to have dozens of services running inside your cluster, and you redirect the traffic to each one using only one external-facing IP.

Requests received by the controller will be forwarded to either service foo or bar,
depending on the Host header in the request (the way virtual hosts are handled in
web servers). DNS needs to point both the foo.example.com and the bar.exam-
ple.com domain names to the Ingress controller’s IP address.

But wait! Didn’t we mention previously that the ingress controller pods are deployed inside the cluster? So how does the traffic reach the ingress controller in the first place?

The idea is that you want to expose your ingress controller itself to the outside network. This way, it can receive external traffic. But this time, the difference is that you only expose a single service through the LoadBalancer, which is the ingress controller service. Then it’s up to this service to route the traffic to other backend services in the cluster.

And this way, you can use a single load balancer IP to forward traffic to all your services. And it’s the responsibility of the ingress controller to decide where to direct traffic. Based on its rules and how the content matches those rules, it will decide which service it should forward requests to.

So the Path now is:

**Client -> LoadBalancer -> Ingress controller -> Other services -> Pod**

## Configuring a LoadBalancer
Now you need to create a LoadBalancer service that receives traffic on port 80 and forwards it to the ingress-service. What happens now is that the cloud provider will provision a new external load balancer with a public IP address. Then it adds a rule to it for forwarding traffic to the ingress-service.

When traffic reaches the load balancer at the <Loadbalancer-IP>:80, it will be redirected to the ingress-service. Next, the ingress controller will check the contents of the traffic and apply a matching rule, if found, and forward it to service 1 or service 2. Finally, this traffic reaches the Pods.