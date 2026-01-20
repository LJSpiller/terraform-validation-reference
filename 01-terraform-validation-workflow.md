# Terraform Validation Workflow  
*A unified process for validating Azure Terraform examples using Terraform Registry, Azure platform rules, and Cloud Adoption Framework guidance.*

---

## 1. Overview

Terraform validation requires checking three authoritative sources:

1. **Terraform Registry**  
   - Required arguments  
   - Optional arguments  
   - Valid values  
   - Provider and resource spelling  
   - Terraform‑enforced constraints  

2. **Azure Resource Manager (ARM) Naming Rules**  
   - Length limits  
   - Allowed characters  
   - Case sensitivity  
   - Hyphen restrictions  
   - Uniqueness requirements  

3. **Azure Cloud Adoption Framework (CAF) Naming Guidance**  
   - Naming patterns  
   - Abbreviations  
   - Recommended structures  
   - General naming principles  

This workflow ensures Terraform examples are accurate, deployable, and aligned with Azure’s platform rules.

---

## 2. Step‑By‑Step Validation Process

### Step 1 — Identify the Terraform Resource
Example:  
`azurerm_storage_account`

### Step 2 — Open the Terraform Registry Page
Validate:
- Required arguments  
- Optional arguments  
- Valid values  
- Terraform‑enforced constraints (e.g., lowercase only)

Example Registry page:  
https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_account

### Step 3 — Map the Resource to the Azure Provider Namespace
Example:  
Storage account → `Microsoft.Storage/storageAccounts`

### Step 4 — Open the Azure Resource Manager Naming Rules
Validate:
- Length limits  
- Allowed characters  
- Case sensitivity  
- Hyphen rules  
- Uniqueness scope  

ARM naming rules:  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

### Step 5 — Cross‑Reference the Cloud Adoption Framework Naming Page
Use for:
- Naming patterns  
- Abbreviations  
- Component ordering  
- General naming guidance  

CAF naming page:  
https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming

### Step 6 — Validate the Terraform Example
Confirm:
- Names meet Azure’s platform rules  
- Required Terraform arguments are present  
- Optional arguments are used correctly  
- Values match allowed sets (e.g., replication types)  
- Example is deployable as written  

---

## 3. What Terraform Enforces vs. What Azure Enforces

### Terraform Enforces:
- Lowercase-only for some resources  
- Case sensitivity for certain arguments  
- Valid values for enumerations  
- Required arguments  

### Azure Enforces:
- Length limits  
- Allowed characters  
- Global uniqueness  
- Hyphen restrictions  
- Resource‑specific constraints  

---

## 4. Summary

This workflow ensures Terraform examples are validated against:

- Terraform’s schema  
- Azure’s platform rules  
- Azure’s naming best practices  

Use this process for every Azure Terraform example you review.
