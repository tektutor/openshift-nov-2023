# Day2

## Day1 Feeback - Kindly provide your feedback here
https://tcheck.co/2HF9hd

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
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/fafe4f8c-e32f-4b07-be09-d4b43eace88e)

## Lab - Create a clusterip internal service in declarative style
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
oc get svc
oc expose deploy/nginx --port=8080 --dry-run=client -o yaml > nginx-svc.yml
oc apply -f nginx-svc.yml
oc get svc
oc describe svc/nginx
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/90c1ad0b-ab68-42cd-bc6f-8bb1fbeceda4)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/36737339-7568-4e1d-b274-15e5687dcfc1)

## Lab - Create a nodeport external service in declarative style
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
oc get svc
oc delete -f nginx-clusterip-svc.yml
oc expose deploy/nginx --type=NodePort --port=8080 --dry-run=client -o yaml > nginx-nodeport-svc.yml
oc apply -f nginx-nodeport-svc.yml
oc get svc
oc describe svc/nginx
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/d477afef-36c9-4b04-8dba-cb7f60d2e93d)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/6c5248d7-75c8-4890-997c-c2e200c921f4)


## Lab - Create a loadbalancer service in declarative style
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
oc get svc
oc delete -f nginx-nodeport-svc.yml
oc expose deploy/nginx --type=LoadBalancer --port=8080 --dry-run=client -o yaml > nginx-lb-svc.yml
oc apply -f nginx-lb-svc.yml
oc get svc
oc describe svc/nginx
```


Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/335fce62-a1c7-4e8f-acf8-4fddb6ea65bf)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/c21b3e60-8b66-48cf-b6cf-e5484513e575)


## Lab - Scaling up nginx deployment in declarative style
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
vim nginx-deploy.yml
oc apply -f nginx-deploy.yml
oc get deploy
oc get po
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/36cf3663-e4cd-42e0-a95d-7fffa68f5d3b)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/1fc500ce-d41d-4fcf-8837-9406937cfca1)

## Lab - Rolling update ( Upgrading nginx from one version to other without downtime )

You need to edit nginx-deploy and update the image version from latest to 1.23 as shown in the screenshot before applying.
```
cd ~/openshift-nov-2023
git pull
cd Day2/declarative-manifest
vim nginx-deploy.yml
oc apply -f nginx-deploy.yml
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/8a073d43-6246-49b5-8643-46a399e3e74c)
