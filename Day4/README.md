# Day4

## Lab - Deploying Hello Microservice using Custom Docker Image from Docker Hub
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





## Ignore this for now - Creating an edge route
```
openssl genrsa -out key.key
openssl req -new -key key.key -out csr.csr -subj="/CN=nginx-jegan.apps.ocp.tektutor-ocp-labs"
openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
oc create route edge --service nginx --hostname nginx-jegan.apps.ocp.tektutor-ocp-labs --key key.key --cert crt.crt
```
