# Day4

## Creating an edge route
```
openssl genrsa -out key.key
openssl req -new -key key.key -out csr.csr -subj="/CN=nginx-jegan.apps.ocp.tektutor-ocp-labs"
openssl x509 -req -in csr.csr -signkey key.key -out crt.crt
oc create route edge --service nginx --hostname nginx-jegan.apps.ocp.tektutor-ocp-labs --key key.key --cert crt.crt
```
