# What Is Terraform?

Terraform is an **open‑source Infrastructure as Code (IaC) tool** created by HashiCorp. It allows you to define, provision, and manage cloud and on‑premises infrastructure using declarative configuration files that are human-readable.

Instead of clicking through cloud consoles, you write code that describes the desired state of your infrastructure. Terraform then handles the API calls required to create, update, or destroy resources.

Terraform is "cloud-agnostic," meaning it can manage resources across multiple providers (AWS, Azure, GCP, Kubernetes, etc.) using a single workflow.

---

## Key concepts

* **Data Sources:** Read‑only lookups for existing infrastructure.

* **Declarative:** You define what the final infrastructure should look like, not how to build it step-by-step.

* **HashiCorp Configuration Language (HCL):** A simple, human-readable language used to write configuration files (.tf files).
 
* **Modules:** Reusable units of Terraform configuration.

* **Outputs:** Values returned after deployment (e.g., IP addresses).

* **Providers:** Plugins that let Terraform manage resources in a specific platform (AWS, Azure, etc.).

* **Resources:** The actual infrastructure objects (VMs, networks, storage accounts, databases).

* **State:** Terraform’s record of what it has created. Stored locally or remotely (e.g., S3, Azure Storage).

* **State file:** A JSON file (terraform.tfstate) that acts as a "source of truth," tracking the real-world resources managed by your code.

* **Variables:** Inputs that make configurations reusable.

* **Workflow:**
  
* Write: Define resources in .tf files.
* Plan: terraform plan previews changes before applying them.
* Apply: terraform apply executes the actions to reach the desired state. 

---

## Why terraform exists

Modern infrastructure is:
- distributed  
- multi‑cloud  
- dynamic  
- versioned  
- automated  

Terraform provides a consistent way to manage all of it using code. This enables:
- repeatable deployments  
- version control  
- automation  
- peer review  
- predictable changes  

---

## Terraform is declarative

Terraform uses a **declarative model**:

> You describe *what* you want, and Terraform figures out *how* to build it.

You don’t write scripts that say:
- “create this first,”  
- “then attach that,”  
- “then configure this.”

Instead, you define the end state, and Terraform:
- builds a dependency graph  
- determines the correct order  
- applies only the necessary changes  

---

## Terraform Uses HashiCorp Configuration Language (HCL)

Terraform configuration files use **HCL**, a human‑readable language designed for infrastructure.

Example:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f"
  instance_type = "t2.micro"
}
```

HCL is:
- easy to read  
- easy to write  
- designed for declarative infrastructure  
- optionally expressible in JSON  

---

## Terraform is cloud‑agnostic

Terraform works across many providers using the same workflow.

Common providers include:
- AWS  
- Azure  
- Google Cloud  
- Kubernetes  
- GitHub  
- Cloudflare  
- Datadog  
- Okta  

This makes Terraform ideal for:
- multi‑cloud deployments  
- hybrid environments  
- consistent workflows across teams  

---

## Terraform’s core workflow

Terraform uses a simple, predictable workflow:

### **1. `terraform init`**  
Downloads providers and prepares the working directory.

### **2. `terraform plan`**  
Shows what Terraform *will* change before it changes anything.

### **3. `terraform apply`**  
Applies the changes and brings infrastructure to the desired state.

### **4. `terraform destroy`**  
Tears down infrastructure when it’s no longer needed.

---

## Core Terraform Commands

Terraform uses a simple, predictable workflow built around four primary commands. These commands form the backbone of every Terraform project, from small examples to full production deployments.

### `terraform init`
Initializes the working directory and downloads the required providers and modules.  
This must be run before any other Terraform command.

### `terraform plan`
Generates an execution plan showing what Terraform *will* change.  
This is a safe, read‑only preview of additions, updates, and deletions.

### `terraform apply`
Applies the changes required to reach the desired state.  
Terraform creates, updates, or deletes infrastructure based on the plan.

### `terraform destroy`
Removes all infrastructure managed by the current configuration.  
Useful for cleanup, testing, and temporary environments.


---

## Why Terraform workflows matter for documentation and validation

Terraform examples must be:
- syntactically correct  
- semantically valid  
- compliant with cloud naming rules  
- deployable  
- minimal but complete  
- consistent with provider schemas  

This is why these validation workflows pages are useful. Terraform examples are easy to write but surprisingly easy to get wrong.

---

## Examples of Terraform usage

These examples are standard Terraform reference configurations used for validation testing. They are intentionally minima and based on public provider schemas.

### Provisioning an AWS EC2 Instance
   
This example defines a single virtual machine in AWS. 


```hcl
# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create an EC2 Instance
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0" # Example AMI ID
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleInstance"
  }
}
```


### Creating a Secure Azure Storage Container
   
This example demonstrates creating a resource group and a storage container in Azure. 

```hcl
# Configure the Azure Provider
provider "azurerm" {
  features {}
}

# Create a Resource Group
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "East US"
}

# Create a Storage Account
resource "azurerm_storage_account" "example" {
  name                     = "examplestorageacc"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
}
```

### Scaling Infrastructure (Variable Use) 

Using variables allows you to scale resources easily. 

```hcl
variable "instance_count" {
  default = 2
}

resource "aws_instance" "server" {
  count         = var.instance_count
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "Server-${count.index}"
  }
}
```
---

# Summary

Terraform provides:

- a unified IaC workflow  
- declarative configuration  
- multi‑cloud support  
- predictable deployments  
- reusable modules  
- version‑controlled infrastructure  
