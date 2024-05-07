
# Mock Exam 2

## Question 1: Run a Pod Using Alpine Image
**Question:**
Run a pod called `alpine-sleeper-cka15-arch` using the alpine image in the default namespace that will sleep for 7200 seconds.

**Answer:**
Create the pod definition using the following YAML configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: alpine-sleeper-cka15-arch
spec:
  containers:
  - name: alpine
    image: alpine
    command: ["/bin/sh", "-c", "sleep 7200"]
```

---

## Question 2: Service Account Permissions
**Question:**
We have created a service account called `red-sa-cka23-arch`, a cluster role called `red-role-cka23-arch` and a cluster role binding called `red-role-binding-cka23-arch`. Identify the permissions of this service account and write down the answer in file `/opt/red-sa-cka23-arch` in format `resource:pods|verbs:get,list` on `student-node`.

**Answer:**
Get the `red-role-cka23-arch` role permissions:

```bash
kubectl get clusterrole red-role-cka23-arch -o json --context cluster1
```

Add data in file as below:

```bash
echo "resource:deployments|verbs:get,list,watch" > /opt/red-sa-cka23-arch
```

---

## Question 3: Troubleshoot Cronjob Scheduling
**Question:**
There is a Cronjob called `orange-cron-cka10-trb` which is supposed to run every two minutes (e.g., 13:02, 13:04, 13:06...14:02, 14:04...and so on). This cron targets the application running inside the `orange-app-cka10-trb` pod to make sure the app is accessible. The application has been exposed internally as a ClusterIP service. However, this cron is not running as per the expected schedule and is not running as intended.

**Answer:**
Troubleshoot the Cronjob scheduling and fix the issues:

```bash
kubectl get cronjob
kubectl logs orange-cron-cka10-trb-xxxx
kubectl edit cronjob orange-cron-cka10-trb
```

Change command:

```bash
curl orange-app-cka10-trb to curl orange-svc-cka10-trb
```

Wait for 2 minutes to run again this cron and it should complete now.

---

## Question 4: Deployment Issue Fix
**Question:**
The `blue-dp-cka09-trb` deployment is having 0 out of 1 pods running. Fix the issue to make sure that pod is up and running.

**Answer:**
List the pods and troubleshoot the deployment:

```bash
kubectl get pod
kubectl logs blue-dp-cka09-trb-xxxx -c init-container
kubectl edit deploy blue-dp-cka09-trb
```

---

... (Continue for other questions similarly) ...

---
