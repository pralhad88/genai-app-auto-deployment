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

7. 
`gcloud iam service-accounts list` `github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com`

8. gcloud projects add-iam-policy-binding genai-auto-deploy --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" --role="roles/artifactregistry.writer"

9. gcloud projects add-iam-policy-binding genai-auto-deploy --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" --role="roles/run.admin"

10. gcloud projects add-iam-policy-binding genai-auto-deploy \ --member="serviceAccount:github-actions-robot@genai-auto-deploy.iam.gserviceaccount.com" \ --role="roles/iam.serviceAccountUser"