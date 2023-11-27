## Red Hat OpenShift pre-test link

Kindly complete the pre-test from RPS Cloud lab windows machine
https://app.mymapit.in/code4/tiny/UPrPW4

Once you completed the test, do let me know so that we can start the training.

## What is Container Runtime?
- is a low-level software that knows how manage containers
  - create a new container
  - listing running containers
  - listing exited containers
  - start/stopping/restarting/deleting/aborting containers
- they aren't so user-friendly, hence normally no end-users use it directly

## What is a Container Engine ?
- is a high-level software that provides user-friendly commands to manage container images and containers
- Container Engines internally makes use of Container Runtime to manage containers
- For example:
  - Docker Container Engine depends on runC Container Runtime
  - Podman Container Engine depends on CRI-O Container Runtime
  
## Docker Overview
- Application Virtualization Technology
- each container represents one running application
- in other words, each container is an application process
- containers don't get their own dedicated hardware resources
- containers are not OS
- containers will never be able to replace Virtual Machine or Operating System
- Certain features of Containers appears similar to an Operating System
- Just like Virtual Machines get an IP address, even container gets their own IP address
- Just like Virtual machines has it own file system, even container has its file sytem
- Virtual Machine with Linux distributions has its own package managers to install/uninstall/update/upgrade softwares, same way container also has its own package managers
- Unlike Virtual machines, the containers runs only one single application wherease VMs are fully functional Operating System hence many applications can run in the operating system installed within Virtual Machine.
- is a Container Engine

## What is a Container Orchestration Platform?
- Orchestration Platform tools helps us manage containerized application workloads
- containerized application workloads could be
  - Microservices
  - Web servers
  - Application Servers
  - REST/SOAP/Web Services
  - DB Servers
  
- they works as a cluster of servers
- Examples
  - Docker SWARM ( supports only managing Docker containerized applications )
  - Google Kubernetes ( supports many different container runtimes unlike Docker SWARM )
    - Opensource and free for personal and commercial use
    - is a production grade, robust orchestration platform
  
  - Red Hat OpenShift ( supports only CRI-O container runtime and Podman Container Engine )
    - developed on top of the opensource Google Kubernetes
    - hence OpenShift supports all the features of Kubernetes
    - OpenShift also supports many additional features which aren't supported by Kubernetes
    - This is an enterprise grade Orchestration platform that requires license from Red Hat

- advantages of using Orchestration Platforms
  - Orchestration Platforms provides an eco-system/environment where you could make your deployed applications highly available(HA)
  - Scaling up/down your application instances is easy on demand
  - Rolling update ie you can upgrade your application workloads from one version to other without any downtime
  - provides in-built monitoring features to check health, liveniness checks for your application workloads
  - load balances features supports both internal and external load balancers

## OpenShift Overview
- Red Hat OpenShift is developed on top of Google Kubernetes
- OpenShift supports all the features of Kubernetes + many additional features
- Google Kubernetes supports Operators and Custom Resources, with this Kuberenetes allows extending Kubernetes functaionalities
- Using the Operators and Custom Resources,the Red Team has add many additional features on top of Kubernetes which is distributed in the name of Red Hat OpenShift
- In other words, Openshift is Red Hat's variant of Kubernetes

## OpenShift Alternatives
- Docker SWARM
  - it is very user-friendly
  - light weight
  - can be easily installed on laptops with normal configurations
  - easy to learn
  - it is not production grade orchestration platform, hence normally used for learning, protyping, dev/qa environments
  
- Google Kubernetes
  - supports only Command Line
  - production grade
  - open source, hence can be used for personal and commercial purpose
  - it does support Kubernetes Dashboard (Web console) as it doesn't support multi-users or login credentails it is considered insecure and opens up some security issues, hence this is one of the first thing Systems Admins disable
 
## OpenShift High Level Architecture

## OpenShift Common Resources
- Pod
  - group of CRI-o containers, a configuration(JSON object) that is stored/managed within etcd database
  - group of containers
  - In Kubernetes/OpenShift IP address is assigned only on the Pod level not on the container level
  - one Pod represents one running instance of an application
  - ideally only one main application should be running within a Pod
- ReplicaSet 
  - a configuration that is stored/managed within etcd database
  - is a JSON object
  - how many Pods are supposed to running for a specific application deployment
  - one or more Pods
  - each ReplicaSet represents one version of an Application deployment
- Deployment
  - is a JSON Object
  - stored within etcd database
  - has one or more ReplicaSets
  - this reprents your application deployed within Openshift
- Controllers
  - are the one which monitors and manages one specific type of OpenShift Resource
  - Deployment Controller
  - ReplicaSet Controller
  - Endpoint Controller
  - Job Controller
  - StatefulSet Controller
  - DaemonSet Controller

## Openshift components/tools
- kubectl - Kubernetes command-line client tool
- oc - openshift command-line client tool
- kubelet
  - container agent that runs as a service in all the nodes of OpenShift
  - this runs in master as well as worker node
  - this component interacts with the Container Runtime to pull images and manage containers/pods
- kube-proxy
  - is a components that runs in every node i.e worker and master nodes
  - provides load-balancing to group of pods that belongs to a specific deployment

# Lab Exercises

## Lab - Checking Docker version
```
docker --version
```

## Lab - Listing Docker images
```
docker images
```

## Lab - Listing all running containers
```
docker ps
```

## Lab - Listing all containers running and exited
```
docker ps -a
```

## Lab - Creating multi containers (Pod) and letting them share same IP in Docker
```
docker run -d --name ubuntu_pause --hostname ubuntu1 google/pause:latest
docker run -dit --name ubuntu1 --network=container:ubuntu_pause ubuntu:22.04 bash
```

Listing the running containers
```
docker ps
```

Finding the IP Address of ubuntu_pause container
```
docker inspect ubuntu_pause | grep IPA
```

Finding the IP Address of ubuntu1 containers
```
docker exec -it ubuntu1 /bin/bash
hostname -i
exit
```

As you have noticed, the ubuntu1 and ubuntu_pause containers shares the IP address, this is how Pods are created in Kubernetes/OpenShift.

## Lab - Listing all nodes in the Red Hat OpenShift cluster
```
oc get nodes
```

Expected output
<pre>
┌──(jegan㉿tektutor.org)-[~/openshift-nov-2023]
└─$ oc get nodes
NAME                             STATUS   ROLES                         AGE     VERSION
master-1.ocp.tektutor-ocp-labs   Ready    control-plane,master,worker   4h48m   v1.27.6+b49f9d1
master-2.ocp.tektutor-ocp-labs   Ready    control-plane,master,worker   4h49m   v1.27.6+b49f9d1
master-3.ocp.tektutor-ocp-labs   Ready    control-plane,master,worker   4h48m   v1.27.6+b49f9d1
worker-1.ocp.tektutor-ocp-labs   Ready    worker                        4h34m   v1.27.6+b49f9d1
worker-2.ocp.tektutor-ocp-labs   Ready    worker                        4h34m   v1.27.6+b49f9d1  
</pre>
