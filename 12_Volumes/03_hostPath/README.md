# Volume: hostPath

A **hostPath** volume points to a specific file or directory on the node’s filesystem. Pods running on the same node and using the same path in their host-
Path volume see the same files.

If a pod is deleted and the next pod uses a hostPath volume pointing to the same path on the host, the new pod will see whatever was left behind by the previous pod, but only if it’s scheduled to the same node as the first pod.

If you’re thinking of using a hostPath volume as the place to store a database’s
data directory, think again. Because the volume’s contents are stored on a specific
node’s filesystem, when the database pod gets rescheduled to another node, it will no longer see the data.

The *hostPath* volumes are often used for trying out persistent storage in single-node clusters, such as the one created by Minikube.

*Note*: Remember to use hostPath volumes only if you need to read or write system files on the node.Never use them to persist data across pods.