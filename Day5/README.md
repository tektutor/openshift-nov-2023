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

## Lab - Checking the knative serverless cli tool version
```
kn version
```
Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/7a667fa8-b0f1-4259-8394-ef36eb17c0aa)

## Lab - Let's deploy a serverless application in Red Hat OpenShift
It is assumed that your System Administrator has already install Red Hat OpenShift Serverless operator, created an instance of knative serving.  With which the following exercise will not work.

```
kn service create greeter --image=quay.io/rhdevelopers/knative-tutorial-greeter:quarkus
```

Expected output


## Lab - Autoscaling knative application based on knative events
In this lab exercise, you will be creating serverless knative application. 
```
cd ~/openshift-nov-2023
git pull
cd Day5/serverless/eventing
oc apply -f hello-sink.yml
kn service list
```

Expected output

Now you can create the ping source application which would trigger the hello sink application.  This is a knative cronjob.
```
cd ~/openshift-nov-2023
git pull
cd Day5/serverless/eventing
oc apply -f ping-source.yml
kn source ping list
```

Now head over to OpenShift webconsole to see the topology in the Developer view
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/3e50f8bc-4109-4484-b122-c831c0a35694)


The the ping-source cronjob triggers the hello knative application every minute. For every message 1 Pod will be auto-scaled, you could observe this in the web console.

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
