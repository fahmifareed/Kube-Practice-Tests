
# Mock Exam 7

## Question 1: Create Service Account and Role Binding
**Question:**
Create a service account called `pink-sa-cka24-arch`, a cluster role `pink-role-cka24-arch` with full permissions on all resources in the core API group under the default namespace in cluster1, and a cluster role binding `pink-role-binding-cka24-arch`.

**Answer:**
Execute the following commands to create the service account, cluster role, and role binding:

```bash
kubectl --context cluster1 create serviceaccount pink-sa-cka24-arch
kubectl --context cluster1 create clusterrole pink-role-cka24-arch --resource=* --verb=*
kubectl --context cluster1 create clusterrolebinding pink-role-binding-cka24-arch --clusterrole=pink-role-cka24-arch --serviceaccount=default:pink-sa-cka24-arch
```

---

## Question 2: Troubleshoot Network Policy
**Question:**
The nginx based app `cyan-pod-cka28-trb` in the `cyan-ns-cka28-trb` namespace is supposed to be accessible only from the `cyan-white-cka28-trb1` pod but is not accessible from anywhere.

**Answer:**
Update the network policy to correct the egress and ingress settings:

```bash
kubectl edit networkpolicy cyan-np-cka28-trb -n cyan-ns-cka28-trb
# Change the port and ensure proper selectors are set for the pods
```

Ensure the app is accessible by the correct pod and not by others.

---

## Question 3: ETCD Backup
**Question:**
Take a snapshot of the ETCD database on the `cluster4-controlplane` node using the etcdctl utility.

**Answer:**
SSH into the controlplane and execute the etcd backup command:

```bash
ssh cluster4-controlplane
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/etcd-boot-cka18-trb.db
```

---

## Question 4: Elastic App with Sidecar Container
**Question:**
Recreate the `elastic-app-cka02-arch` pod with a sidecar container that tails `/var/log/elastic-app.log`.

**Answer:**
Modify the pod definition to include the sidecar container:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: elastic-app-cka02-arch
spec:
  containers:
  - name: elastic-app
    image: busybox:1.28
    args: ["/bin/sh", "-c", "while true; do echo "$(date) INFO $i" >> /var/log/elastic-app.log; i=$((i+1)); sleep 1; done"]
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  - name: sidecar
    image: busybox:1.28
    args: ["/bin/sh", "-c", "tail -f /var/log/elastic-app.log"]
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  volumes:
  - name: varlog
    emptyDir: {}
```

Recreate the pod using the updated YAML file.

---

... (Additional questions would follow a similar structured format) ...

---
