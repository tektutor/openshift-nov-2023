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
- Just like Virtual Machines get an IP address, even container get their own IP address
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

## OpenShift Alternatives

## OpenShift High Level Architecture

## OpenShift Common Resources

