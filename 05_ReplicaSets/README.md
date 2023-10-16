# ReplicaSets
In Kubernetes, a ReplicaSet is a resource that ensures a specified number of pod replicas are running at all times. 

ReplicaSets are similar in purpose to ReplicationControllers but offer more advanced selectors for pod matching (new generation of ReplicationController).

## ReplicaSet V/S ReplicationController
- A ReplicaSet's label selector permits matching pods both with or without a certain label and based on label keys, regardless of their values, unlike a ReplicationController.

    For example, a ReplicationController can match either 'env=production' labeled pods or 'env=devel' labeled pods separately, while a single ReplicaSet can match both sets of pods together.
- A ReplicationController can’t match pods based merely on the presence
of a label key, regardless of its value, whereas a ReplicaSet can.

    For example, a ReplicaSet can match all pods that include a label with the key env, whatever its actual value is.

### Create a ReplicaSet using a yaml file
```bash
$ kubectl create -f <rs_name>.yaml
```

### List all the ReplicaSet resources in a cluster
```bash
$ kubectl get rs
```

**Note**: The shorthand for *ReplicaSet* is *rc*

### Get additional information about ReplicaSet
```bash
$ kubectl describe rs
```

### Delete ReplicaSet as well as Pods
```bash
$ kubectl delete rs <rs_name>        
```

### Delete only ReplicaSet but not the Pods 
#### ( After the deletion of ReplicaSet, the pods becomes unmanaged )
```bash
$ kubectl delete rs <rs_name> --cascade=false  
```

### Using the ReplicaSet’s more expressive label selectors
You can enhance the selector with additional expressions. Each expression includes a key, an operator, and, depending on the operator, a list of values. There are four valid operators:

- 'In' requires the label's value to match one of the specified values.
- 'NotIn' requires the label's value to not match any of the specified values.
- 'Exists' demands the presence of a label with the specified key (value doesn't matter).
- 'DoesNotExist' insists on the absence of a label with the specified key (values should not be specified)."

