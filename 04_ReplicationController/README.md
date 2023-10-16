# ReplicationController
In Kubernetes, a **ReplicationController** is an API resource that ensures a specified number of pod replicas are running at all times.

If the number of pods falls below the desired count, the ReplicationController automatically creates new pods to restore the desired state. Conversely, if there are more pods than desired, it will terminate excess pods.

A ReplicationController has three essential parts:
- A **label selector**, which determines what pods are in the ReplicationController’s scope
- A **replica count**, which specifies the desired number of pods that should be running
- A **pod template**, which is used when creating new pod replicas

## Create a ReplicationController resource using a yaml file
```bash
$ kubectl create -f <rc_name>.yaml
```

**Note**: The shorthand for *replicationcontroller* is *rc*

## Get the additional information about ReplicationController
```bash
$ kubectl describe rc <rc_name>
```

## List all the ReplicationController resources
```bash
$ kubectl get rc
```
## Scaling a ReplicationController using command
```bash
$ kubectl scale rc <rc_name> --replicas=10
```

## Delete ReplicationController as well as Pods
```bash
$ kubectl delete rc <rc_name>        
```

## Delete only ReplicationController but not the Pods 
### ( After the deletion of ReplicationController, the pods becomes unmanaged )
```bash
$ kubectl delete rc <rc_name> --cascade=false  
```

### Points to remember:
- If you modified the
ReplicationController’s label selector then it would make all the pods fall out of the scope of the
ReplicationController, which would result in it creating new pods again to reach out to the to replica count.
- If you change the ReplicationControler's Pod template (i.e container image, name etc.) then it will only affect the pod afterward and will have no effect on the old one's. 

    To modify the old pods, you’d need to delete them and let the ReplicationController replace them with new ones based on the new template.

