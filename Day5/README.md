# Day 5

## What is a canary deployment strategy?
- is a progressive rollout of an application that splits traffic between an already-deployed version and a new version
- rolling it out to a subset of users before rolling out fully

## What is a canary deployment strategy?
- gives us a chance to partially release our application
- we can ensure the new version of our application is reliable before we can deliver it to all users
- we could deploy the new version of our application to a limited number of pods
- the old version would continue to run, but with more of the traffic being sent to the new pods

## Blue Green vs Canary Deployment Strategy
- Blue-green and Canary deployments are two popular strategies for continuous delivery
- aims to deliver software updates faster and more reliably
- both methods of allows us release new versions of software without disrupting the existing service
- the main difference is that blue-green deployments switches all the traffic from the old version (blue) to the new version (green) at once
- while canary deployments gradually expose a small percentage of the traffic to the new version (canary) and monitor its performance and user behavior before rolling it out to the rest of the users

## Lab - Let's deploy a serverless application in Red Hat OpenShift
It is assumed that your System Administrator has already install Red Hat OpenShift Serverless operator, created an instance of knative serving.  With which the following exercise will not work.

```
kn service create greeter --image=quay.io/rhdevelopers/knative-greeter:quarkus
```

Expected output





## Ignore this Lab - Pod Autoscaling
```
oc process -f https://examples.openshift.pub/deploy/autoscaling/pod-autoscaling-template.yaml | oc apply -f -
```

Test Autoscaling
```
# Note - ab is Apache Bench tool to benchmark the applications
ab 'http://choas-professor-omd.paas.osp.consol.de/chaos/heapheap?size=500&time=10000'
ab 'http://choas-professor-omd.paas.osp.consol.de/chaos/cpu?threads=100&keepAlive=20000'
ab -c 10 -n 100 'http://choas-professor-omd.paas.osp.consol.de/chaos/cpu?threads=100&keepAlive=200'
```

Clean up
```
oc get all -o name | xargs -n1  oc delete
oc delete hpa/choas-professor
```
