

# 🚀 Azure Infrastructure Deployment with Terraform and GitHub Actions

Welcome to the **Azure Infrastructure Deployment** repository! This project uses **Terraform** and **GitHub Actions** to automate infrastructure provisioning on **Azure**, following best practices for modular and reusable code. 💻☁️

## 🏗️ Infrastructure Overview

This repository will deploy the following Azure resources:
- 📦 **App Service Plan** and **App Service** (integrated with VNet, managed identity enabled)
- 📊 **Application Insights** linked to the App Service
- 🐳 **Azure Container Registry (ACR)** with access for the App Service
- 🔐 **Azure Key Vault** (integrated with VNet, granting permissions to the App Service)
- 🌐 **Virtual Network (VNet)** with a subnet for private endpoints
- 🗄️ **SQL Server Database** with private endpoint
- 🗂️ **Storage Account** with private endpoint and file share for App Service
- 📁 **Storage Account** for storing the Terraform state file

## 📂 Project Structure

```plaintext
project-root/
├── main.tf                  # Main file to call modules
├── variables.tf             # Variables definition
├── outputs.tf               # Outputs for resources
├── terraform.tfvars         # Variable values
├── .github/
│   └── workflows/
│       └── terraform.yml    # GitHub Actions workflow
└── modules/                 # Modules for each resource
    ├── app_service/
    ├── acr/
    ├── key_vault/
    ├── sql_database/
    ├── storage_account/
    └── vnet/
```

## ⚙️ Prerequisites

Ensure you have the following:
- **Terraform** (>= 1.4.0) 🛠️
- **Azure CLI** for authentication and resource management 📟
- An **Azure Subscription** with necessary permissions ✅

## 🚀 Setup and Usage

1️⃣ **Clone the Repository**
```bash
git clone https://github.com/BlessedXd/azure_tf
cd azure_tf
```

2️⃣ **Configure Azure Credentials**
```bash
az login
az account set --subscription "your-subscription-id"
```

3️⃣ **Add GitHub Secrets**
To enable **GitHub Actions**, add the following secrets to your repository (Settings > Secrets):
🔑 AZURE_CLIENT_ID – Application (client) ID
🔑 AZURE_CLIENT_SECRET – Application secret
🔑 AZURE_SUBSCRIPTION_ID – Azure subscription ID
🔑 AZURE_TENANT_ID – Directory (tenant) ID

4️⃣ **Initialize Terraform**
```bash
terraform init
```

5️⃣ **Plan and Apply**
```bash
terraform plan
terraform apply
```

6️⃣ **GitHub Actions Workflow ⚡️**
**This repository includes** a GitHub Actions workflow in .github/workflows/terraform.yml to automate Terraform actions. It is triggered on push to main and pull requests, performing the following steps:

- Terraform Init: Initializes the backend
- Terraform Plan: Generates a deployment plan
- Terraform Apply: Applies changes on the main branch only

7️⃣ **Terraform Modules 🧩**
Each module in the modules/ directory corresponds to a specific Azure resource for modularity. Modules include:

- App Service Module (modules/app_service/): Deploys an App Service Plan and App Service, with VNet integration.
-VNet Module (modules/vnet/): Configures a Virtual Network and subnet.

8️⃣ **Remote Backend Configuration for Terraform State**
The backend for Terraform state is stored in an Azure Storage Account, created specifically for this purpose. The configuration in main.tf looks like this:
```plaintext
terraform {
  backend "azurerm" {
    resource_group_name  = var.resource_group
    storage_account_name = module.terraform_state_storage.name
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```
## **🧹 Clean Up**
```bash
   terraform destroy
```

## **🐞 Troubleshooting**

- **GitHub Actions Failures**: Ensure GitHub Secrets are set up correctly and accessible.
- **Terraform Errors**: Verify Azure permissions and variable configurations in terraform.tfvars.


## **🌐 Connect with Me**

Let's connect and share knowledge! Feel free to follow me on my social media platforms:

- [LinkedIn](https://www.linkedin.com/in/valeriy-manuilyk-22430a2b3/) 💼
- [Telegram](https://t.me/stoptalk1n) 🐦
- [GitHub](https://github.com/BlessedXd) 🐙

## **🤝 Contributions**

Contributions are welcome! If you have suggestions or improvements, feel free to open an issue or a pull request. 💬

## **📄 License**

This project is licensed under the MIT License. See the file for details. 📜

---

**Thank you for checking out my Azure Terraform Project! Happy learning! 🎉**
