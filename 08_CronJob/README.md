# Cron Job
A Kubernetes CronJob is a resource type used to schedule and automate the execution of jobs or tasks at specified time intervals or on a recurring schedule, similar to traditional cron jobs in Unix-like operating systems.

CronJobs are built on top of the Job resource, and they provide a convenient way to run batch tasks periodically within a Kubernetes cluster. 

## Create a Cron Job using a yaml file
```bash
$ kubectl create -f <cronJob_name>.yaml
```

