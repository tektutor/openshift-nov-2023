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
![image](https://github.com/tektutor/openshift-nov-2023/assets/12674043/6ac7700d-41be-46f7-aea0-d961c94c9281)
