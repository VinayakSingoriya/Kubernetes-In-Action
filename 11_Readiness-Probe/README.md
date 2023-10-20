# Readiness Probe
In Kubernetes, a readiness probe is a mechanism used to determine when a container within a pod is ready to accept network traffic. It is an important concept for ensuring the reliability and availability of applications running in Kubernetes clusters.

When a container is started, Kubernetes can be configured to wait for a configurable
amount of time to pass before performing the first readiness check. The readiness probe is invoked periodically and determines whether the specific
pod should receive client requests or not. When a container’s readiness probe returns success, it’s signaling that the container is ready to accept requests and if pod’s readiness probe fails, the pod is removed from the Endpoints object.

A readiness probe is defined in the pod's configuration and is associated with a specific container. The purpose of the readiness probe is to help Kubernetes determine whether a container is in a healthy state to serve incoming requests. If the readiness probe indicates that the container is not ready, Kubernetes will not send network traffic to that container until it becomes ready. This prevents traffic from being sent to a container that may still be initializing or experiencing issues.

*A readiness probe makes sure clients only talk to those healthy pods and never
notice there’s anything wrong with the system.*

## Type of Readiness Probes
The three types of readiness probes exist:
- An **Exec probe**, where a process is executed. The container’s status is determined by the process’ exit status code.
- An **HTTP GET probe**, which sends an HTTP GET request to the container and
the HTTP status code of the response determines whether the container is ready or not.
- A **TCP Socket probe**, which opens a TCP connection to a specified port of the
container. If the connection is established, the container is considered ready.

## Liveness Probe v/s Readiness Probe
- Liveness probes keep pods healthy by killing off unhealthy containers and replacing them with new, healthy ones, whereas readiness probes make sure that only pods that are ready to serve requests receive them.
- Unlike liveness probes, if a container fails the readiness check, it won’t be killed or restarted, it just get removed from the endpoint object.