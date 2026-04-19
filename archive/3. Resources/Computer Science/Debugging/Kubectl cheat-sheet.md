l```shell
kubectl label namespace buzz optimize-resources-
```
```shell
kubectl get po -n sre | grep sre-api-app-sit | awk '{print $1 }'|xargs kubectl delete -n sre po
```
```shell
kubectl label namespace buzz optimize-resources=enabled
```
```Shell
kubectl label namespace accreditation optimize-resources=enabled
```
```Shell
kubectl delete jobs --field-selector status.successful=0
```
```Shell
kubectl get pods -A [--sort-by=.metadata.creationTimestamp]()
```
```Shell
kubectl get hpa -A --sort-by=.status.currentReplicas
```
```Shell
kubectl get po -o custom-columns="Name:metadata.name,CPU-limit:spec.containers[*].resources.requests.cpu" -A
```
```Shell
 kubectl get deploy -A | awk '{print $1,$2}' | awk '{ system("kubectl rollout restart deploy/"$2" -n "$1"")}'
```

```Shell
kubectl get node -l karpenter.sh/provisioner-name
# Extract the instance ID (replace <node-name> with a node name from the above listing)
INSTANCE_ID=$(kubectl get node <node-name> -ojson | jq -r ".spec.providerID" | cut -d \/ -f5)
# Connect to the instance
aws ssm start-session --target $INSTANCE_ID
# Check Kubelet logsca
sudo journalctl -u kubelet


kubectl get nodes  -o json | jq ".items[].metadata.labels" | grep beta.kubernetes.io/instance-type | sort | uniq -c

```



Read “A life of Packet in Amazon EKS“ by Hemant Rawat on Medium: https://hemantra.medium.com/a-life-of-packet-in-amazon-eks-12b496f178ab