# Install a Three Node Cluster
## Get the Docker gpg, and add it to your repository.
In all three terminals, run the following command to get the Docker gpg key:
#### curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Add to repository: 
#### sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

## Get the Kubernetes gpg key, and add it to your repository.
#### curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

#### cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
#### deb https://apt.kubernetes.io/ kubernetes-xenial main
#### EOF

#### sudo apt update

In all three terminals, run the following command to install Docker, kubelet, kubeadm, and kubectl:

#### sudo apt install -y docker-ce=5:19.03.10~3-0~ubuntu-focal kubelet=1.18.5-00 kubeadm=1.18.5-00 kubectl=1.18.5-00

# Create a Deployment
#### kubectl create deployment nginx --image=nginx
# Expose Port 80 on the Pod
#### kubectl port-forward <pod_name> 8081:80
#### curl -I http://127.0.0.1:8081
# Get the NGINX version running on the pod
#### kubectl exec -it <pod_name> -- nginx -v
# Create a service, and verify connectivity on the node port

#### kubectl expose deployment nginx --port 80 --type NodePort
#### kubectl get services
#### kubectl get po -o wide
#### curl -I YOUR_NODE:YOUR_PORT