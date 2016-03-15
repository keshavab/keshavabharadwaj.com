+++
comments = true
date = 2015-08-17T00:00:00Z
tags = ["kubernetes", "kube-api", "vagrant"]
title = "Kubernetes vagrant - unable to connect to api server"
description = "Making Kubernetes work when it errors out."
+++

When running Kubernetes(K8s) vagrant(sometimes standalone installations), the vagrant up fails with the following error
{{< highlight bash >}}
Validating master
Validating minion-1
.............
Waiting for each minion to be registered with cloud provider
error: couldn't read version from server: Get https://10.245.1.2/api: dial tcp 10.245.1.2:443: connection refused
{{< / highlight >}}

This implies the kubectl client is unable to connect to the kube-api server.
This can happen due to a couple of reasons -

- Prior K8s installation have left config trace in home directory. Delete the contents of *~/.kube* directory, and re provision
  your vagrants.

- The route for the kube-api server could be missing. Add the route
{{< highlight bash >}}
#sudo route -nv add -net 10.245.1 -interface vboxnet0
{{< / highlight >}}
[Note: you should replace it with the subnet vagrant has created for you]
