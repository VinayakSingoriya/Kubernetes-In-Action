# Job Resource
Kubernetes **Job-Resource** allows you to run a pod whose container isn’t restarted when the process running inside finishes successfully. Once it does, the pod is considered complete. Jobs are useful for ad-hoc tasks.

In the event of a node failure, the pods on that node that are managed by a Job will
be rescheduled to other nodes the way ReplicaSet pods are.

## Create  a Job Resource using a Yaml file
```bash
$ kubectl create -f <job_name>.yaml
```

## Get the Job Resources
```bash
$ kubectl get jobs
```