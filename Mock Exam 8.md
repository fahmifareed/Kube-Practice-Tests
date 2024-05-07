
# Mock Exam 8

## Question 1: DaemonSet Troubleshooting
**Question:**
The DaemonSet `logs-cka26-trb` under `kube-system` namespace in cluster2 is not creating any pod on the controlplane node.

**Answer:**
Inspect and modify the DaemonSet to ensure it schedules pods on the controlplane node by adding the necessary tolerations:

```bash
kubectl --context2 cluster2 get ds logs-cka26-trb -n kube-system
kubectl --context2 cluster2 edit ds logs-cka26-trb -n kube-system
# Add tolerations to allow scheduling on the controlplane node
```

---

## Question 2: ClusterIP Service Creation and Pod IP Listing
**Question:**
Create a ClusterIP service named `service-3421-svcn` in the `spectra-1267` namespace to expose pods `pod-23` and `pod-21`, and list their IPs sorted by IP address.

**Answer:**
Create the service and store the pod names and IP addresses:

```bash
kubectl create service clusterip service-3421-svcn -n spectra-1267 --tcp=8080:80
kubectl get pods -n spectra-1267 -o=custom-columns='POD_NAME:metadata.name,IP_ADDR:status.podIP' --sort-by=.status.podIP
# Store the output
echo "POD_NAME	IP_ADDR" > /root/pod_ips_cka05_svcn
kubectl get pods -n spectra-1267 -o=custom-columns='POD_NAME:metadata.name,IP_ADDR:status.podIP' --sort-by=.status.podIP >> /root/pod_ips_cka05_svcn
```

Ensure the service is working correctly by verifying endpoints and testing connectivity.

---

... (Additional questions would follow a similar structured format) ...

---
