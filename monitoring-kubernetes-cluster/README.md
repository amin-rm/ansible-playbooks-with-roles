# Ansible Playbook for Installing Grafana and Prometheus on Kubernetes

This Ansible playbook installs Grafana and Prometheus on a Kubernetes cluster. The configuration requires a persistent volume to be used by Prometheus. If you do not have a persistent volume already, use the `PV.yaml` playbook to create one and adjust it to the size you want. Additionally, Helm must be installed on the control machine to run this playbook.

## Playbook Details

### Variables

- **kube_config_path**: Path to your kubeconfig file.
- **prometheus_chart_version**: Version of the Prometheus Helm chart to install.
- **grafana_chart_version**: Version of the Grafana Helm chart to install.
- **namespace**: Namespace where Grafana and Prometheus will be installed.
- **prometheus_release_name**: Release name for Prometheus.
- **grafana_release_name**: Release name for Grafana.

### Tasks

1. **Ensure Helm is installed on the control machine**: Checks if Helm is installed. If not found, it installs Helm.
2. **Add Prometheus Helm repository**: Adds the Prometheus Helm repository.
3. **Add Grafana Helm repository**: Adds the Grafana Helm repository.
4. **Update Helm repository to fetch the latest charts**: Updates Helm repositories.
5. **Install Prometheus chart**: Installs Prometheus using Helm.
6. **Install Grafana chart**: Installs Grafana using Helm.

## Usage

### Prerequisites

- Ensure you have a Kubernetes cluster up and running.
- **Helm must be installed on the control machine**.
- Verify that the kubeconfig file is accessible and correctly configured.

### Steps

1. Clone this repository to your local machine.
2. Adjust the variables in the playbook to match your configuration:
    - `kube_config_path`: Update with the path to your kubeconfig file.
    - `prometheus_chart_version`: Specify the desired version of Prometheus.
    - `grafana_chart_version`: Specify the desired version of Grafana.
    - `namespace`: Choose the namespace for deployment (default is `monitoring`).
    - `prometheus_release_name`: Set the release name for Prometheus.
    - `grafana_release_name`: Set the release name for Grafana.
3. If you do not have a persistent volume for Prometheus, use the `PV.yaml` playbook to create one. You can refer to README-PV.md for further instructions :) .
4. Run the playbook:
    ```sh
    ansible-playbook -i inventory.ini install_grafana_prometheus.yml
    ```

### Note

This configuration requires a persistent volume to be used by Prometheus. If you don't have that already, use the `PV.yaml` playbook to create a persistent volume and adjust it with the size you want.