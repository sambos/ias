
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
  



# gcloud useful commands
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

gcloud config list
gcloud config configurations list
gcloud config configurations describe <account>
gcloud auth list
gcloud info
gcloud projects list




# networking commands
gcloud compute networks list
gcloud compute networks subnets list
gcloud compute networks sublets list --network vpc-1
gcloud compute networks create vpc-2 --description "vpc 2" --subnet-mode custom
gcloud compute firewall-rules create <firewall-rule-name> --network vpc-2 --allow tcp:22
gcloud compute networks subnets create <subnet-name: vpc-2-europe-west-2-1> --network vpc-2 --region europe-west2 --range 10.10.1.0/24

#delete networks (if vm installed in subnet they must be deleted first)
gcloud compute networks subnets delete <subnet-name> --region europe-west2
gcloud compute firewall-rules delete <firewall-name>
gcloud compute networks delete vpc-2

```



### Resources
* https://github.com/ned1313/terraform-tuesdays/tree/main/2021-07-20-Getting-Started-GCP