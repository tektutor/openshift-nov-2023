# Day3

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
