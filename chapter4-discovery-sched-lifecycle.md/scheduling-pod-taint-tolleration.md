# Taint one of the worker nodes to repel work.
List out the nodes:
#### kubectl get nodes
Taint the node, replacing <NODE_NAME> with one of the worker node names returned in the previous command:
#### kubectl taint node <NODE_NAME> node-type=prod:NoSchedule
Schedule a pod to the dev environment.
Create the dev-pod.yaml file:
#### vim dev-pod.yaml
Enter the following YAML to specify a pod that will be scheduled to the dev environment:

Save and quit the file by pressing Escape followed by wq!.
Create the pod:
#### kubectl create -f dev-pod.yaml

Create the prod-deployment.yaml file:

#### vim prod-deployment.yaml
Enter the following YAML to specify a pod that will be scheduled to the prod environment:


Create the pod:

#### kubectl create -f prod-deployment.yaml
Verify each pod has been scheduled to the correct environment.
Verify the pods have been scheduled:

#### kubectl get pods -o wide
Scale up the deployment:

#### kubectl scale deployment/prod --replicas=3
Look at our deployment again:
#### kubectl get pods -o wide
We should see that two more pods have been deployed.