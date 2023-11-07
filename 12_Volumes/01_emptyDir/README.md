# Volume: emptyDir
Volume emptyDir starts out as an empty directory. The app running inside the pod can then write any files it needs to it. An emptyDir volume is first created when a Pod is assigned to a Node and initially its empty. Because the volume’s lifetime is tied to that of the pod, the volume’s contents are lost when the pod is deleted.

An emptyDir volume is especially useful for sharing files between containers
running in the same pod. But it can also be used by a single container for when a container needs to write data to disk temporarily, such as when performing a sort
operation on a large dataset, which can’t fit into the available memory.

The emptyDir we have used as the volume was created on the actual disk of the worker
node hosting your pod, so its performance depends on the type of the node’s disks.
But you can tell Kubernetes to create the emptyDir on a tmpfs filesystem (in memory
instead of on disk).

To do this, set the emptyDir’s medium to Memory like this:

```bash
volumes:
    - name: html
      emptyDir:
        medium: Memory
```
An emptyDir volume is the simplest type of volume, but other types build upon it.
After the empty directory is created, they populate it with data. One such volume type is the gitRepo volume type.