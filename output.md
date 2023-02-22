# Steps to run the robot-shop application on K8s:

The following steps outline the necessary steps involved in running the robot-shop
application on minikube

Stop the minikube
\# minikube stop

Start the minikube
\# minikube start

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

# Commiting directly to the master branch is not a best practice for the following reasons:
1. GIT keeps an account of all the commit logs which will lost lost otherwise. There will be not accountability and credibility.
2. When we do a merge, we will get to know about the merge conflicts.
3. Copy/paste can introduce unintended results.

# How can you prevent it:
Go to Settings -> Branches -> Branch Protection Rules -> Add branch protection rule

![Add branch protection rule] (https://github.com/vdhar71/robot-shop/blob/master/GIT-branch-protection.png)

# Final image:
! [Could change name and build the application] (https://github.com/vdhar71/robot-shop/blob/master/final-robot-shop.png)

I am running my application an Apple Silicon MacBook Pro. Per documentation, there is limitation. I made changes to the 
robot-shop/web/static/index.html and tried to build using docker-compose build, but it failed.

dhar-arm:robot-shop vidyadhar$ docker-compose build
WARN[0000] The "INSTANA_AGENT_KEY" variable is not set. Defaulting to a blank string.
[+] Building 0.0s (0/0)
[+] Building 0.0s (0/0)
[+] Building 0.0s (0/0)
[+] Building 0.0s (0/0)
[+] Building 0.2s (1/1)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.3s (2/2)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.2s (1/2)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.2s (1/1)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.5s (2/3)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
 => => transferring dockerfile: 32B                                                                                                    0.0s
[+] Building 0.3s (2/2)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.3s (2/2)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.3s (2/2)
 => [internal] load build definition from Dockerfile                                                                                   0.0s
[+] Building 0.6s (2/3)
[+] Building 0.5s (2/3)
[+] Building 0.5s (2/3)
[+] Building 0.8s (3/3) FINISHED
 => [internal] load build definition from Dockerfile                                                                                   0.0s
 => => transferring dockerfile: 32B                                                                                                    0.0s
[+] Building 0.6s (3/3) FINISHED
 => [internal] load build definition from Dockerfile                                                                                   0.0s
 => => transferring dockerfile: 32B                                                                                                    0.0s
 => [internal] load .dockerignore                                                                                                      0.0s
 => => transferring context: 2B                                                                                                        0.0s
 => CANCELED [internal] load metadata for docker.io/library/node:14                                                                    0.3s
failed to solve: rpc error: code = Unknown desc = failed to solve with frontend dockerfile.v0: failed to create LLB definition: no match for platform in manifest sha256:8cf035b14977b26f4a47d98e85949a7dd35e641f88fc24aa4b466b36beecf9d6: not found

