# Terraform Registry Validation Guide  
*Explains what to check in the Terraform Registry for common `azurerm_*` resources.*

This guide explains **what to look for** when reviewing Terraform examples, using the Terraform Registry as your authoritative source for schema rules, required arguments, optional arguments, valid values, and Terraform‑enforced constraints.

Use this alongside the Azure Naming Rules Cheat Sheet and the Unified Validation Workflow.

---

# 1. Resource Groups  
**Terraform resource:** `azurerm_resource_group`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group

### What to look for:
- **Required arguments:**  
  - `name`  
  - `location`
- **Optional arguments:**  
  - `tags`
- **Terraform‑enforced rules:**  
  - None for naming (Azure enforces naming rules)
- **Common issues:**  
  - Wrong location spelling  
  - Using uppercase in locations (Azure requires exact casing)

---

# 2. Storage Accounts  
**Terraform resource:** `azurerm_storage_account`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_account

### What to look for:
- **Required arguments:**  
  - `name`  
  - `resource_group_name`  
  - `location`  
  - `account_tier`  
  - `account_replication_type`
- **Terraform‑enforced rules:**  
  - `name` must be **lowercase only**
- **Valid values:**  
  - Replication types: `LRS`, `GRS`, `RAGRS`, `ZRS`, `GZRS`, `RAGZRS`
- **Common issues:**  
  - Uppercase letters in `name`  
  - Hyphens in `name` (Azure forbids them)  
  - Invalid replication type strings  
  - Missing `account_tier`

---

# 3. Storage Containers  
**Terraform resource:** `azurerm_storage_container`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_container

### What to look for:
- **Required arguments:**  
  - `name`  
  - `storage_account_name`
- **Terraform‑enforced rules:**  
  - `name` must be **lowercase only**
- **Optional arguments:**  
  - `container_access_type`
- **Common issues:**  
  - Uppercase letters in container names  
  - Invalid access types  
  - Missing dependency on storage account

---

# 4. Virtual Machines  
**Terraform resources:**  
- `azurerm_linux_virtual_machine`  
- `azurerm_windows_virtual_machine`  

**Registry:**  
Linux: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine  
Windows: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/windows_virtual_machine

### What to look for:
- **Required arguments:**  
  - `name`  
  - `resource_group_name`  
  - `location`  
  - `size`  
  - `admin_username`  
  - `network_interface_ids`  
  - OS disk block
- **Terraform‑enforced rules:**  
  - None for naming (Azure enforces VM name rules)
- **Common issues:**  
  - Missing OS disk block  
  - Incorrect image reference structure  
  - Wrong NIC reference syntax  
  - Using `admin_password` without secure settings

---

# 5. Virtual Networks  
**Terraform resource:** `azurerm_virtual_network`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network

### What to look for:
- **Required arguments:**  
  - `name`  
  - `address_space`  
  - `location`  
  - `resource_group_name`
- **Optional arguments:**  
  - `dns_servers`
- **Common issues:**  
  - Invalid CIDR blocks  
  - Missing brackets around `address_space` list  
  - Incorrect resource group reference

---

# 6. Subnets  
**Terraform resource:** `azurerm_subnet`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet

### What to look for:
- **Required arguments:**  
  - `name`  
  - `resource_group_name`  
  - `virtual_network_name`  
  - `address_prefixes`
- **Common issues:**  
  - Using `address_prefix` instead of `address_prefixes`  
  - Incorrect VNet name reference  
  - CIDR block overlaps

---

# 7. Public IP Addresses  
**Terraform resource:** `azurerm_public_ip`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip

### What to look for:
- **Required arguments:**  
  - `name`  
  - `location`  
  - `resource_group_name`  
  - `allocation_method`
- **Valid values:**  
  - `Static`  
  - `Dynamic`
- **Common issues:**  
  - Wrong allocation method casing  
  - Missing SKU when required by downstream resources

---

# 8. Network Security Groups  
**Terraform resource:** `azurerm_network_security_group`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_group

### What to look for:
- **Required arguments:**  
  - `name`  
  - `location`  
  - `resource_group_name`
- **Optional arguments:**  
  - `security_rule` blocks
- **Common issues:**  
  - Incorrect priority ordering  
  - Missing direction or access fields  
  - Invalid port ranges

---

# 9. Azure SQL Server  
**Terraform resource:** `azurerm_mssql_server`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mssql_server

### What to look for:
- **Required arguments:**  
  - `name`  
  - `resource_group_name`  
  - `location`  
  - `administrator_login`  
  - `administrator_login_password`
- **Terraform‑enforced rules:**  
  - None for naming (Azure enforces lowercase + length)
- **Common issues:**  
  - Uppercase letters in server name  
  - Missing admin credentials  
  - Incorrect firewall rule blocks

---

# 10. Azure SQL Database  
**Terraform resource:** `azurerm_mssql_database`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mssql_database

### What to look for:
- **Required arguments:**  
  - `name`  
  - `server_id`
- **Optional arguments:**  
  - `collation`  
  - `max_size_gb`  
  - `sku_name`
- **Common issues:**  
  - Wrong SKU names  
  - Missing server reference  
  - Invalid collation strings

---

# Summary

This guide helps you quickly identify:

- Required arguments  
- Optional arguments  
- Terraform‑enforced constraints  
- Valid values  
- Common pitfalls  

Use this alongside:

- **Azure Naming Rules Cheat Sheet**  
- **Unified Terraform Validation Workflow**  
- **Azure Resource Manager naming rules**  
- **Terraform Registry documentation**

Together, these provide a complete validation process.
