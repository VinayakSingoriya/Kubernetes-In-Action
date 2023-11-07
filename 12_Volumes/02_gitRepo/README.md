# Volume: gitRepo

A gitRepo volume is basically an emptyDir volume that gets populated by cloning a
Git repository and checking out a specific revision when the pod is starting up (but
before its containers are created).

NOTE: After the gitRepo volume is created, it isn’t kept in sync with the repo
it’s referencing. The files in the volume will not be updated when you push
additional commits to the Git repository. However, if your pod is managed by
a ReplicationController, deleting the pod will result in a new pod being cre-
ated and this new pod’s volume will then contain the latest commits.

For example, you can use a Git repository to store static HTML files of your website
and create a pod containing a web server container and a gitRepo volume. Every time
the pod is created, it pulls the latest version of your website and starts serving it.Only drawback to this is that you need to delete the pod every time you push changes to the gitRepo and want to start serving the new version of the website.