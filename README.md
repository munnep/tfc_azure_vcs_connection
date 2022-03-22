# tfc_azure_vcs_connection

This repository describes a step by step creation of the following

- Create a repository within Azure DevOps Services with Terraform code to execute
- Create a VCS connection from Terraform Cloud to Azure DevOps
- Create a workspace within Terraform Cloud  

This repository is based on the official HashiCorp documentation:  
[https://www.terraform.io/cloud-docs/vcs/azure-devops-services](https://www.terraform.io/cloud-docs/vcs/azure-devops-services)


# Prerequisites

- Access to Azure DevOps
- Access to Terraform Cloud

# How to

## Create a repository within Azure DevOps

- login to Azure DevOps
[https://dev.azure.com/](https://dev.azure.com/)
- create a new Project   
![](media/2022-03-22-15-11-24.png)  
- Give it a name and make it public/private and click create    
![](media/2022-03-22-15-12-37.png)  
- go to Repos -> files -> Initialize Main branch with a README     
![](media/2022-03-22-15-14-49.png)  
- select new branch    
![](media/2022-03-22-15-15-30.png)  
- fill in the details   
![](media/2022-03-22-15-16-18.png)  
- create a new file called ```main.tf```  
![](media/2022-03-22-15-17-06.png)  
- Add the following code and click commit
```
provider "random" {}

resource "random_pet" "pet1" {}

output "pet1" {
  value = random_pet.pet1.id
}
```
- commit  
![](media/2022-03-22-15-19-38.png)  
- edit the ```README.md``` with the following and commit
```
# Repository tfc_example_azure

This repository is stored within Azure DevOps services

It is used for an example using a VCS provider within Terraform Cloud
```
- commit    
![](media/2022-03-22-15-22-04.png)  
- Go to repos --> branches   
![](media/2022-03-22-15-23-19.png)  
- create a new pull request  
![](media/2022-03-22-15-23-48.png)    
![](media/2022-03-22-15-24-32.png)  
- Complete the merge
![](media/2022-03-22-15-25-07.png)  
![](media/2022-03-22-15-25-22.png)  

## Check Azure DevOps settings
- login to Azure DevOps
[https://dev.azure.com/](https://dev.azure.com/)
- go to your organization settings  
![](media/2022-03-22-15-27-12.png)  
- Go to Policies and make sure the ```Third-party application access via OAuth``` is turned on as below   
![](media/2022-03-22-15-28-29.png)  

## Create a VCS provider to Azure DevOps

### Terraform Cloud - Part 1
- Login to your Terraform Cloud organization
[Terraform Cloud](https://app.terraform.io/app)
- Go to Settings -> Version Control -> Providers
- Click on add a VCS provider  
![](media/2022-03-22-15-34-01.png)  
- Select Azure DevOps Services  
![](media/2022-03-22-15-34-27.png)
- leave this page open
- Go to the next Chapter on Azure DevOps Services

### Azure DevOps Services
We are going to create an application with DevOps to use
- Go to the following page 
[DevOps](https://aex.dev.azure.com/app/register?mkt=en-US)
- Add the information you find on the Terraform Cloud page

| Field name                 | Value                                       |
| -------------------------- | ------------------------------------------- |
| Company name               | HashiCorp                                   |
| Application Name           | Terraform Cloud (YOUR ORGANIZATION NAME)    |
| Application website        | https://app.terraform.io                    |
| Authorization callback URL | https://app.terraform.io/YOUR CALLBACK URLV |

- Check the boxes for ```code (read)``` and ```Code (status)``` only  
![](media/2022-03-22-15-43-31.png)  
- at the bottem create application  
![](media/2022-03-22-15-43-58.png)  
- Copy the app secret and client secret to the Terraform Cloud location
![](media/2022-03-22-15-44-47.png)  
- Go back to the Terraform Cloud page again

### Terraform Cloud - Part 2

- Insert a name for the connection
- Paste the App ID from the Azure page 
**NOTE the space that you perhaps copy/paste in the beginning**
- Client Secret  
![](media/2022-03-22-15-47-46.png)  
- Accept the connection  
![](media/2022-03-22-15-57-39.png)  
- Skip the SSH key pair   
![](media/2022-03-22-15-59-36.png)  

## Create a workspace using the VCS provider and the DevOps repository

- Login to Terraform Cloud
