# Ansible Playbook: Create Persistent Volume for Prometheus

This Ansible playbook creates a persistent volume (PV) for Prometheus in a Kubernetes cluster.

## Playbook Details

- **Name**: Create Persistent Volume for Prometheus
- **Hosts**: localhost
- **Connection**: local
- **Gather Facts**: false

### Variables

- **kube_config_path**: Path to your kubeconfig file.
- **pv_name**: Name of the persistent volume to be created.
- **storage_size**: Size of the persistent volume (e.g., "10Gi").
- **host_path**: Path on the host where the volume will be mounted.

### Tasks

1. **Ensure kubectl is installed on the control machine**: Checks if kubectl is installed.
2. **Create PV definition from template**: Uses the Jinja2 template `PV.j2` to generate the PV definition.
3. **Apply Persistent Volume using kubectl**: Applies the PV definition to the Kubernetes cluster using kubectl.
4. **Clean up PV definition file**: Removes the temporary PV definition file after applying it.

## Usage

1. Ensure Ansible is installed on your control machine.
2. Modify the playbook variables (`kube_config_path`, `pv_name`, `storage_size`, `host_path`) to match your environment.
3. Run the playbook:
   ```sh
   ansible-playbook -i inventory.ini create_pv.yml
