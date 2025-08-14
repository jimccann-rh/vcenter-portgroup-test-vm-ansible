## vCenter Portgroup Deployment Playbook

### Files
- `ansible/vcenter_deploy_from_portgroups.yml`
- `ansible/portgroups.txt`

### How it works
- Reads vCenter connection and placement from environment variables.
- Reads port groups from a file (one per line).

### For each port group
- Deploys a VM from content library template "IPtest".
- Places it in the specified datacenter/cluster/folder and `vsanDatastore`.
- Connects its NIC to the port group.
- Powers it on.

### Environment variables to set
- `VCENTER_SERVER`
- `VCENTER_USERNAME`
- `VCENTER_PASSWORD`
- `VCENTER_DATACENTER`
- `VCENTER_CLUSTER`
- `VCENTER_DATASTORE` (defaults to `vsanDatastore`)
- `VCENTER_CONTENT_LIBRARY` (optional if needed to disambiguate)
- `VCENTER_CL_TEMPLATE` (defaults to `IPtest`)
- `PORTGROUP_FILE` (defaults to `ansible/portgroups.txt`)
- `VCENTER_VALIDATE_CERTS` (default `false`)

# To enable and use defaults: export PRECLEAN_DELETE_VMS=true and run the play.
# To change delay: export PRECLEAN_PAUSE_SECONDS=180.

### Run
```bash
ansible-galaxy collection install community.vmware
ansible-galaxy collection install vmware.vmware
pip install pyvmomi
ansible-playbook ansible/vcenter_deploy_from_portgroups.yml
```

