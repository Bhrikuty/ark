//Let's pull down the Heptio Ark GitHub repo to help us get started: 

git clone https://github.com/heptio/ark

//Apply some basic prerequisites (e.g. CustomResourceDefinitions, namespaces, and RBAC): 
kubectl apply -f ark/examples/common/00-prereqs.yaml

//Apply a local storage service (e.g. Minio):
kubectl apply -f ark/examples/minio/

//Deploy an example nginx application: 
kubectl apply -f ark/examples/nginx-app/base.yaml

Check to see that both Ark and nginx deployments have been successfully created or not




//Let's download and install the Ark client:

curl -LO https://github.com/heptio/ark/releases/download/v0.9.0/ark-v0.9.0-linux-amd64.tar.gz

tar -C /usr/local/bin -xzvf ark-v0.9.0-linux-amd64.tar.gz

//Let's backup any resource with labels "app=nginx": 
ark backup create nginx-backup --selector app=nginx

//Now, let's simulate a disaster: 
kubectl delete namespace nginx-example

Check that the nginx service and deployment are gone........

To REstore
//Run: 
ark restore create --from-backup nginx-backup

//Run: 
ark restore get

NOTE: The restore can take a few moments to finish. During this time, the STATUS column reads InProgress.

Refer https://www.katacoda.com/courses/kubernetes/heptio-ark 
