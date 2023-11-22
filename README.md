Steps to get started:

We assume that the minikube installation is done, and you have a healthy system.


##
First create the LoadBalancer:
`minikube kubectl -- apply -f load-balancer.yaml`

Verify the creation of the service: 
`minikube kubectl -- get svc`


##
Create the database-service:
`minikube kubectl -- apply -f database-service.yaml`  

Verify the creation of the service: 
`minikube kubectl -- get svc`

You should now see both the `myreds` and the `postgres-service` services listed.


##
Create the statefulest for the database:
`minikube kubectl -- apply -f database.yaml`

Verify both the statefulset and the pod: 
`minikube kubectl -- get sts`
`minikube kubectl -- get pod`


##
Create the directory on the minikube host for the persistent volume:
ssh into the minikube VM: `minikube ssh`

Create the directory: `mkdir /tmp/hostpath-provisioner/default/redmine-files/`

After this we can leave the minikube VM: `exit`

Now we can create the persistent volume and the volume claim:
`minikube kubectl -- apply -f redmine-files.yaml`

Verify that both created, and the status for both is "Bound":
`minikube kubectl -- get pv`
`minikube kubectl -- get pvc`


##
Create the redmine-service:
`minikube kubectl -- apply -f redmine-service.yaml`

Check if the service is created and healthy:
`minikube kubectl -- get svc`


##
Create the redmine statefulset:
`minikube kubectl -- apply -f redmine.yaml`

Check both the statefulset, and the pods:
`minikube kubectl -- get sts`
`minikube kubectl -- get pod`

##
Create the dashboard-service:
`minikube kubectl -- apply -f dashboard-service.yaml`

Check if the service is created and healthy:
`minikube kubectl -- get svc`


##
Create the dashboard deployment:
`minikube kubectl -- apply -f dashboard.yaml`

Check both the statefulset, and the pods:
`minikube kubectl -- get deploy`
`minikube kubectl -- get pod`


##
If all the above operations succeeded, and every service, statefulset, volume claim and pod is active and healthy, our MyReds application is ready to server!

The access the loadbalancer, you need to expose it to the host system that runs minikube:
`minikube tunnel`

After this start a browser on the host system:
navigate to http:\\\\localhost, should open the redmine GUI
navigate to http:\\\\localhost:81, should open the dashboard, which shows all Issues of the redmine system


##
To remove something:
`minikube kubectl -- delete --cascade='foreground' -f <yaml-file.yaml>`


