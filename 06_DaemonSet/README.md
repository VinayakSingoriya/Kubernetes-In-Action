# DaemonSet
The DaemonSet object is designed to ensure that a single pod runs on each worker node. This means you cannot scale daemonset pods in a node. And for some reason, if the daemonset pod gets deleted from the node, the daemonset controller creates it again.

A DaemonSet makes sure it creates as many pods as there are nodes and deploys
each one on its own node. If a node goes down, the DaemonSet doesn’t cause the pod to be created elsewhere. But when a new node is added to the cluster, the DaemonSet immediately deploys a new pod instance to it.

A DaemonSet deploys pods to all nodes in the cluster, unless you specify that the pods should only run on a subset of all the nodes.

For example, you’ll want to run a log collector and a resource monitor on every
node.

## Create a DaemonSet using Yaml file
```bash
$ kubectl create -f <ds_name>.yaml
```

## List all the DeamonSet resources
```bash
$ kubectl get ds
``` 

**Note**: The shorthand for *DaemonSet* is *ds*.
