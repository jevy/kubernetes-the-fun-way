---
description: Let's start with installing k8s onto your first machine
---

# Setting up your Master Node

There are a number of "distributions" of Kubernetes that exist \(minikube, microk8s, k3s etc\) and they all have their use cases. A distribution is basically a set of smart defaults and configuration settings. You COULD build everything from scratch \(like in [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)\) but that's now why you're here. You want to just get started. I chose [k3s](https://k3s.io/) and so far, I've been happy with that. Let's use that.

One your fresh linux machine, let's get going. It's super easy to get going:

```text
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
```

The above is slight variation on the default install you see on the k3s site, the `--write-kubeconfig-mode 644` simply makes the configuration files with the correct permissions, so you can run kubectl commands right away. I have no idea why this is not part of the defaults.

When that finishes, type `kubectl get nodes` and you should see the node with Ready in the STATUS column. If you do, congrats! You have your first cluster up and running.

```text
pi@cpi6:~ $ kubectl get nodes
NAME   STATUS   ROLES                  AGE   VERSION
cpi6   Ready    control-plane,master   51s   v1.21.3+k3s1
```

❗ Concept: Roles - Here you can see that your new Node has two roles, **control-plane** and **master.**

**Control Plane -** From the Kubernetes doc:

> The control plane's components make global decisions about the cluster \(for example, scheduling\), as well as detecting and responding to cluster events \(for example, starting up a new [pod](https://kubernetes.io/docs/concepts/workloads/pods/) when a deployment's `replicas` field is unsatisfied\). -- [Kubernetes doc](https://kubernetes.io/docs/concepts/overview/components/#control-plane-components)

**Master** - Runs the database of the current start of the cluster

### Uninstalling \(If you ever need to do this\)

If you ever mess things up, it's actually really easy to undo everything. Just run:

```text
/usr/local/bin/k3s-uninstall.sh
```



