
# Mock Exam 6

## Question 1: Find High Memory Node
**Question:**
Find the node across all clusters that consumes the most memory and store the result to the file `/opt/high_memory_node` in the format `cluster_name,node_name`.

**Answer:**
Check the memory usage across all nodes and clusters, find the node with the highest usage, and save the details:

```bash
kubectl top node --context cluster1 --no-headers | sort -nr -k4 | head -1
kubectl top node --context cluster2 --no-headers | sort -nr -k4 | head -1
kubectl top node --context cluster3 --no-headers | sort -nr -k4 | head -1
kubectl top node --context cluster4 --no-headers | sort -nr -k4 | head -1

echo cluster3,cluster3-controlplane > /opt/high_memory_node
```

---

## Question 4: Fix Pod Resource Limits
**Question:**
The pod `nginx-wl06` deployed on `cluster3-controlplane` used Gebibytes instead of Mebibytes for resource limits, causing it to be stuck in a pending state due to insufficient resources.

**Answer:**
Inspect the pod, correct the resource unit from Gi to Mi, and re-deploy:

```bash
kubectl config use-context cluster3
kubectl describe po nginx-wl06
kubectl edit po nginx-wl06
kubectl replace -f /tmp/kubectl-edit-xxxx.yaml --force
```

---

## Question 5: Create ReplicaSet and DNS Lookup
**Question:**
Create a ReplicaSet named `checker-cka10-svcn` in the `ns-12345-svcn` namespace with specific configurations and perform a DNS lookup of `kubernetes.default`.

**Answer:**
Create the ReplicaSet, ensure pods are running, and perform a DNS lookup:

```bash
kubectl apply -f <ReplicaSet-definition>
kubectl get pods -n ns-12345-svcn
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

Store the DNS lookup output in `/root/dns-output-12345-cka10-svcn`.

---

... (Additional questions would follow a similar structured format) ...

---
