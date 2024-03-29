# Simple deployment with kubernetes

This is a simple example of deploying a docker image to Kubernetes.


## Task 1: Ensure you have a kubernetes cluster running with at least 1 node

Help for setting up kubernetes cluster can be found here:

https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/

Basically 2 easy options to run kubernetes locally is to use docker-for-desktop or minikube. For OS X at least docker-for-desktop kubernetes is easier to set up.

If using docker for desktop, launch it from the docker-for-desktop settings and run:

```
kubectl config get-contexts
kubectl config use-context docker-for-desktop
```


## Task 2: Build your image and push it to docker hub

First, let's open terminal and navigate to the root of the repository we want to build. If you have not created Docker Hub account you can create one at: https://hub.docker.com/signup . Then ensure you are logged in to Docker hub with

```
docker login
```

Build your docker image and tag it

```
docker build -t <your-docker-hub-username>/<image-name> .
```

Lastly push it to Docker Hub

```
docker push <your-docker-hub-username>/<image-name>
```

## Task 3: Deploy your application to kubernetes

Ensure that your kubernetes is configured correctly with typing

```
kubectl version
```

After that deploy your application

```
kubectl run <desired-deployment-name> --image=docker.io/<your-docker-hub-username>/<image-name>:latest --port=<desired-port>
```

Verify your deployment is running

```
kubectl get deployments
```

Lastly, expose your deployment with:

```
kubectl expose deployment/<desired-deployment-name> --type="NodePort" --port <desired-port>
```

Get the port number of the exposed service with

```
kubectl get services
```

The command should output the service name and the port mapping associated with it. Now navigate to to localhost:\<port-number\> . You should be able to see your application now.

If you are using minikube to run your Kubernetes you can get the url you need to use to access your application by typing:

```
minikube service <service-name> --url
```

## Task 4: Cleaning up

Delete service create with:

```
kubectl delete service <desired-deployment-name>
```

And lastly delete the deployment with:

```
kubectl delete deployment <desired-deployment-name>
```
