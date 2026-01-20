# Azure Naming Rules Cheat Sheet 

*Cheatsheet that is mapped to common `azurerm_*` Terraform resources.*

---

## 1. Resource Groups
**Terraform:** `azurerm_resource_group`  
**Azure Namespace:** `Microsoft.Resources/resourceGroups`  
**Naming Rules:**  
- 1–90 characters  
- Alphanumeric, underscores, parentheses, hyphens, periods  
- No trailing period  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules  

<br>

**CAF Guidance:**  
https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming

---

## 2. Storage Accounts
**Terraform:** `azurerm_storage_account`  
**Azure Namespace:** `Microsoft.Storage/storageAccounts`  

<br>

**Naming Rules:**  
- 3–24 characters  
- Lowercase only  
- Alphanumeric only  
- Globally unique  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules  

<br>

**CAF Guidance:**  
https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming

---

## 3. Storage Containers (Blob Containers)
**Terraform:** `azurerm_storage_container`  
**Azure Namespace:** `Microsoft.Storage/storageAccounts/blobServices/containers`  

<br>

**Naming Rules:**  
- 3–63 characters  
- Lowercase only  
- Alphanumeric + hyphens  
- Must start with letter or number  
- No consecutive hyphens  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules  

<br>

**CAF Guidance:**  
https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming

---

## 4. Data Lake Storage Gen2
**Terraform:** `azurerm_storage_account` with `is_hns_enabled = true`  

<br>

**Naming Rules:**  
- Same as storage accounts  
- No hyphens  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 5. Virtual Machines
**Terraform:**  
- `azurerm_linux_virtual_machine`  
- `azurerm_windows_virtual_machine`  
**Azure Namespace:** `Microsoft.Compute/virtualMachines`  

<br>

**Naming Rules:**  
- Windows: 1–15 characters  
- Linux: 1–64 characters  
- Alphanumeric + hyphens  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 6. Virtual Networks
**Terraform:** `azurerm_virtual_network`  
**Azure Namespace:** `Microsoft.Network/virtualNetworks`  

<br>

**Naming Rules:**  
- 2–64 characters  
- Alphanumeric, underscores, hyphens, periods  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 7. Subnets
**Terraform:** `azurerm_subnet`  
**Azure Namespace:** `Microsoft.Network/virtualNetworks/subnets` 

<br>

**Naming Rules:**  
- 1–80 characters  
- Alphanumeric, underscores, hyphens, periods  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 8. Public IP Addresses
**Terraform:** `azurerm_public_ip`  
**Azure Namespace:** `Microsoft.Network/publicIPAddresses` 

<br>

**Naming Rules:**  
- 1–80 characters  
- Alphanumeric, underscores, hyphens, periods  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 9. Network Security Groups
**Terraform:** `azurerm_network_security_group`  
**Azure Namespace:** `Microsoft.Network/networkSecurityGroups`  

<br>

**Naming Rules:**  
- 1–80 characters  
- Alphanumeric, underscores, hyphens, periods  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 10. Azure SQL Server
**Terraform:** `azurerm_mssql_server`  
**Azure Namespace:** `Microsoft.Sql/servers`  

<br>

**Naming Rules:**  
- 1–63 characters  
- Lowercase only  
- Alphanumeric + hyphens  
- Must start with a letter  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules

---

## 11. Azure SQL Database
**Terraform:** `azurerm_mssql_database`  
**Azure Namespace:** `Microsoft.Sql/servers/databases`  

<br>

**Naming Rules:**  
- 1–128 characters  
- Alphanumeric, underscores, hyphens  

<br>

**ARM Rules:**  
https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules
