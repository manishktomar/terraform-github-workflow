# Terraform and Github Workflow (Action) 

This setup provides a fully automated pipeline that deploys an EC2 instance on AWS whenever code is pushed to GitHub.
![image](https://github.com/user-attachments/assets/1e6181f7-e0d5-49c1-8b2b-d800b4069d5a)

### Trigger Jenkins Pipeline via GitHub

When you push code to your GitHub repository, the GitHub Actions workflow will:
1. Set up AWS credentials using the GitHub Secrets.
2. Trigger the Jenkins pipeline, which will run the Terraform code.

## Prerequisites:
1. GitHub Repository containing your Terraform configuration files (main.tf, provider.tf, etc.).
2. AWS Access and Secret Keys stored as GitHub secrets.
3. GitHub Actions Workflow to pass AWS credentials to Jenkins and run Terraform.

## AWS IAM Policy for Terraform
User Name = CICD-User
AWS Credential Type = Access Key 
Attach Policy = Administration Access       // You can change any other policy.
Access Key and Secret Key                   // Required for Terraform.

### Steps:

- 1. GitHub Secrets
In your GitHub repository, go to **Settings** > **Secrets and variables** > **Actions** and add the following secrets:
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY

These keys will be passed to Terraform to allow it to authenticate with AWS.

- 2. Terraform Files
You need to add the Terraform configuration files (main.tf, provider.tf, variables.tf, and output.tf) to your GitHub repository.

- 3. GitHub Actions Workflow (.github/workflows/**terraform.yml**)
Create the GitHub Actions workflow in .github/workflows/terraform.yml. This workflow will handle AWS credentials, install Terraform, and run the Terraform commands when you push code to the repository.

- 4. Push Code to GitHub
Once you've added the Terraform files and the GitHub Actions workflow to your repository, commit and push the changes to the main branch.
- GitHub Actions will automatically trigger the workflow, set up AWS credentials, run Terraform, and provision the EC2 instance on AWS.

- 5. Monitor the Workflow
You can monitor the workflow's progress under the Actions tab in your GitHub repository. It will show the steps executed (checkout code, configure AWS credentials, Terraform init, plan, and apply).

#### Terraform Commands:
- terraform init initializes Terraform in the workspace.
- terraform workspace ensures that the right workspace is selected or created.
- terraform plan creates a plan to be executed.
- terraform apply applies the plan to create the EC2 instance.

### Summary:
- **GitHub Actions** handles AWS credentials, installs Terraform, and runs Terraform commands (init, plan, and apply).
- **Terraform** provisions an EC2 instance using the configuration in your GitHub repository.
- **AWS Credentials** are securely managed using GitHub Secrets, and the pipeline is triggered automatically on every code push to the specified branch.
