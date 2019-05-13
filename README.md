# Simple deployment with kubernetes

This is a simple example of deploying a docker image to Kubernetes.


## Task 1: Ensure you have a kubernetes cluster running with at least 1 node

Help for setting up kubernetes cluster can be found here:

https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/

If using docker for desktop, launch it from the docker-for-desktop settings and run:

```
kubectl config get-contexts
kubectl config use-context docker-for-desktop
```


## Task 2: Build your image and push it to docker hub

Ensure you are logged in to Docker hub with

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
kubectl expose deployment/react-lesson-2 --type="NodePort" --port 8000
```

Get the port number of the exposed service with

```
kubectl get services
```

Now navigate to to localhost:\<port-number\>
