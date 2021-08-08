# Setting Up Your Development Machine

## Cluster Access

It's not ideal having to ssh into your server every time you want to do something. To access this cluster remotely, we need to do two things:

1. Copy the cluster access configuration that k3s generated to your development machine.
2. Install the kubernetes control tool \(kubectl\)

#### Install Kubectl

Depending on if your development machine is Linux, Mac or Windows, there are instructions to install it [here](https://kubernetes.io/docs/tasks/tools/#kubectl). 

#### Copy your cluster config

From the doc:

> Copy `/etc/rancher/k3s/k3s.yaml` on your machine located outside the cluster as `~/.kube/config`. Then replace “localhost” with the IP or name of your K3s server. `kubectl` can now manage your K3s cluster.

Now let's run that same command we did before to see if the node is working:

```text
jevin@laptop:~ $ kubectl get nodes
NAME   STATUS   ROLES                  AGE   VERSION
cpi6   Ready    control-plane,master   51s   v1.21.3+k3s1
```

Winner! So much nicer than sshing to the machine every time

### Starting Your Infrastructure as Code Directory

❗**Concept: Kubernetes Objects** What is really awesome about Kubernetes is that you can code up a desired state that you want it to do, then "apply" those configuration files \(call Kubernetes Objects\) and it will try to do set up that state \(called ". As your cluster grows over time, you want to keep your configuration in static files so you can refer back, make changes as needed, and use them as references for other things you want to deploy. 

Since the configuration files that we ask Kubernetes to "apply" are just yaml files, you can organize them however you like. Personally, I like to group them by the purpose for each deployment. It looks like this \(I didn't include everything to not clutter everything\)

```text
todo.txt
README.md
shared/
smarthome/
├─ home-assistant/
├─ (other stuff)/
rss-reader/
media/
├─ jellyfin/
├─ (other stuff)/
network/
├─ healthcheck/
├─ adguard/

```

Each folder contains a few Kubernetes Object files. Let's start simple and create a new directory somewhere on your machine:

```text
$ mkdir homelab-code
$ cd homelab-code
```

Let's also create a git repo for that dir:

```text
$ git init .
```

Let's get rolling

#### References

* Official [k3s doc on this process](https://rancher.com/docs/k3s/latest/en/cluster-access/)
* [Kubernetes Objects ](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)

