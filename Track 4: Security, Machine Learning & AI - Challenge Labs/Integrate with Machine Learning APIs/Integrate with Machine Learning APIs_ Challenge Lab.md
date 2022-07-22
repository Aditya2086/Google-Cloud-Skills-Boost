# Integrate with Machine Learning APIs: Challenge Lab

[YouTube Video Link](https://youtu.be/JnLoobzhlTI)

## Defining some variables given by Cloud Skill Boosts

```
export LANGUAGE=
```

```
export LOCAL=
```

```
export BIGQUERY_ROLE=
```

```
export CLOUD_STORAGE_ROLE=
```

## Task 1: Configure a Service Account & IAM permissions


1.1 Create a sample service account

```
gcloud iam service-accounts create sample-sa
```

1.2 Bind bigquery role to the created Service Account

```
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member=serviceAccount:sample-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role=$BIGQUERY_ROLE
```

1.3 Bind Cloud Storage role to the created Service Account

```
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member=serviceAccount:sample-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role=$CLOUD_STORAGE_ROLE
```
1.4 Create a key of your Service Account

```
gcloud iam service-accounts keys create sample-sa-key.json --iam-account sample-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com
```

1.5 Define Google Application Credentials for all API calls

```
export GOOGLE_APPLICATION_CREDENTIALS=${PWD}/sample-sa-key.json
```

## Download the file analyze-images-v2.py

```
wget https://raw.githubusercontent.com/guys-in-the-cloud/cloud-skill-boosts/main/Challenge-labs/Integrate%20with%20Machine%20Learning%20APIs%3A%20Challenge%20Lab/analyze-images-v2.py
```
- this command will change your Locale content
```
sed -i "s/'en'/'${LOCAL}'/g" analyze-images-v2.py
```
- In Cloud Shell run
```
python3 analyze-images-v2.py $DEVSHELL_PROJECT_ID $DEVSHELL_PROJECT_ID
```
- Run this bigquerry command 
```
bq query --use_legacy_sql=false "SELECT locale,COUNT(locale) as lcount FROM image_classification_dataset.image_text_detail GROUP BY locale ORDER BY lcount DESC"
```

