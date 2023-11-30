# Day4

## Lab - Deploying Hello Microservice using Custom Docker Image from Docker Hub
Upgrading the openssl in CentOS
https://webhostinggeeks.com/howto/install-update-openssl-centos/

```
oc project jegan
oc create deployment hello --image=tektutor/openshift-maven:latest
oc get deploy,rs,po
oc expose deploy/hello --port=8080
oc expose svc/hello
oc get route
curl hello-jegan.apps.ocp.tektutor-ocp-labs
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/95354aa7-3230-4da0-8a71-849b3cad8c85)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/af063a56-bb90-4cae-9e95-ce76dc520f11)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/f73c4d39-d6fd-4679-9b65-0d50282c1e39)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/3fabdcc6-3e0f-4047-9e89-8390eb233089)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/8aa8005a-4179-4dd3-b1d7-4bc425e01c07)


## Lab - Deploying Hello Microservice application from source code using github code repository url
```
oc project jegan
oc new-app https://github.com/tektutor/spring-ms.git --strategy=docker
oc logs -f buildconfig/spring-ms
oc get svc 
oc expose svc/spring-ms
oc get route
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/bc92c9b0-585c-4277-b365-d9c536eff4a6)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/bef74028-2e38-494a-a583-bee98901bdfa)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/1efb944f-8316-4391-b8e4-0cb83429fd94)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/59b67334-704c-4681-9767-47694ae70404)


## Lab - Building the application within OpenShift with source strategry using source code from GitHub url
```
oc new-app registry.access.redhat.com/ubi8/openjdk-11~https://github.com/tektutor/spring-ms.git --strategy=source
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/e0b7ba66-9bd4-47e9-b6c5-314d129e82ae)

Let's check the build status as shown below
```
oc logs -f buildconfig/spring-ms
```
Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/0905997e-8259-4fa4-8fa4-a5d00dff6618)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/91720e4c-f791-4c70-8f81-711d2bb40d89)

You may try listing the deployment
```
oc get deploy,rs,po
oc get svc
oc expose svc/spring-ms 
```

![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/372969d5-26f3-47e6-b444-4918cbabe6a3)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/5b745b1f-54aa-42d1-8778-a742916a4605)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/d7d4da56-f9d5-4b64-bba1-4f9fcb34e7fe)


## Lab - Securing our application route with edge route (https)
```
openssl genrsa -out key.key
openssl req -new -key key.key -out csr.csr -subj="/CN=hello-jegan.apps.ocp.tektutor-ocp-labs"
openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
oc create route edge --service spring-ms --hostname hello-jegan.apps.ocp.tektutor-ocp-labs --key key.key --cert crt.crt
```
