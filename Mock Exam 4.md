
# Mock Exam 4

## Question 1: Troubleshoot Web Deployment
**Question:**
The deployment called `web-dp-cka17-trb` has 0 out of 1 pods up and running. Troubleshoot this issue and fix it. The application runs on port 80 inside the container and is exposed on the node port 30090.

**Answer:**
Troubleshoot the deployment by checking the pods and events:

```bash
kubectl get pod
kubectl get event --field-selector involvedObject.name=<pod-name>
```

**Solution:**
Adjust the PVCs, check logs, and correct deployment errors. Update ports and liveness probes as needed.

---

## Question 2: Network Policy Troubleshooting
**Question:**
Troubleshoot why the `nginx` based pod called `cyan-pod-cka28-trb` is not accessible despite being exposed with a service and governed by a network policy.

**Answer:**
Examine and modify the network policy to ensure correct ports and access controls are specified:

```bash
kubectl edit networkpolicy cyan-np-cka28-trb -n cyan-ns-cka28-trb
```

Ensure the policy allows traffic from `cyan-white-cka28-trb1` pod only.

---

## Question 3: DaemonSet Pod Creation Issue
**Question:**
A DaemonSet called `logs-cka26-trb` is not creating pods on the controlplane node in cluster2.

**Answer:**
Check DaemonSet status and update tolerations to ensure pods are scheduled on all nodes including the controlplane node:

```bash
kubectl --context2 cluster2 get ds logs-cka26-trb -n kube-system
kubectl --context2 cluster2 edit ds logs-cka26-trb -n kube-system
```

Add necessary tolerations.

---

## Question 4: Rollback Deployment
**Question:**
Roll back a failed deployment update in the `dev-wl07` namespace and fix the deployment to use a working image.

**Answer:**
Undo the deployment, check the image, and adjust replica counts:

```bash
kubectl config use-context cluster1
kubectl rollout undo -n dev-wl07 deploy webapp-wl07
kubectl describe deploy -n dev-wl07 webapp-wl07
kubectl scale deploy -n dev-wl07 webapp-wl07 --replicas=5
```

---

... (Additional questions would follow a similar structured format) ...

---
