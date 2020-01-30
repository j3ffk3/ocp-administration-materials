# Persistence Volume

## [Prepare] set up NFS by the following steps
### Run Bash script **setup-nfs**
```
./setup-nfs <dirtory-name>
```
### Set up NFS Server manually
- Step1 Create a export directory
```
mkdir -p /var/export/example
```
- Step2 Change the folder owner and permisson
```
chown nfsnobody:nfsnobody /var/export/example
chmod 700 /var/export/example
```
- Step3 Create a export config file to export directory.
```
vi /etc/exports.d/example.exports
```
- Step4 Config expot file
Paste the following text to export file.
```
/var/export/example *(rw,async,all_squash)
```
- Step5 export 
```
exportfs -a 
```

## [Create PV]
- Step1 Fill up the yaml and save as pv.yaml.
```
apiVersion: v1
kind: PersistentVolume
metadata: 
  name: <PersistentVolume Name>
spec: 
  capacity: 
    storage: <Storage Size>Gi
  accessModes:
  - <Access mode includes ReadWriteOnce/ReadOnlyMany/ReadWriteMany>
  nfs: 
    path: <Export Directory>
    server: <Your NFS Server IP>
 ```
- Step2 Create it by oc command.
```
oc create -f pv.yaml.
```
- Step3 Check PV is created
```
oc get pv
```
