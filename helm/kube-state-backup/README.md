# Kubernetes state backup as a Cron Job

This chart will schedule [Kubernetes Cron Job](https://kubernetes.io/docs/user-guide/cron-jobs/) to backup Kubernetes state to AWS or GCS cloud storage.

## Install for the first time
### AWS S3
```bash
helm upgrade --install kube-backup kube-state-backup --namespace kube-backup \
    --set schedule="*/50 * * * *",aws.enabled="true" \
    --set aws.accessKeyId="UNF37N93MG374B27",aws.secretAccessKey="AvgjbYndf9TMF8Y3F3J993TMTJ2309T" \
    --set aws.bucket="my-kube-state-backup-bucket",aws.region="eu-west-2"
```

### GCS
```bash
helm upgrade --install kube-backup kube-state-backup --namespace kube-backup \
    --set schedule="*/50 * * * *",gcs.enabled="true",gcs.projectId="project-123" \
    --set gcs.serviceAccountKey="$(cat sa.json | base64)" \
    --set gcs.bucket="my-kube-state-backup",gcs.region="eu"
```

### Run upgrades e.g. for schedule or docker image change
```bash
helm upgrade kube-backup kube-state-backup --reuse-values --set schedule="*/30 * * * *"
helm upgrade kube-backup kube-state-backup --reuse-values --set imageTag="0.1.8"
```
