1. Create the deployment with four replicas:

    #### cat << EOF | kubectl apply -f -
    #### apiVersion: apps/v1
    #### kind: Deployment
    #### metadata:
    ####  name: store-products
    ####  labels:
    ####    app: store-products
    #### spec:
    ####  replicas: 4
    ####  selector:
    ####    matchLabels:
    ####      app: store-products
    ####  template:
    ####    metadata:
    ####      labels:
    ####        app: store-products
    ####    spec:
    ####      containers:
    ####      - name: store-products
    ####        image: linuxacademycontent/store-products:1.0.0
    ####        ports:
    ####        - containerPort: 80
    #### EOF


2. Create a service for the store-products pods:
#### cat << EOF | kubectl apply -f -
#### kind: Service
#### apiVersion: v1
#### metadata:
####  name: store-products
#### spec:
####  selector:
####    app: store-products
####  ports:
####  - protocol: TCP
####    port: 80
####    targetPort: 80
#### EOF

3. Make sure the service is up in the cluster:
#### kubectl get svc store-products

3. Use kubectl exec to query the store-products service from the busybox testing pod.
##### kubectl exec busybox -- curl -s store-products