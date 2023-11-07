# Kubernetes Volumes

Each container in a pod has its own isolated filesystem, because the filesystem comes from the container’s image.

In certain scenarios you want the new container to continue where the last one fin-
ished, such as when restarting a process on a physical machine. You may not need (or
want) the whole filesystem to be persisted, but you do want to preserve the directories
that hold actual data.

*Kubernetes provides this by defining storage volumes.*

Kubernetes volumes are a component of a pod and are thus defined in the pod’s spec-
ification—much like containers.

A volume is bound to the lifecycle of a pod and will stay in existence only while the
pod exists, but depending on the volume type, the volume’s files may remain intact
even after the pod and volume disappear, and can later be mounted into a new volume.

Here’s a list of
several of the available volume types:

- emptyDir — A simple empty directory used for storing transient data.

- hostPath — Used for mounting directories from the worker node’s filesystem
into the pod.

- gitRepo — A volume initialized by checking out the contents of a Git repository.

- nfs — An NFS share mounted into the pod.

- gcePersistentDisk (Google Compute Engine Persistent Disk), awsElastic-
BlockStore (Amazon Web Services Elastic Block Store Volume), azureDisk
(Microsoft Azure Disk Volume)—Used for mounting cloud provider-specific
storage.

- cinder, cephfs, iscsi, flocker, glusterfs, quobyte, rbd, flexVolume, vsphere-
Volume, photonPersistentDisk, scaleIO — Used for mounting other types of
network storage.

- configMap, secret, downwardAPI — Special types of volumes used to expose cer-
tain Kubernetes resources and cluster information to the pod.

- persistentVolumeClaim — A way to use a pre- or dynamically provisioned persistent storage.
