# kubernetes-and-ansible
This repository has set of ansible playbooks created to setup a kubernetes cluster fully automated with one master and multiple worker nodes. This will work on physical servers, virtual machines, aws cloud, google cloud or any other cloud servers. This has been tested and verified on Centos 7.3 64 bit operating systems. 

How to use this (Setup Instructions):

1. Make your servers ready (one master node and two worker nodes).
2. Make an entry of your each hosts in /etc/hosts file for name resolution.
3. You can do this with vagrant

      

4. Make sure kubernetes master node and other worker nodes are reachable between each other.
5. Internet connection must be enabled in all nodes, required packages will be downloaded from kubernetes official yum repository.

6. There is a file "hosts" available in "ansible_config_for kubernetes_dep" directory, Just make your entries of your all kubernetes nodes. 
7. Provide your server details in "env_variables" available in "ansible_config_for kubernetes_dep" directory.
8. Deploy the ssh key from master node to other nodes for password less authentication.

   ssh-keygen
   
   Copy the public key to all nodes including your master node and make sure you are able to login into any nodes without password.
   
9. Run "settingup_kubernetes_cluster.yml" playbook to setup all nodes and kubernetes master configuration.

   ansible-playbook settingup_kubernetes_cluster.yml
   
10. Run "join_kubernetes_workers_nodes.yml" playbook to join the worker nodes with kubernetes master node once "settingup_kubernetes_cluster.yml" playbook tasks are completed.

      ansible-playbook join_kubernetes_workers_nodes.yml

11. Verify the configuration from master node.

      kubectl get nodes

What are the files this repository consist

ansible.cfg - Ansible configuration file created locally.

hosts - Ansible Inventory File

env_variables - Main environment variable file where we have to specify based on our environment.

settingup_kubernetes_cluster.yml - Ansible Playbook to perform prerequisites ready, setting up nodes, configure master node.

configure_worker_nodes.yml - Ansible Playbook to join worker nodes with master node.

clear_k8s_setup.yml - Ansible Playbook helps to delete entire configurations from all nodes.

playbooks - Its a directory holds all playbooks.

