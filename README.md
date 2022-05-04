# Deploy Kubernetes Clusster with Ansible
This repository can help to deploy a kubernetes cluster consisting of one master and 2 worker nodes using ansible. 


Setup Instructions:

1. Make you servers ready (1 master and 2 worker nodes) using vagrant. Please follow below repository for getting those vagrant files server wise.\

     `git clone https://github.com/shoeb816/kubernetes_vagrant.git`

2. After servers are up please entry all hostname with corresponding IP addresses declared in above Vagrantfile /etc/hosts file for name resolution in all hosts.
3. Make sure kubernetes master node and other worker nodes are rechable corresponding to each other.
4. Internet connection must be enabled in all nodes,
5. Make sure 2 worker-servers are accessible from kubernetes master server (implement ssh-keygen)\
     a. In kubernetes master run `ssh-keygen` command and add the `$HOME/.ssh/id_rsa.pub` under `$HOME/.ssh/authorized_keys` file.\
     b. For other 2 worker node server paste the above `id_rsa.pub` in `$HOME/.ssh/authorized_keys`.\
     c. Test from master server whether those worker node are accessible or not.\
     d. If unable to find `$HOME/.ssh` directory, run `ssh-keygen` command once for worker nodes as well. But keep in mind that only need to provide master's id_rsa.pub key in those worker node servers.\
     e. Make sure you are able to login into any nodes without password from master server.\
     
6. Clone this repository into your master node.
   
   `git clone https://github.com/shoeb816/Kubernetes-Ansible.git`

   
   once it is cloned, get into the directory
   
   `cd Kubernetes-Ansible/kubernetes_ansible/`

6. There is a file "hosts" available in "jobs_config" directory, Need to make entry as per your nodes.
7. need to update below parameters as per your host config in `env_variables` file\
   `ad_addr`\
   `cidr_v`
   
9. Run "kubernetes_cluster_setup_with_common_tasks.yml" playbook to setup all nodes and kubernetes master configuration.

   `ansible-playbook kubernetes_cluster_setup_with_common_tasks.yml`
   
10. Run "kubernetes_worker_join_with_master.yml" playbook to join the worker nodes with kubernetes master node once the above tasks completed.

      `ansible-playbook kubernetes_worker_join_with_master.yml`

11. Verify the configuration from master node.

      `kubectl get nodes`

