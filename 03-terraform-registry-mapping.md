# Terraform Registry Cheat Sheet  
*Common Azure Terraform resources mapped to their Registry documentation, with quick “what to look for” notes.*

Use this page when you want a fast reminder of **what to check** in the Terraform Registry for each resource. For deeper detail, see the **Terraform Registry Validation Guide**.

---

## 1. Resource Groups  
**Terraform:** `azurerm_resource_group`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group  

**What to look for:**
- **Required:** `name`, `location`  
- **Optional:** `tags`  
- **Terraform‑enforced:** none for naming  
- **Common issues:** wrong location spelling, incorrect casing for locations  

---

## 2. Storage Accounts  
**Terraform:** `azurerm_storage_account`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_account  

**What to look for:**
- **Required:** `name`, `resource_group_name`, `location`, `account_tier`, `account_replication_type`  
- **Terraform‑enforced:** `name` must be lowercase only  
- **Common issues:** uppercase or hyphens in `name`, invalid replication type, missing `account_tier`  

---

## 3. Storage Containers  
**Terraform:** `azurerm_storage_container`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_container  

**What to look for:**
- **Required:** `name`, `storage_account_name`  
- **Optional:** `container_access_type`  
- **Terraform‑enforced:** `name` must be lowercase only  
- **Common issues:** uppercase letters in names, invalid access type, missing dependency on storage account  

---

## 4. Virtual Machines  
**Terraform:**  
- `azurerm_linux_virtual_machine`  
- `azurerm_windows_virtual_machine`  

**Registry:**  
- Linux: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine  
- Windows: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/windows_virtual_machine  

**What to look for:**
- **Required:** `name`, `resource_group_name`, `location`, `size`, `admin_username`, `network_interface_ids`, OS disk block  
- **Terraform‑enforced:** none for naming  
- **Common issues:** missing OS disk, incorrect image reference, wrong NIC reference syntax, insecure `admin_password` usage  

---

## 5. Virtual Networks  
**Terraform:** `azurerm_virtual_network`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network  

**What to look for:**
- **Required:** `name`, `address_space`, `location`, `resource_group_name`  
- **Optional:** `dns_servers`  
- **Common issues:** invalid CIDR blocks, missing list brackets for `address_space`, incorrect RG reference  

---

## 6. Subnets  
**Terraform:** `azurerm_subnet`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet  

**What to look for:**
- **Required:** `name`, `resource_group_name`, `virtual_network_name`, `address_prefixes`  
- **Common issues:** using `address_prefix` instead of `address_prefixes`, wrong VNet name, overlapping CIDR blocks  

---

## 7. Public IP Addresses  
**Terraform:** `azurerm_public_ip`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip  

**What to look for:**
- **Required:** `name`, `location`, `resource_group_name`, `allocation_method`  
- **Valid values:** `Static`, `Dynamic`  
- **Common issues:** wrong casing for allocation method, missing SKU when required by downstream resources  

---

## 8. Network Security Groups  
**Terraform:** `azurerm_network_security_group`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_group  

**What to look for:**
- **Required:** `name`, `location`, `resource_group_name`  
- **Optional:** `security_rule` blocks  
- **Common issues:** incorrect priority ordering, missing direction/access, invalid port ranges  

---

## 9. Azure SQL Server  
**Terraform:** `azurerm_mssql_server`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mssql_server  

**What to look for:**
- **Required:** `name`, `resource_group_name`, `location`, `administrator_login`, `administrator_login_password`  
- **Terraform‑enforced:** none for naming (Azure enforces lowercase + length)  
- **Common issues:** uppercase letters in server name, missing admin credentials, incorrect firewall rule blocks  

---

## 10. Azure SQL Database  
**Terraform:** `azurerm_mssql_database`  
**Registry:** https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mssql_database  

**What to look for:**
- **Required:** `name`, `server_id`  
- **Optional:** `collation`, `max_size_gb`, `sku_name`  
- **Common issues:** wrong SKU names, missing server reference, invalid collation strings  

