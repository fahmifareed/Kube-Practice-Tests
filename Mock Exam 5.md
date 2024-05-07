
# Mock Exam 5

## Question 1: Elastic App Pod with Sidecar
**Question:**
A pod called `elastic-app-cka02-arch` is running in the default namespace. The YAML file for this pod is at `/root/elastic-app-cka02-arch.yaml`. The application container in this pod writes logs to `/var/log/elastic-app.log`. Recreate this pod with an additional sidecar container using the `busybox` image to print logs to STDOUT by running `tail -f /var/log/elastic-app.log`.

**Answer:**
Update the YAML file to include the sidecar container that tails the log file:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: elastic-app-cka02-arch
spec:
  containers:
  - name: elastic-app
    image: busybox:1.28
    args:
    - /bin/sh
    - -c
    - >
      mkdir /var/log; 
      i=0;
      while true;
      do
        echo "$(date) INFO $i" >> /var/log/elastic-app.log;
        i=$((i+1));
        sleep 1;
      done
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  - name: sidecar
    image: busybox:1.28
    args: [/bin/sh, -c, 'tail -f /var/log/elastic-app.log']
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  volumes:
  - name: varlog
    emptyDir: {}
```

---

## Question 2: Troubleshoot PVC Issue
**Question:**
There is an existing PV `orange-pv-cka13-trb` and a PVC `orange-pvc-cka13-trb` that is stuck in a Pending state.

**Answer:**
List the PVC to check its status and adjust the storage request:

```bash
kubectl get pvc
kubectl edit pvc orange-pvc-cka13-trb
```

Update the storage request from 150Mi to 100Mi, and then reapply the PVC configuration.

---

## Question 3: Network Policy Troubleshooting
**Question:**
The `nginx` based pod `cyan-pod-cka28-trb` in `cyan-ns-cka28-trb` namespace should be accessible only from `cyan-white-cka28-trb1` pod, but it's not accessible from anywhere.

**Answer:**
Edit the network policy to ensure proper port and pod selector settings:

```bash
kubectl edit networkpolicy cyan-np-cka28-trb -n cyan-ns-cka28-trb
```

Adjust the policy to allow ingress from `cyan-white-cka28-trb1` and ensure the service is accessible using the `curl` utility from within allowed pods.

---

... (Additional questions would follow a similar structured format) ...

---
