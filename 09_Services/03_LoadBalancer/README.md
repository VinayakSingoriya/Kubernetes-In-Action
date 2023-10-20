# Service: LoadBalancer
A LoadBalancer Service is another way you can expose your applications to external clients.LoadBalancer service is an extension of a NodePort service. However, it only works if you're using Kubernetes on a cloud platform that supports this Service type.

Now, when you create a LoadBalancer Service, Kubernetes detects which cloud computing platform your cluster is running on and creates a load balancer in the infrastructure of the cloud provider. The load balancer will have its own unique, publicly accessible IP address that clients can use to connect to your application.

For example, if you're running a Kubernetes cluster on a cloud platform like Amazon Web Services (AWS), you can create a LoadBalancer Service. When you do this, Kubernetes will create an Elastic Load Balancer in AWS to route traffic to the nodes in your cluster.

Note that the LoadBalancer Service this time builds on top of the NodePort Service, with an added benefit: It adds load balancing functionality to distribute traffic between nodes. This reduces the negative effects of any one node failing or becoming overloaded with requests.

If Kubernetes is running in an environment that doesn’t support LoadBalancer services, the load balancer will not be provisioned, but the service will still behave like a NodePort service.

The traffic coming from external clients goes through a path like this: External client -> Loadbalancer -> Worker NodeIP:NodePort -> ClusterIP Service -> Pod.

## Create a ClusterIP service using a yaml file
```bash
$ kubectl create -f <service>.yaml
```
## Get the list of services in a cluster
```bash
$ kubectl get svc
```

Now the load balancer is available at IP <External_IP> (which is retrieved from t the above command), so you can now access the service at that IP address:
```bash
$ curl http://<External_IP>
```

## Usecase
Use this Service type when you want to expose your application to external clients. Sounds like the same thing mentioned for NodePort. But, there's the added benefit. You take advantage of a cloud provider's load balancing capabilities. And all client requests can be smoothly load balanced to multiple nodes in your cluster.

LoadBalancer Services are typically used in production environments. Why? One big reason is the increased reliability. When clients connect to one node specifically (through NodePort), if that node fails, the clients will be left hanging. Their requests will remain unfulfilled as the node is unreachable.

But, with a LoadBalancer, if one node fails, the LoadBalancer doesn't rely on a single node (it sends traffic to all). So only a few requests hitting the problematic node will fail, not all.

And with proper health checks in place, the LoadBalancer can stop sending traffic to the failed node. So future client requests can all land on healthy nodes.
