Series of commands for setting up kubernetes on both master and worker node
# On both master and worker nodes
1. Update the package list:

'''
sudo apt-get update -y 
'''
2. Install Docker

'''
sudo apt-get install docker.io -y
'''
 - Install Docker, a conatinerized platform.

3. Restart Docker Service:

'''
sudo service docker restart
'''
  - Restart the docker service to apply any changes made during the installation.
4. Add kubernetes apt-key:

'''
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
'''
  - Fetches the GPG key for the Kubernetes packages and adds it to the keyring.
5. Add Kubernetes repository:
'''
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
'''
  - Adds the Kubernetes repository to the system's package sources.
6. Update the package list again:
'''
sudo apt-get update
'''
  - Updates the package list to include the newly added Kubernetes repository.
7. Install specific versions of Kubeadm, Kubectl, and Kubelet:
'''
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
'''
  - Installs specific versions of Kubeadm, Kubectl, and Kubelet, in this case, version 1.20.0-00.
# Step 2 - On Master node :
8. Initialize the Kubernetes cluster with a specified pod network CIDR:
'''
kubeadm init --pod-network-cidr=192.168.0.0/16
'''
  - Initializes the Kubernetes master node, specifying the pod network CIDR for communication between pods.
# Step 3 - On Master node:
9. Create a directory for kubeconfig and copy the admin.conf file:
'''
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
'''
  - Creates a directory for storing kubeconfig files and copies the admin.conf file to the appropriate location.
10. Set ownership for the kubeconfig file:

'''
sudo chown $(id -u):$(id -g) $HOME/.kube/config
'''
- Ensures that the user has ownership of the kubeconfig file.
# Step 4 - On Master node
11. Apply Calico network plugin:

'''
kubectl apply -f https://docs.projectcalico.org/v3.20/manifests/calico.yaml
'''
  - Applies the Calico network plugin manifest to enable networking within the Kubernetes cluster.
12. Apply Ingress-Nginx controller:

'''
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
'''
  - Applies the Ingress-Nginx controller manifest for handling Ingress resources in the cluster.
These steps collectively set up a Kubernetes cluster with Calico networking and Ingress-Nginx controller on the master node. The specific versions of Kubeadm, Kubectl, and Kubelet are installed, and Docker is used for containerization.





