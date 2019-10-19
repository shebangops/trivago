Prerequisites:

- Minikube
- kubectl-cli

# start minikube
$ minikube start

# run deployments and services

//deployments

$ kubectl apply -f webserver.yml
$ kubectl apply -f mysql.yaml

//services
$ kubectl apply -f webserver-svc.yaml
$ kubectl apply -f mysql-svc.yaml

//claims, persistence volume for mysql
$ kubectl apply -f mysql-pv-claim.yaml

# check pods 
$ kubectl get pods 

# persitance volumes
In order to have saved data even when cluster, minikube is down i have mount path to minikube env so kubernetes can catch it. 
//start minikube with your path of the site so it can be persisten.
$minikube start --mount-string /Users/satoshe/workspace/trivago/php-apache/src:/data --mount

App is consisted with webserver (php 7 and apache) with mysql db on docker with Kubernetes orchestration. Docker image for php-apache images is created with Dockerfile while mysql is created with docker-composer. Everything was running on my local machine with minikube since i don`t have any avalibale resources on cloud providers. 


1. Logging
For log aggregators in the cluster, I would create an ELK stack with L replaces by Fluentd. It integrates nice with Kubernetes and has a great visualization with Kibana.
There is also a implementations of pod counter to stream logs out of cluster or node-level logging.
2. Monitoring
Prometheus and Grafana for centralized monitoring, also we can use the Kubernetes dashboard for monitoring basic metrics.
3. HA (high availability )
In this task, webserver deployment is written with replicas of 3 and service with loadbalancer.deployment of a newer version of docker images are preformed with rollout strategy, Blue-Green deployment where is zero down-time.

The app is pretty much basic, but the next step will be to deploy WordPress site or even platform with many microservices. Implementation of metrics, centralized logs, etc. Also, it improved Jenkinsfile. CI for dev/test environments etc.
