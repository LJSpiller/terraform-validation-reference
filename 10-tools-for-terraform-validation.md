# Tools and setup for terraform validation

This page lists recommended tools and environment settings that support the validation workflows described in Pages 1 through 5.

These tools are especially helpful when reviewing AI‑generated Terraform examples, which often contain subtle schema or naming issues that automated linting can catch early.

To ensure technical accuracy and minimize manual errors when validating Terraform samples, use this environment configuration. This setup allows for real-time syntax checking (linting) and schema validation without needing to deploy live infrastructure.

---

## 1. Visual Studio Code extensions

Use these two extensions in tandem to provide full coverage for both HCL syntax and Azure-specific platform rules.

### **[HashiCorp Terraform](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform)**

* **The "Why":** This is the official industry-standard extension. 
* **Validation Power:** Provides **Syntax Highlighting** (spots missing braces/quotes) and **IntelliSense** (suggests valid resource attributes like `account_tier`).
* **Workflow:** When you type `resource "azurerm_...`, it pulls the current schema from the Terraform Registry to ensure your code matches the latest version.

### **[Azure Terraform (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureterraform)**

* **The "Why":** Essential for validating Microsoft-specific content.
* **Validation Power:** Includes a **Preflight Validation** command that checks if your configuration is valid specifically for Azure Resource Manager (ARM).
* **Workflow:** Integrates with the Azure Cloud Shell, allowing you to quickly test a command in a real terminal if a naming rule is ambiguous.

---

## 2. The Terraform CLI
Even if you aren't a DevOps Engineer, having the **Terraform CLI** installed is a "superpower" for a Technical Writer or Technical Editor. 

### **The "One Command" Validation**
By running one command in the VS Code terminal, you can instantly verify if a sample is "deployable" from a syntax perspective:

```bash
terraform validate
```

* **What it catches:** Missing required arguments, mismatched data types (e.g., a string where a number belongs), and circular dependencies.
* **Why it's safe:** This command is **static**. It checks the logic of the code without ever connecting to a cloud provider or costing money.

---

## 3. GitHub and PR workflow

For Microsoft Learn-style workflows, use **GitHub Desktop** or the **VS Code Git Integration** to:

* Track changes to technical samples over time.
* Manage "Docs-as-Code" PRs (Pull Requests).
* Run automated "Linters" (like `TFLint`) that can be integrated into a GitHub Action to catch errors before the documentation is ever published.




