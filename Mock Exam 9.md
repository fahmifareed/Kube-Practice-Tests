
# Mock Exam 9

## Question 1: Log Inspection and Filtering
**Question:**
Inspect the logs of a pod named `beta-pod-cka01-arch` in the `beta-cka01-arch` namespace and save all logs starting with the string ERROR in the file `/root/beta-pod-cka01-arch_errors`.

**Answer:**
Filter the logs to capture only lines that start with ERROR and save them to a file:

```bash
kubectl logs -n beta-cka01-arch beta-pod-cka01-arch | grep '^ERROR' > /root/beta-pod-cka01-arch_errors
```

---

## Question 2: Persistent Volume and Claim Setup
**Question:**
Create a persistent volume `coconut-pv-cka01-str` and a matching persistent volume claim `coconut-pvc-cka01-str` using the `coconut-stc-cka01-str` storage class.

**Answer:**
Define and apply a YAML configuration for both the persistent volume and the claim:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: coconut-pv-cka01-str
  labels:
    storage-tier: gold
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: /opt/coconut-stc-cka01-str
  storageClassName: coconut-stc-cka01-str
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - cluster1-node01
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: coconut-pvc-cka01-str
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 50Mi
  storageClassName: coconut-stc-cka01-str
  selector:
    matchLabels:
      storage-tier: gold
```

Apply the configuration to set up the storage and claim.

---

## Question 3: DNS Lookup from a Pod
**Question:**
Create a pod `tester-cka02-svcn` in the `dev-cka02-svcn` namespace and perform a DNS lookup for `kubernetes.default`.

**Answer:**
Create the pod and execute a DNS lookup command to store the output:

```bash
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: tester-cka02-svcn
  namespace: dev-cka02-svcn
spec:
  containers:
  - name: tester-cka02-svcn
    image: registry.k8s.io/e2e-test-images/jessie-dnsutils:1.3
    command:
      - sleep
      - "3600"
  restartPolicy: Always
EOF

kubectl exec -n dev-cka02-svcn -i -t tester-cka02-svcn -- nslookup kubernetes.default > /root/dns_output
```

---

## Question 4: LoadBalancer Service Creation
**Question:**
Create a LoadBalancer service `wear-service-cka09-svcn` to expose the `webapp-wear-cka09-svcn` deployment in the `app-space` namespace.

**Answer:**
Expose the deployment as a LoadBalancer service:

```bash
kubectl -n app-space expose deployment webapp-wear-cka09-svcn --type=LoadBalancer --name=wear-service-cka09-svcn --port=8080
```

Verify the service is accessible through the assigned external IP.

---

... (Additional questions would follow a similar structured format) ...

---
