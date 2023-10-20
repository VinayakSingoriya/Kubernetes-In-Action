# Service: ClusterIP
ClusterIP is the default service type in Kubernetes. It receives a cluster-internal IP address, making its pods only accessible from within the cluster.It is mainly used for Pod-to-Pod communication within the same cluster i.e. exposing groups of pods to other pods in the cluster.

Kubernetes will assign a cluster-internal IP address to ClusterIP service. This makes the service only reachable within the cluster i.e. You cannot make requests to service (pods) from outside the cluster.

You can specify your own cluster IP address as part of a Service creation request. To do this, set the .spec.clusterIP field.

## Create a ClusterIP service using a yaml file
```bash
$ kubectl create -f <service>.yaml
```
## Get the list of services in a cluster
```bash
$ kubectl get svc
```
## Testing your services within the cluster
You can send requests to your service from within the cluster in a few ways:

- The obvious way is to create a pod that will send the request to the service’s
cluster IP and log the response. You can then examine the pod’s log to see
what the service’s response was.

- You can ssh into one of the Kubernetes nodes(minikube) and use the curl command.

    ```bash
    $ minikube ssh
    $ curl <Cluster_IP>
    ```
    *Note:* curl-ing the service works, but pinging it doesn’t. That’s because the service’s
cluster IP is a virtual IP, and only has meaning when combined with the service port.
- You can execute the curl command inside one of your existing pods through
the kubectl exec command.

    ```bash
    $ kubectl exec <pod_name> -- curl -s http://<Cluster_IP>
    ```

## Session Affinity on the Service
If you execute the curl command on the ClusterIP a few more times, you should hit a different pod with every invocation, because the service proxy normally forwards each connection to a randomly selected backing pod, even if the connections are coming from the same client.

If, on the other hand, you want all requests made by a certain client to be redi-
rected to the same pod every time, you can set the service’s sessionAffinity property to ClientIP (instead of None, which is the default).

**Note**: Kubernetes services don’t operate at the HTTP level. Services
deal with TCP and UDP packets and don’t care about the payload they carry. Because
cookies are a construct of the HTTP protocol, services don’t know about them, which
explains why session affinity cannot be based on cookies.

## Exposing multiple ports in the same service
Your service exposes only a single port, but services can also support multiple ports.

For example, if your pods listened on two ports—let’s say 8080 for HTTP and 8443 for
HTTPS—you could use a single service to forward both port 80 and 443 to the pod’s
ports 8080 and 8443. You don’t need to create two different services in such cases. Using a single, multi-port service exposes all the service’s ports through a single cluster IP. 

**Note**: When creating a service with multiple ports, you must specify a name
for each port.


## Usecase
Use this Service type when you want to expose an application within the cluster and allow other Pods within the cluster to access it.
