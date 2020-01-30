# A Persistence volume claim example

## rwx-pvc.yaml shows the following highlights
- A pvc names **example-pvc**
- Access mode is **ReadWriteMany**
- Request **5Gi** storage

## How to claim it by oc command?
```
oc set volume dc/<DeploymentConfig> \
--add --overwrite --name=<volume name in DeploymentConfig> -t pvc \
--claim-name=example-pvc \
--claim-size=5Gi \
--claim-mode='ReadWriteMany'

```
