# Day4

## Lab - Deploying Hello Microservice using Custom Docker Image from Docker Hub
```
oc project jegan
oc create deployment hello --image=tektutor/openshift-maven:latest
oc get deploy,rs,po
oc expose deploy/hello --port=8080
expose svc/hello
oc get route
curl curl hello-jegan.apps.ocp.tektutor-ocp-labs
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/95354aa7-3230-4da0-8a71-849b3cad8c85)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/af063a56-bb90-4cae-9e95-ce76dc520f11)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/f73c4d39-d6fd-4679-9b65-0d50282c1e39)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/3fabdcc6-3e0f-4047-9e89-8390eb233089)


## Creating an edge route
```
openssl genrsa -out key.key
openssl req -new -key key.key -out csr.csr -subj="/CN=nginx-jegan.apps.ocp.tektutor-ocp-labs"
openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
oc create route edge --service nginx --hostname nginx-jegan.apps.ocp.tektutor-ocp-labs --key key.key --cert crt.crt
```
