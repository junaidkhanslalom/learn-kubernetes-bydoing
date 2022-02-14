# Create and Roll Out Version 1 of the Application, and Verify a Successful Deployment
Create and open the kubeserve-deployment.yaml to create your deployment:
#### vim kubeserve-deployment.yaml

Create the deployment:
#### kubectl apply -f kubeserve-deployment.yaml
Verify the deployment was successful:
#### kubectl rollout status deployments kubeserve
You should see that the deployment was successfully rolled out.
Verify the app is at the correct version:
#### kubectl describe deployment kubeserve
You should see that the image is version 1.

# Scale Up the Application to Create High Availability
Check for pods:
#### kubectl get pods
You should see 3 pods.

Scale up your application to 5 replicas:
#### kubectl scale deployment kubeserve --replicas=5
Verify the additional replicas have been created:
#### kubectl get pods
You should now see 5 pods.

Create a Service So Users Can Access the Application
Create a service for your deployment:

#### kubectl expose deployment kubeserve --port 80 --target-port 80 --type NodePort
Verify the service is present:
#### kubectl get services
Copy the Cluster-IP of the NodePort service from this screen. You will need it for the next objective.

Perform a Rolling Update to Version 2 of the Application, and Verify Its Success
Start another terminal session logged in to the same Kube Master server. There, use the following curl loop command to see the version change as you perform the rolling update. Replace <ip-address-of-the-service> with the Cluster-IP of the NodePort service you copied before:
#### while true; do curl http://<ip-address-of-the-service>; done
Perform the update in the original terminal session (while the curl loop is running in the second terminal session):
#### kubectl set image deployments/kubeserve app=linuxacademycontent/kubeserve:v2 --v 6
After you run this command, if you view the second terminal session, you should see v2 of the pod displayed in the output. Press CTRL+C to stop.

In the first terminal, view the additional ReplicaSet created during the update:
#### kubectl get replicasets
You should see 2 replicasets.
Verify all pods are up and running:
#### kubectl get pods
You should still see 5 pod replicas.
View the rollout history:
#### kubectl rollout history deployment kubeserve
You should see 2 rollouts.