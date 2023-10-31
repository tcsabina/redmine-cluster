Steps to get started:

Create the database-service:
minikube kubectl -- apply -f database-service.yaml

Create the database:
minikube kubectl -- apply -f database.yaml

Create redmine, together with the redmine-service:
minikube kubectl -- apply -f redmine.yaml


With this setup the redmine pod and the redmine-service is up and running.
You need to expose the redmine-service:
minikube service redmine-service

This will start a browser that is connected to the redmine-service.
At the first time you will need to define the admin password.


To remove something:
minikube kubectl -- delete --cascade='foreground' -f redmine.yaml

