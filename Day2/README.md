# Day2

## Lab - Creating routes to make it accessible outside the cluster
```
oc get deploy
oc delete svc/nginx
oc expose deploy/nginx --port=8080
oc expose svc/nginx
oc get route
curl 
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/f755638b-4b5e-4d70-bca5-644ab0f1e252)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/7aa71a69-60ed-43c0-a817-64a1910bd481)

## Lab - Creating ingress routing rules for HAProxy Load Balancer
Before you apply the ingress manifest file, you need to replace the host from "tektutor.apps.ocp.tektutor-ocp-labs" to "tektutor.apps.ocp4.rps.com"

```
oc get svc
cd ~/openshift-nov-2023
git pull
cd Day2/ingress
cat ingress.yml
oc apply -f ingress.yml
oc get ingress
oc describe ingress/tektutor
oc get svc
curl http://tektutor.apps.ocp.tektutor-ocp-labs/nginx
curl http://tektutor.apps.ocp.tektutor-ocp-labs/hello
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/76ae8b1c-fec9-4f0e-a315-79824118b51e)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/6d0d22bd-da5b-42cc-99ac-cff805815b0f)

## Lab - Deploying nginx in declarative style
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
oc create deploy nginx --image=bitnami/nginx:latest --dry-run=client -o yaml
oc create deploy nginx --image=bitnami/nginx:latest --dry-run=client -o yaml > nginx-deploy.yml
oc apply -f nginx-deploy.yml
oc get deploy,rs,po
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/054ffc61-5f75-4fd1-9f80-0d03a3102bd1)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/c16cd6e9-4ba1-400b-b7fb-5b221efb6ee9)
