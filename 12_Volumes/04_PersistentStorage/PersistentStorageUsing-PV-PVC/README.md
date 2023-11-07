# Persistent Storage

Ideally, a developer deploying their apps on Kubernetes should never have to
know what kind of storage technology is used underneath, the same way they don’t
have to know what type of physical servers are being used to run their pods. Infrastructure-related dealings should be the sole domain of the cluster administrator.

When a developer needs a certain amount of persistent storage for their applica-
tion, they can request it from Kubernetes, the same way they can request CPU, mem-
ory, and other resources when creating a pod. The system administrator can configure
the cluster so it can give the apps what they request.
To enable apps to request storage in a Kubernetes cluster without having to deal with infrastructure specifics, two new resources were introduced. They are PersistentVolumes and PersistentVolumeClaims.

Instead of the developer adding a technology-specific volume to their pod, it’s the
cluster administrator who sets up the underlying storage and then registers it in
Kubernetes by creating a PersistentVolume resource through the Kubernetes API
server. When creating the PersistentVolume, the admin specifies its size and the access modes it supports.

When a cluster user needs to use persistent storage in one of their pods, they first
create a PersistentVolumeClaim manifest, specifying the minimum size and the access
mode they require. The user then submits the PersistentVolumeClaim manifest to the
Kubernetes API server, and Kubernetes finds the appropriate PersistentVolume and
binds the volume to the claim.

The PersistentVolumeClaim can then be used as one of the volumes inside a pod.
Other users cannot use the same PersistentVolume until it has been released by deleting the bound PersistentVolumeClaim.


*NOTE*

    - PersistentVolumes don’t belong to any namespace. They’re cluster-level resources like nodes.

    - PersistentVolumeClaims can only be created in a specific namespace. They can then only be used by pods in the same namespace.
