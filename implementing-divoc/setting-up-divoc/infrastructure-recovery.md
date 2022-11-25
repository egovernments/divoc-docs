# Infrastructure Recovery

## Kubernetes&#x20;

### Recovering control plane&#x20;

* To recover from broken nodes in the control plane, use the                                      "[**recover-control-plane.yml**](https://github.com/egovernments/divoc-installer/blob/master/ansible-cookbooks/kubernetes/recover-control-plane.yml)" playbook.
* Back **** up what you can.
* Provision new nodes to replace the broken ones.
* Place the surviving nodes of the control plane first in the "etcd" and "kube\_control\_plane" groups.
* Add the new nodes below the surviving control plane nodes in the "etcd" and "kube\_control\_plane" groups.

### Examples of what broken means in this context:

* One or more bare metal node(s) suffer from unrecoverable hardware failure.&#x20;
* One or more node(s) fail during patching or upgrading.&#x20;
* Etcd database corruption.&#x20;
* Other node-related failures that leave your control plane degraded or nonfunctional.
* **Note:** You need at least one functional control plane node to be able to recover using this method. If all control planes go down, there is no scope of recovery, and you will have to reinstall Kubernetes. Typically, even if the control plane goes down, the application still functions. Kubernetes functions like scaling, creating new pods, upgrading deployments, etc. will not work. The application, as is available, will continue to function.

### Runbook

* Move any broken etcd nodes into the "broken\_etcd" group, make sure the "etcd\_member\_name" variable is set.
* Move any broken control plane nodes into the "broken\_kube\_control\_plane" group.
* Run the playbook with **--limit etcd,kube\_control\_plane**, and increase the number of etdc retries by setting **-e etcd\_retries=10** or something even larger. The amount of retries required is difficult to predict.
* Once you are done, you should have a fully working control plane again.

### **Recover from the last quorum**

* The playbook attempts to figure out if the etcd quorum is intact. If the quorum is lost, it will attempt to take a snapshot from the first node in the "etcd" group and restore from that.&#x20;
* To restore from an alternate snapshot, set the path to that snapshot in the "etcd\_snapshot" variable: **-e etcd\_snapshot=/tmp/etcd\_snapshot**.

### **Adding or replacing a node**

#### Removal of first kube\_control\_plane and etcd-master&#x20;

Currently, you cannot remove the first node in your kube\_control\_plane and etcd-master list. If you still want to remove this node, you have to do the following:

1. Modify the order of your control plane list by pushing your first entry to any other position, such as if you want to remove node-1 of the following example:

{% hint style="info" %}
**children:**\
&#x20;   **kube\_control\_plane:**\
&#x20;     **hosts:**\
&#x20;       **node-1:**\
&#x20;       **node-2:**\
&#x20;       **node-3:**\
&#x20;   **kube\_node:**\
&#x20;     **hosts:**\
&#x20;       **node-1:**\
&#x20;       **node-2:**\
&#x20;       **node-3:**\
&#x20;   **etcd:**\
&#x20;     **hosts:**\
&#x20;       **node-1:**\
&#x20;       **node-2:**\
&#x20;       **node-3:**
{% endhint %}

2\. Run **upgrade-cluster.yml or cluster.yml.** After this, you are good to go on with the removal.

### **Adding or replacing a worker node**

1. Add a new node to the inventory.
2. Run **scale.yml**. You can use **--limit=NODE\_NAME** to limit Kubespray to avoid disturbing other nodes in the cluster. Before using **--limit,** run playbook **facts.yml** without the limit to refresh facts cache for all nodes.
3. Remove an old node with **remove-node.yml.** With the old node still in the inventory, run **remove-node.yml**. You need to pass **-e node=NODE\_NAME** to the playbook to limit the execution to the node being removed. If the node you want to remove is not online, you should add **reset\_nodes=false and allow\_ungraceful\_removal=true** to your extra-vars: **-e node=NODE\_NAME -e reset\_nodes=false -e allow\_ungraceful\_removal=true**. Use this flag even when you remove other types of nodes like a control plane or etcd nodes.
4. Remove node from the inventory.

### **Adding or replacing a control plane node**

1. Append the new host to the inventory and run **cluster.yml**. You cannot use **scale.yml** for that.
2. In all hosts, restart **nginx-proxy pod**. This pod is a local proxy for the apiserver. Kubespray will update its static config, but it needs to be restarted to reload:

{% hint style="info" %}
docker ps | grep k8s\_nginx-proxy\_nginx-proxy | awk '{print $1}' | xargs docker restart
{% endhint %}

&#x20;3\. With the old node still in the inventory, run **remove-node.yml**. You need to pass **-e        node=NODE\_NAME** to the playbook to limit the execution to the node being removed. If the node you want to remove is not online, you should add **reset\_nodes=false** and **allow\_ungraceful\_removal=true** to your extra-vars.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
