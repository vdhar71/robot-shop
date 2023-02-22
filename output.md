Steps to run the robot-shop application on K8s:

The following steps outline the necessary steps involved in running the robot-shop
application on minikube

Stop the minikube
# minikube stop

Start the minikube
# minikube start

Navigate to 'helm' directory under robot-shop. The following example is with Helm 3.x:
$ kubectl create ns robot-shop
namespace/robot-shop created
$ helm install robot-shop --namespace robot-shop .
NAME: robot-shop
LAST DEPLOYED: Tue Feb 21 16:45:21 2023
NAMESPACE: robot-shop
STATUS: deployed
REVISION: 1
TEST SUITE: None

The above did not start the application:

! [Unable to start the application via Kubernetes minikube] (https://github.com/vdhar71/robot-shop/blob/master/k8s-failure-k9s-output.png)

I have an ARM based MacBook Pro.  So had to move to Docker-compose.

Run Locally:

$ docker-compose pull

Fire up the application along with some load:

$ docker-compose -f docker-compose.yaml -f docker-compose-load.yaml up

![Robot shop application via docker-compose] (https://github.com/vdhar71/robot-shop/blob/master/robot-shop.png)





