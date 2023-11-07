# Kubernetes : Persistent Storage

When an application running in a pod needs to persist data to disk and have that
same data available even when the pod is rescheduled to another node, you can’t use
any volumes(emptyDir, hostPath, gitRepo etc.). Because this data needs to be accessible from any cluster node, it must be stored on some type of network-attached storage (NAS).

Running a database pod without a volume or with a non-persistent volume doesn’t make sense, except for testing purposes.