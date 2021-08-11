---
description: Let's add a second node to your cluster
---

# \(Optional\) Adding a Node

Now it's starting to become fun. If you have another machine you want to add to your cluster, let's do that together. If you don't, that's okay, use what you have for now and you can easily add one later.

On your master node, there is a security token that was generated. You need this token when adding additional nodes so that the master knows this is a legitimate machine you want to add.

1. On your master node, copy the token from \```/var/lib/rancher/k3s/server/node-token```
2. On the node you want to add, run: `curl -sfL https://get.k3s.io | K3S_URL=<ip_of_your_master_node>:6443 K3S_TOKEN=<node> sh -`
3. Go back to your dev machine and `kubectl get nodes` and check that your new node is ready. You should now see two nodes. It might say at first it's `NotReady` but it should become `Ready` in a few minutes. 

