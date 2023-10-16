# POD
A "Pod" is the smallest deployable unit, and it represents a single instance of a running process in a cluster. A Pod can contain one or more containers that share the same network namespace, storage, and configuration.

### Get the information about Pod:
```bash
$ kubectl explain pod
$ kubectl explain pod.spec
```

### Create a Pod using a yaml file
```sh
$ kubectl create -f pod.yml
```

### Check the log of a container(If there is only a single container in a Pod)
```bash
$ kubectl logs <pod_name>
```

### Check the logs if there are multiple containers in a Pod
```bash
$ kubectl logs <pod_name> -c <container_name>
```

### Access a Pod without any service (usually for debugging)
```bash
$ kubectl port-forward <pod_name> <host_port>:<container_port>
```
### Delete a Pod by name
```bash
$ kubectl delete pod <pod_name>
```

## Labels
A label is an arbitrary key-value pair you attach to a resource, which is then utilized when selecting resources using label selectors.

### List Pods along with their labels
```bash
$ kubectl get pod --show-labels
```

### List Pods Against Specific Labels
```bash
$ kubectl get pod -L <label1_name>,<label2_name>
```

### List Pods Against a Specific 'Key=Value'
```bash
$ kubectl get pod -l <label_key>=<label_value>
$ kubectl get pod -l <label1_name>
```

### List all Pods except those with a specific label
```bash
$ kubectl get po -l '!<label_name>'
```

### List all Pods whose label key is not set to a specific label value
```bash
$ kubectl get pod -l '<label_key>!=<label_value>'
```

### List all Pods whose label key is not set to either of two label values
```bash
$ kubectl get pod -l '<label_key> notin (<label_value1>,<label_value2>)'
```

### Add labels to an existing Pod:
```bash
$ kubectl label pod <pod_name> <label_key>=<label_value>
```

### Update the value of an existing label on a Pod
```bash
$ kubectl label pod <pod_name> <existing_label_key>=<label_new_value> --overwrite
```

### Add labels to a Kubernetes node
```bash
$ kubectl label node <node_name> <node_label_key>=<node_label_value>
```

### Delete Pods that match a specific label
```bash
$ kubectl delete pod -l <label_key>=<label_value>
```

## Namespaces
In Kubernetes, a "Namespace" is a way to logically divide and isolate a Kubernetes cluster into multiple virtual clusters. It provides a scope for resources in a cluster, allowing you to create separate environments and prevent naming conflicts.

### Listing all the Namespaces in a cluster
```bash
$ kubectl get namespaces
```
or
```bash
$ kubectl get ns
```

### List all the pods running in a specific Namespaces
```bash
$ kubectl get pods -n <namespace_name>
```

### Create a namespace using a yaml file
```bash
$ kubectl create -f custom-namespace.yaml
```

### create a namespace using a command (without a yaml file)
```bash
$ kubectl create namespace <namespace_name>
```

### Create a resource in a specific Namespace
```bash
$ kubectl create -f custom-namespace.yaml -n <namespace_name>
```

### Delete a Namespace as well as delete all resources with in the same Namespace
```bash
$ kubectl delete ns <namespace_name>
```

### Delete all the pods in the current Namespace (but not the namespace)
```bash
$ kubectl delete po --all
```

### Deleting (almost) all resources in a current Namespace
```bash
$ kubectl delete all --all
```




