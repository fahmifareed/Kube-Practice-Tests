
# Mock Exam 1

## Question 1: High Memory Pod Identification
**Question:**
Find the pod that consumes the most memory and store the result to the file `/opt/high_memory_pod` in the following format: `cluster_name,namespace,pod_name`.

**Answer:**
Check the metrics for all pods across all clusters and identify the highest memory usage:

```bash
kubectl top pods -A --context cluster1 --no-headers | sort -nr -k4 | head -1
kubectl top pods -A --context cluster2 --no-headers | sort -nr -k4 | head -1
kubectl top pods -A --context cluster3 --no-headers | sort -nr -k4 | head -1
kubectl top pods -A --context cluster4 --no-headers | sort -nr -k4 | head -1
```

Identify the highest from the outputs and save the result:

```bash
echo cluster3,default,backend-cka06-arch > /opt/high_memory_pod
```

---

## Question 2: Cronjob Scheduling
**Question:**
A Cronjob called `orange-cron-cka10-trb` is supposed to run every two minutes but is not running as intended. Fix this issue.

**Answer:**
Examine the cron schedule and logs, then adjust the job configuration:

```bash
kubectl get cronjob
kubectl logs orange-cron-cka10-trb-xxxx
kubectl edit cronjob orange-cron-cka10-trb
```

Change the curl command within the cronjob:

```bash
curl orange-app-cka10-trb to curl orange-svc-cka10-trb
```

Wait for the next run to ensure the cronjob completes.

---

## Question 3: Web Application Update
**Question:**
The `frontend-wl04` web application on `cluster1` is outdated and insecure. Update the application to version 2.

**Answer:**
Update the deployment to use the new image version:

```bash
kubectl set image deployment/frontend-wl04 simple-webapp=kodekloud/webapp-color:v2
```

Verify the updated deployment:

```bash
curl http://cluster1-node01:30080
```

---

## Question 4: Troubleshoot Deployment Revision
**Question:**
Inspect the revision 2 of the `trace-wl08` deployment and store the image name used in this revision in the file `/opt/trace-wl08-revision-book.txt`.

**Answer:**
Check the deployment history and extract the image name for revision 2:

```bash
kubectl rollout history deployment trace-wl08 --revision=2
kubectl rollout history deployment trace-wl08 --revision=2 | grep -i image > /opt/trace-wl08-revision-book.txt
```

---

... (Additional questions would follow a similar structured format) ...

---
