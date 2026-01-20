# Full validation walkthrough: Azure storage account example

A complete validation walkthrough using this Azure storage acccount example.

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "East US"
}

resource "azurerm_storage_account" "example" {
  name                     = "examplestorageacc"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
}
```

This walkthrough uses the same steps in pages 1–5.

---

## 1. General Terraform validation checklist

**Syntax & structure**

- **HCL validity:**  
  - Blocks are correctly formed: `provider`, `resource`.  
  - Braces are balanced, indentation is consistent.  
  - Attribute assignments use `=` and valid HCL expressions.

- **Provider spelling:**  
  - `azurerm` is the correct provider name for Azure.

- **Resource type spelling:**  
  - `azurerm_resource_group` and `azurerm_storage_account` are valid resource types.

No syntax or structural issues.

---

## 2. Terraform Registry checks

### 2.1 `azurerm_resource_group`

**What the Registry expects:**

- **Required arguments:**  
  - `name`  
  - `location`
- **Optional:**  
  - `tags`

**Compare to example:**

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "East US"
}
```

- `name` present ✔  
- `location` present ✔  
- `tags` omitted (optional) ✔  

From a Terraform schema perspective, this block is complete and valid.

---

### 2.2 `azurerm_storage_account`

**What the Registry expects:**

- **Required arguments (core):**  
  - `name`  
  - `resource_group_name`  
  - `location`  
  - `account_tier`  
  - `account_replication_type`
- **Terraform‑enforced constraints:**  
  - `name` must be lowercase only.
- **Valid values:**  
  - `account_tier`: typically `Standard` or `Premium`.  
  - `account_replication_type`: `LRS`, `GRS`, `RAGRS`, `ZRS`, `GZRS`, `RAGZRS`.

**Compare to example:**

```hcl
resource "azurerm_storage_account" "example" {
  name                     = "examplestorageacc"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
}
```

- `name` present ✔  
- `resource_group_name` present ✔  
- `location` present ✔  
- `account_tier` present (`Standard`) ✔  
- `account_replication_type` present (`GRS`) ✔  
- `name` is all lowercase ✔  
- `GRS` is a valid replication type ✔  

From the Registry’s perspective, this resource is correctly specified.

---

## 3. Azure Resource Manager naming rules

Now apply the ARM naming rules (Page 1 + Page 2 + Page 5 mental model).

### 3.1 Resource group name

- Resource type: `Microsoft.Resources/resourceGroups`.  
- Rules (summarized):  
  - 1–90 characters.  
  - Letters, numbers, parentheses, periods, hyphens, underscores.  
  - No trailing period.

**Example value:**

```hcl
name = "example-resources"
```

- Length: `"example-resources"` is well within 1–90 ✔  
- Characters: letters + hyphen ✔  
- No trailing period ✔  

Resource group name passes Azure’s rules.

---

### 3.2 Storage account name

- Resource type: `Microsoft.Storage/storageAccounts`.  
- Rules (summarized):  
  - 3–24 characters.  
  - Lowercase only.  
  - Alphanumeric only.  
  - Globally unique.

**Example value:**

```hcl
name = "examplestorageacc"
```

- Length: count characters → within 3–24 ✔  
- Case: all lowercase ✔  
- Characters: letters only (no digits, no hyphens) ✔  
- Global uniqueness:  
  - In a real deployment, Azure would enforce this.  
  - For a sample, the name is structurally valid; uniqueness is assumed.

Storage account name passes Azure’s platform rules.

---

## 4. Cloud Adoption Framework (CAF) naming guidance

Here we’re checking “does this *look* like a good Azure name?” rather than “is it strictly allowed?”

### 4.1 Resource group

CAF often recommends:

- Including environment, workload, region, and resource type.  
- Using hyphens as separators.  

`example-resources` is:

- Generic but acceptable for a simple sample.  
- You might improve it in real docs (e.g., `rg-example-eastus`), but it’s not wrong.

### 4.2 Storage account

CAF guidance for storage accounts:

- Often uses a pattern like:  
  - `<org><app><env><region><type>`  
- Must still obey platform rules (lowercase, alphanumeric, length).

`examplestorageacc`:

- Reads as “example storage account.”  
- Conforms to lowercase + alphanumeric.  
- For a sample, it’s fine; in production, you’d likely shorten and encode more meaning.

From a documentation standpoint, this is acceptable for an introductory example.

---

## 5. Dependencies and references

Check that references are wired correctly.

```hcl
resource_group_name = azurerm_resource_group.example.name
location            = azurerm_resource_group.example.location
```

- `azurerm_resource_group.example` is defined above.  
- Attribute references (`.name`, `.location`) are valid.  
- Implicit dependency is established via interpolation.

No dependency issues.

---

## 6. Deployability assessment

Putting it all together:

- **Terraform schema:**  
  - All required arguments present.  
  - No invalid values.  
  - Provider and resource types are correct.

- **Azure naming rules:**  
  - Resource group name valid.  
  - Storage account name valid.  
  - No illegal characters or lengths.

- **CAF guidance:**  
  - Names are simple but acceptable for examples.  
  - Could be made more descriptive in production, but not required here.

- **Other considerations:**  
  - Region `East US` is valid.  
  - Replication type `GRS` is valid.  
  - No obvious blockers to deployment.

Conclusion: this example is **deployable as written** and passes the full validation workflow.

---

## 7. How this maps to the five pages

- **Page 1 (Workflow):**  
  - This followed the unified process: Registry → ARM rules → CAF → final validation.

- **Page 2 (Azure naming rules):**  
  - Applied resource group and storage account rules.

- **Page 3 (Registry mapping):**  
  - Used the correct Registry pages for `azurerm_resource_group` and `azurerm_storage_account`.

- **Page 4 (Registry validation guide):**  
  - Checked required arguments, Terraform‑enforced lowercase, valid replication types, and common pitfalls.

- **Page 5 (checklists + quick‑reference):**  
  - Used the general and Azure‑specific checklists.  
  - Cross‑checked naming against the quick‑reference table.


