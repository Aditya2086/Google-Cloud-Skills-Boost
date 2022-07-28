# Ensure Access & Identity in Google Cloud - Challenge Lab

## Let's start with defining some variables given by Cloud Skill Boosts

```
export CUSTOM_SECURIY_ROLE=
```
```
export SERVICE_ACCOUNT=
```
```
export CLUSTER_NAME=
```

## Task 1: Create a custom security role.

```
wget https://github.com/Aditya2086/Google-Cloud-Skills-Boost/blob/c4fb5d93fe7dbee8c400d2c920e62c622e1e5039/Track%204:%20Security,%20Machine%20Learning%20&%20AI%20-%20Challenge%20Labs/Ensure%20Access%20&%20Identity%20in%20Google%20Cloud/role-definition.yaml
```

```
sed -i "s/<IAM-ROLE-NAME-TASK-1>/$CUSTOM_SECURIY_ROLE/g" role-definition.yaml
```

```
gcloud iam service-accounts create orca-private-cluster-sa --display-name "${SERVICE_ACCOUNT} Service Account"
gcloud iam roles create $CUSTOM_SECURIY_ROLE --project $DEVSHELL_PROJECT_ID --file role-definition.yaml

```

## Task 2: Create a service account

```
gcloud iam service-accounts create $SERVICE_ACCOUNT --display-name "${SERVICE_ACCOUNT} Service Account"
```

## Task 3: Bind a custom security role to an account

```
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member serviceAccount:$SERVICE_ACCOUNT@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.viewer

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member serviceAccount:$SERVICE_ACCOUNT@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.metricWriter

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member serviceAccount:$SERVICE_ACCOUNT@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/logging.logWriter

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member serviceAccount:$SERVICE_ACCOUNT@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role projects/$DEVSHELL_PROJECT_ID/roles/$CUSTOM_SECURIY_ROLE

```
## Task 4: Create and configure a new Kubernetes Engine private cluster
```
gcloud config set compute/zone us-east1-b
```

```
gcloud container clusters create $CLUSTER_NAME --num-nodes 1 --master-ipv4-cidr=172.16.0.64/28 --network orca-build-vpc --subnetwork orca-build-subnet --enable-master-authorized-networks  --master-authorized-networks 192.168.10.2/32 --enable-ip-alias --enable-private-nodes --enable-private-endpoint --service-account $SERVICE_ACCOUNT@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --zone us-east1-b

```
- SSH Machine orca-jumphost
```
gcloud compute ssh --zone "us-east1-b" "orca-jumphost" 
```
```
gcloud config set compute/zone us-east1-b
```
```
export CLUSTER_NAME=
```
```
gcloud container clusters get-credentials $CLUSTER_NAME --internal-ip

kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0

kubectl expose deployment hello-server --name orca-hello-service --type LoadBalancer --port 80 --target-port 8080
```



# Congratulations! You've Completed Your Challenge Lab :)
## Happy Learning :)
## See You In The Cloud...



