Use the following command to list the pods in the default namespace:
#### kubectl get pods

Use the following command to find the IP address of the API server:

#### kubectl get pods --all-namespaces -o wide

Use the following command to list the labels for all nodes
##### kubectl get no --show-labels

Create a file named pod.yaml (vi pod.yaml) and paste in the following:

#### apiVersion: v1
#### kind: Pod
#### metadata:
####  name: nginx
#### spec:
####  containers:
####    - name: nginx
####      image: nginx
####  nodeSelector:
####    disk: ssd

Apply the YAML to the Kubernetes cluster with the following command:

#### kubectl apply -f pod.yaml

Verify that pod is on correct node with the following command
#### kubectl get po -o wide
