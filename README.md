# Terraform validation reference
![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)
![Made with VS Code](https://img.shields.io/badge/Made%20with-VS%20Code-blue?logo=visual-studio-code)

A collection of reference pages designed to help technical writers and technical editors review and validate Terraform configuration files.

This repository provides a structured set of materials for creating, reviewing, and validating Terraform configuration samples. It includes workflows, checklists, naming rules, and full validation walkthroughs for both Azure and AWS. The content also supports validating AI‑generated Terraform examples, which often require additional checks for correctness and compliance with cloud platform rules.

---

## How to use this repository

*If you’re new to Terraform, start with `09-what-is-terraform.md` for a quick introduction, then return to `01-terraform-validation-workflow.md` to begin the validation process.*

These documents are intended as practical reference material for anyone who needs to:

- validate Terraform examples for correctness and deployability  
- check naming rules for Azure and AWS resources  
- review technical content that includes Terraform code  
- evaluate or refine AI‑generated Terraform examples  
- understand the reasoning behind Terraform validation workflows  

Each file focuses on a specific part of the validation process, and together they form a complete reference set.

**Pages:**

- **01–05** → The validation process  
- **06–08** → Full walkthroughs  
- **09** → Conceptual background information  
- **10** → Tooling and environment  

---

## Terraform validation process diagram

The following diagram provides a visual overview of the decision-making process for validating Terraform configuration samples.

<details>
<summary><b>Click to expand validation flowchart</b></summary>

<p align="center">
  <img src="assets/terraform-validation.svg" alt="Terraform Validation Process" width="100%">
</p>

</details>

## Files in this repository

| File Name | Purpose |
| :--- | :--- |
| **`01-terraform-validation-workflow.md`** | Process for validating Azure Terraform examples. |
| **`02-azure-naming-rules-cheatsheet.md`** | Azure naming rules cheatsheet. |
| **`03-terraform-registry-mapping.md`** | Cheatsheet of what to check in the Terraform Registry for each resource. |
| **`04-registry-validation-guide.md`** | Common `azurerm_*` Terraform Registry resources guide. |
| **`05-terraform-aws-azure-checklists.md`** | Azure + AWS + naming quick‑reference guide. |
| **`06-azure-example-full-validation.md`** | Azure storage account validation example. |
| **`07-aws-ec2-example-full-validation.md`** | AWS EC2 validation example. |
| **`08-terraform-scaling-example-full-validation.md`** | Terraform scaling validation example. |
| **`09-what-is-terraform.md`** | An overview and introduction to Terraform. |
| **`10-tools-for-terraform-validation.md`** | Tools and setup for Terraform validation. |
| **`terraform-validation`** | Visual process diagram in .svg and .png formats. |

---
## License

This repo and its assets are licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](https://creativecommons.org/licenses/by-nc-nd/4.0/).

You may share this work with attribution for non-commercial purposes, but you may not remix or reuse it in derivative works.
