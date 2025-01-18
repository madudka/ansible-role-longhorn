Longhorn
=========

Longhorn Debian installer.

Tested on OS Debian GNU/Linux 12 (bookworm) with kernel Linux 6.1.0-23-amd64.

Install
-------
```
ansible-galaxy install madudka.longhorn
```

Requirements
------------
Min ansible version: 2.16.8

Some tasks of the Ansible role should include the `become: true` parameter to ensure that tasks are executed with elevated privileges.
You can use any method to pass the `ansible_become_user` and `ansible_become_password` parameters.
More: https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_privilege_escalation.html

When using early versions of Ansible you need to install `community.general` collection:

```
ansible-galaxy collection install community.general
```

Example hosts file
----------
The presence of master and worker groups is mandatory.

    [master]
    vm-master-1 ansible_host=192.168.0.101
    vm-master-2 ansible_host=192.168.0.102
    vm-master-3 ansible_host=192.168.0.103
    
    [worker]
    vm-worker-1 ansible_host=192.168.0.111
    vm-worker-2 ansible_host=192.168.0.112
    
    [all:vars]
    ansible_port=22
    ansible_user=username
    ansible_ssh_private_key_file=./id_rsa_ansible 
    ansible_become_password=password

Role Variables
--------------
Default lower priority variables for this role `/defaults/main.yml`:

Here’s the generated markdown table with descriptions of the Ansible role variables:

| Name                             | Description                                            | Value example                                                                            |
| -------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| `helm_install_script_path`       | Path to save the Helm installation script.             | /tmp/get_helm.sh                                                                        |
| `helm_install_url`               | URL to download the Helm installation script.          | https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3                      |
| `kubeconfig_base_path`           | Base directory for kubeconfig files.                   | /home/{{ ansible_user }}/.kube                                                           |
| `kubeconfig_file`                | Path to the kubeconfig file.                           | {{ kubeconfig_base_path }}/config                                                        |
| `k3s_config_path`                | Path to the k3s configuration file.                    | /etc/rancher/k3s/k3s.yaml                                                                |
| `bashrc_path`                    | Path to the user's `.bashrc` file.                     | /home/{{ ansible_user }}/.bashrc                                                         |
| `longhorn_env_check_script_path` | Path to save the Longhorn environment check script.    | /tmp/longhorn_env_check.sh                                                               |
| `longhorn_env_check_url`         | URL to download the Longhorn environment check script. | https://raw.githubusercontent.com/longhorn/longhorn/v1.7.2/scripts/environment_check.sh |
| `longhorn_repo_url`              | URL of the Longhorn Helm repository.                   | https://charts.longhorn.io                                                              |
| `longhorn_chart_version`         | Version of the Longhorn Helm chart to install.         | 1.7.2                                                                                   |

Dependencies
------------

No dependencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: k3s
      roles:
         - { role: madudka.longhorn }

License
-------

GPL-3.0-only

Author Information
------------------

https://madudka.github.io/