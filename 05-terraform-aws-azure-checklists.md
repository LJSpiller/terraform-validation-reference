# Terraform Validation Checklists  
*Azure + AWS + Naming Quick‑Reference*

This page provides:
- Terraform example validation checklists  
- AWS equivalents for common patterns  
- A combined Azure + Terraform naming quick‑reference table  

Use this page alongside the other pages for a complete validation workflow.

---

# 1. Terraform Example Validation Checklists

## 1.1 General Terraform Validation Checklist
Use this for **any** Terraform example.

### Syntax & Structure
- Valid HCL syntax  
- Correct resource type spelling  
- Correct provider spelling  
- No deprecated arguments  

### Required Arguments
- All required arguments present  
- No missing blocks (e.g., OS disk, network interface)  

### Optional Arguments
- Optional arguments used correctly  
- No invalid combinations  

### Naming Rules
- Check Terraform‑enforced rules (lowercase, case‑sensitive fields)  
- Check Azure platform naming rules (length, characters, hyphens)  
- Check AWS naming rules (looser, mostly tag‑based)  

### Dependencies
- Correct resource references  
- No circular dependencies  
- Correct use of `depends_on` when needed  

### Variables & Outputs
- Variables typed correctly  
- Defaults valid  
- Outputs reference valid attributes  

### Deployability
- Example can deploy as written  
- No placeholder values that break deployment  
- No invalid regions or SKUs  

---

## 1.2 Azure‑Specific Terraform Validation Checklist

### Provider & Resource Types
- Provider: `azurerm`  
- Resource types match Registry exactly  

### Naming Rules (Azure)
- Check ARM naming rules  
- Check CAF naming guidance  
- Validate length, characters, case, hyphens  

### Common Azure Pitfalls
- Storage account names with hyphens  
- Container names with uppercase letters  
- Wrong VM image reference format  
- Incorrect VNet/subnet CIDR blocks  
- Missing `features {}` in provider block  

---

## 1.3 AWS‑Specific Terraform Validation Checklist

### Provider & Resource Types
- Provider: `aws`  
- Resource types match Registry exactly  

### Naming Rules (AWS)
- AWS is more permissive  
- Most naming rules apply to tags, not resources  
- Some services enforce length/character rules (e.g., S3)  

### Common AWS Pitfalls
- Invalid AMI IDs  
- Wrong region spelling  
- Missing required IAM blocks  
- Incorrect security group rule syntax  
- Using `availability_zone` instead of `availability_zone_id`  

---

# 2. AWS Equivalents for Common Azure Patterns

| Concept | Azure Resource | AWS Equivalent | Notes |
|--------|----------------|----------------|-------|
| Virtual Machine | `azurerm_linux_virtual_machine` | `aws_instance` | AWS uses AMIs; Azure uses image references |
| Virtual Network | `azurerm_virtual_network` | `aws_vpc` | VPC is AWS’s VNet |
| Subnet | `azurerm_subnet` | `aws_subnet` | Nearly identical concepts |
| Network Security Group | `azurerm_network_security_group` | `aws_security_group` | AWS SGs are stateful; Azure NSGs are stateless |
| Public IP | `azurerm_public_ip` | `aws_eip` | AWS Elastic IPs |
| Storage Account | `azurerm_storage_account` | S3 bucket (`aws_s3_bucket`) | Very different naming rules |
| SQL Server | `azurerm_mssql_server` | `aws_rds_instance` | RDS supports SQL Server engine |
| SQL Database | `azurerm_mssql_database` | `aws_rds_cluster` or `aws_rds_instance` | Depends on engine mode |

---

# 3. Azure + Terraform Naming Quick‑Reference Table

## 3.1 Azure Naming Rules (Platform‑Level)

| Resource Type | Length | Allowed Characters | Case | Hyphens | Notes |
|---------------|--------|--------------------|------|---------|-------|
| Storage Account | 3–24 | a–z, 0–9 | Lowercase | ❌ | Must be globally unique |
| Storage Container | 3–63 | a–z, 0–9, - | Lowercase | ✔ | No consecutive hyphens |
| Resource Group | 1–90 | Letters, numbers, (), ., -, _ | Mixed | ✔ | No trailing period |
| Virtual Machine | 1–15 (Windows), 1–64 (Linux) | Letters, numbers, - | Mixed | ✔ | Must start with letter/number |
| VNet | 2–64 | Letters, numbers, ., -, _ | Mixed | ✔ | — |
| Subnet | 1–80 | Letters, numbers, ., -, _ | Mixed | ✔ | — |
| Public IP | 1–80 | Letters, numbers, ., -, _ | Mixed | ✔ | — |
| SQL Server | 1–63 | a–z, 0–9, - | Lowercase | ✔ | Must start with letter |
| SQL Database | 1–128 | Letters, numbers, -, _ | Mixed | ✔ | — |

---

## 3.2 Terraform‑Enforced Naming Rules

| Resource | Terraform‑Enforced Rules |
|----------|--------------------------|
| `azurerm_storage_account` | Lowercase only |
| `azurerm_storage_container` | Lowercase only |
| `azurerm_mssql_server` | None (Azure enforces lowercase) |
| `azurerm_resource_group` | None |
| `azurerm_virtual_network` | None |
| `azurerm_subnet` | None |
| `azurerm_public_ip` | None |

Terraform enforces **very few** naming rules — Azure enforces most of them.

---

# 4. Combined Azure + Terraform Validation Flow (Quick Version)

1. **Check Terraform Registry**  
   - Required arguments  
   - Optional arguments  
   - Valid values  
   - Terraform‑enforced constraints  

2. **Check Azure ARM Naming Rules**  
   - Length  
   - Characters  
   - Case  
   - Hyphens  
   - Uniqueness  

3. **Check CAF Naming Guidance**  
   - Patterns  
   - Abbreviations  
   - Recommended structures  

4. **Validate Example**  
   - Syntax  
   - Dependencies  
   - Deployability  

This is the fastest way to validate any Azure Terraform example.

---

# 5. Summary

This page gives you:
- Terraform validation checklists  
- AWS equivalents for Azure resources  
- A combined Azure + Terraform naming quick‑reference  

Use this page when reviewing Terraform examples, validating AI‑generated IaC, or preparing for technical interviews.

