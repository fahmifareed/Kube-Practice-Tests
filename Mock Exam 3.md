
# Mock Exam 3

## Question 1: etcd Backup Restoration
**Question:**
An etcd backup is stored at `/opt/cluster1_backup_to_restore.db` on the cluster1-controlplane node. Restore it using `/root/default.etcd` as the `--data-dir`.

**Answer:**
SSH into the cluster1-controlplane node and restore the backup:

```bash
ssh root@cluster1-controlplane
cd /tmp
export RELEASE=$(curl -s https://api.github.com/repos/etcd-io/etcd/releases/latest | grep tag_name | cut -d '"' -f 4)
wget https://github.com/etcd-io/etcd/releases/download/${RELEASE}/etcd-${RELEASE}-linux-amd64.tar.gz
tar xvf etcd-${RELEASE}-linux-amd64.tar.gz; cd etcd-${RELEASE}-linux-amd64
mv etcd etcdctl /usr/local/bin/
etcdctl snapshot restore --data-dir /root/default.etcd /opt/cluster1_backup_to_restore.db
```

---

## Question 2: Service Account Permission Update
**Question:**
Update the permissions of the service account called `green-sa-cka22-arch` so it can only get all the namespaces in cluster1.

**Answer:**
Edit the `green-role-cka22-arch` to update permissions:

```bash
kubectl edit clusterrole green-role-cka22-arch --context cluster1
```

Add the following permissions:

```yaml
- apiGroups: ["*"]
  resources: ["namespaces"]
  verbs: ["get"]
```

Verify the updated permissions:

```bash
kubectl auth can-i get namespaces --as=system:serviceaccount:default:green-sa-cka22-arch
```

---

## Question 3: Install etcd Utility on Cluster2-Controlplane
**Question:**
Install etcd utility on cluster2-controlplane node for taking/restoring etcd backups.

**Answer:**
SSH into the cluster2-controlplane node and install etcd:

```bash
ssh root@cluster2-controlplane
cd /tmp
export RELEASE=$(curl -s https://api.github.com/repos/etcd-io/etcd/releases/latest | grep tag_name | cut -d '"' -f 4)
wget https://github.com/etcd-io/etcd/releases/download/${RELEASE}/etcd-${RELEASE}-linux-amd64.tar.gz
tar xvf etcd-${RELEASE}-linux-amd64.tar.gz; cd etcd-${RELEASE}-linux-amd64
mv etcd etcdctl /usr/local/bin/
```

---

... (Additional questions would follow a similar structured format) ...

---
