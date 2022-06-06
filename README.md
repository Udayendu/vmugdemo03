# Changelog
- Kubernetes Cluster deployment using Ansible & Jenkins
- This deployment will setup a Kubernetes Cluster of:
  - Master Node: 1
  - Worker Nodes: 3



![kubernetes](https://user-images.githubusercontent.com/1809177/172183297-9c049f19-308b-40df-a860-8d29277f28a0.png)




## [v1.0] - 05-06-2022 (dd-mm-yyyy)

### Added
  - Ansible Roles for:
    - VM Management:
      - vmdeploy
      - gocustom
      - vmdelete
    - VM Snapshot Management:
      - vmsnapshot
      - vmsnapshotrevert
      - vmsnapshotremove
    - Kubernetes Cluster Management:
      - mastersetup
      - nodesetup
      - nodelabel

### Software support
  - ansible: 5.2.0
  - ansible-core: 2.12.1
  - pyvmomi: 7.0.3
  - vSphere-Automation-SDK: 1.71.0

### Kubernetes Packages:
  - docker: 1.13.1
  - kubelet: 1.23.7
  - kubeadm: 1.23.7
  - kubectl: 1.23.7

## Deployment Guide:

### VM Management
- To deploy the linux server, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "deploy"

- To do the guest os customization, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "oscustom"

- To delete the linux server use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "delete"

### VM Snapshot Management
- To take the vm snapshots, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshot"

- To revert the vm snapshot, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshotrevert"

- To remove the vm snapshot, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshotremove"

### Kubernetes Cluster Management
- To deploy & configure the kubernetes master, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "mastersetup"

- To deploy & configure the kubernetes worker nodes, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "nodesetup"

- To label the kubernetes worker nodes, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "nodelabel"
