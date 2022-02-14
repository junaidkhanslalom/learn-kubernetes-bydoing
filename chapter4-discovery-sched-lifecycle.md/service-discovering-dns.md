# Create an nginx deployment, and verify it was successful.
Use this command to create an nginx deployment:

#### kubectl run nginx --image=nginx

Use this command to verify deployment was successful:
#### kubectl get deployments
Create a service, and verify the service was successful.
Use this command to create a service:
#### kubectl expose deployment nginx --port 80 --type NodePort
Use this command to verify the service was created:
#### kubectl get services

Create a pod that will allow you to query DNS, and verify it’s been created.
Use the following command to create the busybox pod:
#### kubectl create -f busybox.yaml
Use the following command to verify the pod was created successfully:
#### kubectl get pods


# Perform a DNS query to the service.
Use the following command to query the DNS name of the nginx service:
#### kubectl exec busybox -- nslookup nginx

# Record the DNS name.
Record the name of:

#### [service-name].default.svc.cluster.local