# etcd-backup-restore

This repo contains a working example of an ETCD backup process using an NFS export instead of a PV/PVC.

Built and tested on Openshift 4.8

Using OC commands and shell:
Create the batch job:
1.  Clone repo and modify vars for your environment / save manifest file.
2.  oc apply -f <filename> on the file that you just saved
## Create a job from the batch job to test
3.  oc create job backup --from=cronjob/openshift-backup
4.  Check job results from the openshift console or the CLI

At time of Disaster:
## Log into master node using SSH key for the core account
1. ssh -i <ssh_key_path> core@<master_node_IP_address>
## use sudo to mount the NFS export containing the ETCD store snapshot
2. sudo mount <nfs_server_address>:<nfs_server_export> /home/core/backup
## follow the rest of the instructions provided in the ETCD disaster recovery
## guide
3.  https://docs.openshift.com/container-platform/4.8/backup_and_restore/control_plane_backup_and_restore/disaster_recovery/scenario-2-restoring-cluster-state.html#dr-restoring-cluster-state
