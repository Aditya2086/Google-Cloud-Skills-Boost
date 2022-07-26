# Perform Foundational Infrastructure Tasks in Google Cloud - Challenge Lab

## Let's start with defining some variables given by Cloud Skill Boosts

Defining bucket name variable
```
export BUCKET_NAME=
```
Defining Cloud Pub/Sub topic name variable
```
export TOPIC_NAME=
```
Defining Cloud Function name variable
```
export CLOUDFUNCTION_NAME=
```
Defining username variable
```
export USERNAME2=
```

## Downloading index.js and package.json file we will use this while creating cloud function 

```
wget https://github.com/Aditya2086/Google-Cloud-Skills-Boost/blob/1b60b5b597eb07d4450aaa02697580ef5a9182dd/Track%201:%20Cloud%20Infrastructure%20Track%20-%20Challenge%20Labs/Perform%20Foundational%20Infrastructure%20Tasks%20in%20Google%20Cloud/index.js

wget https://github.com/Aditya2086/Google-Cloud-Skills-Boost/blob/1b60b5b597eb07d4450aaa02697580ef5a9182dd/Track%201:%20Cloud%20Infrastructure%20Track%20-%20Challenge%20Labs/Perform%20Foundational%20Infrastructure%20Tasks%20in%20Google%20Cloud/package.json

```

## Task 1: Create a bucket

```
gsutil mb gs://$BUCKET_NAME
```
## Task 2: Create a Pub/Sub topic

```
gcloud pubsub topics create $TOPIC_NAME
```

## Task 3: Create the thumbnail Cloud Function

3.1 Replacing the variable with REPLACE_WITH_YOUR_TOPIC ID 
```
sed -i "s/REPLACE_WITH_YOUR_TOPIC ID/$TOPIC_NAME/g" index.js
```
3.2 Create a function with name thumbnail
```
gcloud functions deploy $CLOUDFUNCTION_NAME \
    --entry-point thumbnail \
    --runtime nodejs12 \
    --trigger-bucket $BUCKET_NAME \
    --region us-east1
```
2. Testing cloud function working by uploading given file into the bucket 

2.1 Downloading sample image
```
wget https://storage.googleapis.com/cloud-training/gsp315/map.jpg
```
2.2 uploading sample image to the bucket
```
gsutil cp map.jpg gs://$BUCKET_NAME
```
## Task 4: Remove the previous cloud engineer
```
gcloud projects remove-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member=user:$USERNAME2 --role=roles/viewer
```
 
# Congratulations! You've Completed Your Challenge Lab :)
## Happy Learning :)
## See You In The Cloud...

