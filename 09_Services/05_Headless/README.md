# Headless Service
In Kubernetes, Services provide a stable IP address for clients to connect to Pods. A client makes a request to the Service. Then the Service forwards that request to one of the Pods associated with it. The client does not know which Pod it is connected to, nor does it care about it.

But what if the client wants to see the Pods’ IP addresses, so that it has complete control over which Pod(s) it can connect to? In such cases, Kubernetes provides the concept of headless Services.

A Kubernetes headless Service allows a client to connect to whichever Pod it prefers, directly. It doesn’t route the client request like a regular Service does.

*To make this Service headless, we need to add the "clusterIP" field and set its value to "None".*

The Service does not have a cluster IP, which means that it does not load balance traffic across any Pods. Instead of forwarding traffic, the Service behaves differently.

When a client sends a request to a headless Service, it will get back a list of all Pods that this Service represents. Basically, the Service now lets the client decide on how it wants to connect to the Pods.

**In a simplified form, the ClusterIP Service tells the client "Let me take care of routing that request for you." In contrast, a headless Service says "Here is a list of all the Pods that I know about and their IP addresses. Send and route your network requests however you want."**

