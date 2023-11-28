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
```
oc get svc
cd ~/openshift-nov-2023
git pull
cd Day2/ingress
cat ingress.yml
oc apply -f ingress.yml
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/76ae8b1c-fec9-4f0e-a315-79824118b51e)
