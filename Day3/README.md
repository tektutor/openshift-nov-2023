# Day3

## What is ConfigMaps?
- If your application deployment need to configure certain details, like path of JDK, maven path, etc, instead of hard coding those information, we could store them in a configmap in the key/value format.
- Your application can retrieve the data and use those values in the deployments
- This is similar to properties we use in java or other languages
- This should be used only to store non-sensitive as anyone can view the information stored inside the configmap

## What is OpenShift Secret?
- OpenShift secrets works exactly like configmap, except that it stores sensitive data like login credentials, certs , etc in an encrypted fashion
- whatever data is stored in a secret will be visible
- hence, your application can securely store sensitive data in secrets and securely access them from your application

## Lab - Using ConfigMaps and Secrets within deployment
```
cd ~/openshift-nov-2023
git pull
cd Day3/configs-and-secrets
oc apply -f secrets.yml
oc get secrets
oc describe secrets/mysql-login-credentials
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/cfab21f5-86af-4241-88e5-75f6b1b8e87f)

Now, let's try to create the configmap that has non-sensitive data
```
cd ~/openshift-nov-2023
git pull
cd Day3/configs-and-secrets
oc apply -f cm.yml
oc get configmaps
oc describe cm/
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/a21164de-97b7-4085-9412-dd2e08924290)

Now, create the mysql deployment
```
cd ~/openshift-nov-2023
git pull
cd Day3/configs-and-secrets
oc apply -f mysql-deploy.yml
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/b608a309-021a-4595-8207-3d01d1e479cf)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/49adbb81-70cd-4cf0-8520-b9c49520d640)

## Lab - Deploying Wordpress and MariaDB multi-pod application that uses Persistent Volume and Persistent Volume Claims
In this lab exercise, you will practically learn the below topics
- Practical use-case of ConfigMaps and Secrets
- Service Discovery
- How two different application deployment Pods communicate via Service
- Using Perristent Volumes and Claims
- Routes
- ClusterIP Internal Service

Let's first deploy mariadb db server into Openshift  
```
cd ~/openshift-nov-2023
git pull
cd Day3/wordpress-configmap-and-secrets
oc apply -f wordpress-secrets.yml
oc apply -f wordpress-cm.yml
oc apply -f mysql-pv.yml
oc apply -f mysql-pvc.yml
oc apply -f mysql-deploy.yml
oc apply -f mysql-svc.yml
```

Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/4386fbff-4aa0-4a80-bcc7-e89df91b2664)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/50dde9cc-1862-4375-a128-d5867c2cc7fc)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/0c0e5377-196e-4a32-9e42-f278d78a7cda)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/3be2b3a6-3cd5-4a79-9940-46256d6766e4)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/b7a962bf-3b71-4bc0-8c53-f815c958cd6c)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/f9217737-c92a-43b7-b84a-6705458aec1d)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/dfccbf02-8c99-456b-b06a-15e70f68c5f9)


Let's then deploy wordpress
```
cd ~/openshift-nov-2023
git pull
cd Day3/wordpress-configmap-and-secrets
oc apply -f wordpress-pv.yml
oc apply -f wordpress-pvc.yml
oc apply -f wordpress-deploy.yml
oc apply -f wordpress-svc.yml
oc apply -f wordpress-route.yml
```
Expected output
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/e2848922-15bc-4f7f-bcd0-13bcf9bd47f2)

![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/6ac7700d-41be-46f7-aea0-d961c94c9281)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/775add8b-5fb2-493a-9ef1-22fd2b1c1875)
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/0a40d48a-4c2a-4c0d-847b-c05c61d0c24d)

## Lab - Installing Helm Package Manager

Installing helm on your lab machine
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
