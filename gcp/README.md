
## Terraform with GCP

#### Steps
* download gcloud CLI
* Setup credentials
  * Setup New Project in google cloud
  * Add Service Account to project
  * Create Acess Key
* Enable billing for the Project
* Enable cloud services api (each service has an api, you must enable before you can use data source or resources for that service)

### Add Credentials
* For CLI based (cached locally): ``` gcloud auth application-default login  ```
* For File based (with access key) : ```export GOOGLE_APPLICATION_CREDENTIALS=~/.gcloud/auth-conf.json```
* Using Terraform Cloud as the Backend (remove new line character from file) - store your credentials in Terraform Cloud
  * ```export GOOGLE_CREDENTIALS="$(cat ~/.gcloud/auth-conf.json)"```
  
### gcloud useful commands
```
# create project
PROJECT_ID=taconet-${RANDOM}
gcloud projects create $PROJECT_ID --set-as-default

# to login using local cache
gcloud auth application-default login

# enable google service apis
gcloud services enable compute.googleapis.com
gcloud services enable cloudresourcemanager.googleapis.com


# list service accounts
gcloud iam service-accounts list --project <your porject id>
```



### Resources
* https://github.com/ned1313/terraform-tuesdays/tree/main/2021-07-20-Getting-Started-GCP