# Google Cloud Project setup 
1. Create Project on G-Cloud
`gcloud projects create genai-auto-deploy --name="GenAI Automation"`

2. List Down List of billing account. My paid account is `01F8A8-15F0F0-68D4A0`
`gcloud billing accounts list`

3. Set billing account for Project 
`gcloud billing projects link genai-auto-deploy --billing-account 01F8A8-15F0F0-68D4A0`

4. Set Project default config
`gcloud config set project genai-auto-deploy`

5. Create a docker artifact for docker

`gcloud services enable artifactregistry.googleapis.com run.googleapis.com iam.googleapis.com`

6. GitHub Action IAM role
`gcloud iam service-accounts create github-actions-robot`

7. Create a IAM role and policy for Github Action
`gcloud iam service-accounts list` 
MY service account details `github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com`

## Attach below IAM policy to the GitHub Action service.
1. `gcloud projects add-iam-policy-binding genai-auto-deploy --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" --role="roles/artifactregistry.writer"`

2. `gcloud projects add-iam-policy-binding genai-auto-deploy --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" --role="roles/run.admin"`

3. `gcloud projects add-iam-policy-binding genai-auto-deploy --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" --role="roles/iam.serviceAccountUser"`


8. Create Data warehouse repository
`gcloud artifacts repositories create genai-repo --repository-format=docker --location=asia-south1 --description="Warehouse for our automated GenAI builds"`

9. Create A gcp Key for GitHub service
`gcloud iam service-accounts keys create gcp_key.json --iam-account=github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com`