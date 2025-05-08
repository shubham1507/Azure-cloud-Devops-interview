1. Explain the structure of an ARM template. What are the main sections it contains?

parameters, resources, outputs, variables, $schema, contentVersion

2.What is the purpose of the parameters and variables sections in an ARM template?

Parameters accept input values at deployment, and variables store reusable values.


Overall explanation
Parameters allow input values (e.g., VM size) to be passed at deployment, while variables store reusable values (e.g., defining a location to avoid repetition).

3.How do you define dependencies between resources in an ARM template?

Using the dependsOn attribute to ensure resources are deployed in order.


dependsOn ensures that a resource (e.g., a VM) is deployed only after its dependent resource (e.g., a virtual network) is successfully deployed.

4.How is ARM template validation performed before deployment?

az deployment validate

5.What are resource locks in ARM, and how do they work?

Prevent accidental deletion or modification using CanNotDelete or ReadOnly locks.

6. Explain the difference between ARM templates and Azure Bicep.

ARM templates use JSON, while Bicep is a more concise declarative language that compiles to ARM.

7.What is the purpose of a deploymentMode parameter in ARM templates?

Defines whether the deployment is Incremental (default) or Complete.

8. How do you deploy an ARM template using Azure PowerShell?


New-AzResourceGroupDeployment -ResourceGroupName myResourceGroup -TemplateFile template.json

Overall explanation
The correct Azure PowerShell command for deploying an ARM template is New-AzResourceGroupDeployment.

9.How do you deploy an ARM template using Azure CLI?

az deployment group create --resource-group myResourceGroup --template-file template.json

Overall explanation
The Azure CLI command for deploying ARM templates is az deployment group create.

10.Explain the process of deploying ARM templates through Azure DevOps Pipelines.

Overall explanation
Azure DevOps Pipelines support ARM template deployment using the AzureResourceManagerTemplateDeployment@3 task in YAML pipelines.

11.How do you manage multiple environments (Dev, QA, Prod) using ARM templates?

Use parameter files like parameters.dev.json, parameters.prod.json for each environment.
Overall explanation
Parameter files allow environment-specific configurations without modifying the main ARM template, ensuring 
consistency.

12. What is the role of linked templates in ARM? How are they implemented?

They enable modular deployments using the templateLink property in the main template.

13. How do you handle secrets (e.g., passwords, keys) in ARM templates securely?

Use Azure Key Vault references in the ARM template’s parameters section.

14. Explain how to use conditionals in an ARM template to deploy optional resources.

Use the condition property in resource definitions.

15.What is a nested template in ARM? Provide an example of its use.

A nested template is an ARM template embedded within another ARM template for modularization.

16.How do you update existing resources using ARM templates?
Deploy the ARM template in incremental mode with updated configurations.

17.How can you roll back a failed deployment using ARM templates?
Redeploy the last working template or enable deployment history with Azure Policy.

18. How do you troubleshoot a failed ARM template deployment?

Check deployment logs in the Azure Portal or use az deployment group show.

19. What does the error "ResourceNotFound" indicate during an ARM deployment, and how do you resolve it?
The resource does not exist; verify dependencies and ensure the resource exists.


20. How do you analyze and debug the deployment logs for an ARM template?
Use Azure Activity Log or az deployment group operation list.

21. How do you deal with circular dependency errors in ARM templates?
Use dependsOn correctly to break the cycle.

22. How do you ensure that ARM templates are idempotent?
Design templates to create or update resources without duplication.

23. How do you modularize large ARM templates for better manageability?
Split them into linked templates using templateLink.

24. What is the purpose of using the outputs section in ARM templates?
It returns values like resource IDs, connection strings, or IP addresses after deployment.


25. How do you handle resource naming conventions in ARM templates?
Overall explanation
Dynamic naming using concat() and uniqueString() ensures consistency across deployments.

26.What are ARM template functions, and how are they used? Provide examples of commonly used functions.
Functions perform operations like concat(), resourceId(), and uniqueString().

27. How do you integrate ARM template deployments in Azure DevOps release pipelines?
Overall explanation
The Azure Resource Group Deployment task automates ARM template deployment in Azure DevOps release pipelines.

28. How do you validate ARM templates automatically in Azure DevOps?
Use az deployment validate in the pipeline script.

29. How can you automate the deployment of ARM templates for a CI/CD pipeline?
Link the template in a YAML pipeline and set triggers.

Overall explanation
CI/CD pipelines automate ARM deployments by triggering deployments on commits/merges.

30. How do you perform testing for ARM templates before deployment in Azure DevOps?
Deploy to a test environment or run validation scripts in Azure DevOps pipelines.

31. How do you implement a "blue-green deployment" strategy using ARM templates?
Create two identical environments and swap traffic between them.

32. Explain how to create a Virtual Machine Scale Set (VMSS) using ARM templates.
Use Microsoft.Compute/virtualMachineScaleSets in the ARM template.

33. How do you create and deploy custom roles and policies using ARM templates?
Assign roles manually after deployment.

34. What are management groups, and how do you use them in ARM templates?
Management groups organize subscriptions using Microsoft.Management/managementGroups.

35. How do you deploy multiple regions simultaneously using an ARM template?
Use a copy loop with region parameters.

36. Explain how to configure role-based access control (RBAC) using ARM templates.
Deploy Microsoft.Authorization/roleAssignments.

37. How do you implement Azure Policy definitions and assignments using ARM templates?
Use policyDefinitions and policyAssignments in the ARM template.

38. What is the best way to handle large datasets (e.g., IP address ranges) in an ARM template?
Use external parameter files or reference Azure Key Vault.


39. Describe a scenario where you used ARM templates for infrastructure as code in a production environment.
Deploying an AKS cluster with monitoring and scaling configurations.

40. How have you handled deployment rollbacks using ARM templates?
Redeploy a previous stable template or use incremental mode.

41. Explain a situation where ARM templates helped you reduce deployment time or errors.

Automating repeatable VM provisioning.

42. Have you faced any challenges with scaling infrastructure using ARM templates? How did you resolve them?
Resolved scaling issues by parameterizing instance counts and using VMSS for auto-scaling infrastructure.

43. Share an example of automating resource provisioning using ARM templates in a DevOps pipeline.
Automated resource provisioning by integrating ARM templates into an Azure DevOps pipeline with YAML tasks for deployment.

---------------
Terraform

44. Explain the role of the main.tf, variables.tf, and outputs.tf files in a Terraform project.
main.tf defines resources, variables.tf stores input variables, and outputs.tf returns deployment values.

45. What is the Terraform state file, and why is it important?
The Terraform state file tracks the mapping of resources between the real infrastructure and the configuration. It helps Terraform understand the current state, preventing issues like drift during updates.

46. How do you use Terraform modules, and why are they beneficial?
Use modules for reusable code by referencing them with module "name" { source = "./module-path" }.

47. What is a backend in Terraform? Provide examples of common backends.
A backend stores Terraform state; common examples are local files or remote Azure Blob Storage.

48. Explain the difference between local and remote backends in Terraform.

Local backends store state on disk, while remote backends store it in shared storage like Azure Blob.

49. How do you configure Terraform to deploy resources in Azure?
Configure Terraform for Azure by defining the azurerm provider and authenticating using service principal credentials.

50. How do you manage resource groups in Azure using Terraform?
Manage resource groups using **resource "azure_rm_resource_group" {}`.

51. How do you deploy a Virtual Network (VNet) and subnets in Azure using Terraform?
azurerm_virtual_network and azurerm_subnet 

52. Explain how to provision an Azure Kubernetes Service (AKS) cluster using Terraform.
Overall explanation
Use the azurerm_kubernetes_cluster resource to provision an AKS cluster with configurations for nodes, scaling, and networking.

53. How do you use Terraform to manage Azure Active Directory resources?


Manage Azure AD resources using the azuread provider in Terraform for users, groups, and app registrations.

54. How do you deploy Azure App Services and Azure SQL databases using Terraform?
Deploy App Services and SQL databases using azurerm_app_service and azurerm_sql_database resources.

55. Explain the use of Terraform for multi-region deployments in Azure.

Perform multi-region deployments with variables for regions and a for_each loop in Terraform.

56. How do you manage secrets in Azure Key Vault using Terraform?
Manage secrets in Azure Key Vault using azurerm_key_vault and azurerm_key_vault_secret resources.

57. What are Azure-managed identities, and how can they be configured using Terraform?
Azure-managed identities are created with resources like azurerm_user_assigned_identity and linked to services.

58. What is the difference between a state file (terraform.tfstate) and a state lock?

State files track resources; state locks prevent simultaneous state changes during deployments.

59. How do you enable remote state storage for Terraform in Azure?
Enable remote state storage using Azure Blob by configuring the backend in terraform {}.

60. ********* What happens if the state file gets corrupted? How do you recover from this?
Terraform automatically creates backups of the state file, and terraform refresh helps reconcile the state with actual resources.

61. Explain how you handle shared state across multiple teams in Terraform.

Share state across teams using remote backends with proper locking mechanisms like Azure Blob.

62. How do you import existing Azure resources into Terraform state?

Import Azure resources into Terraform using terraform import <resource> <id>.

63. What is the purpose of a Terraform module? How do you create one?

Terraform modules are reusable resource blocks; create one with a main.tf and use source = "./module-path".

64. How do you handle multiple environments (Dev, QA, Prod) using Terraform workspaces?
Manage environments using workspaces (terraform workspace new dev).


65. Explain how you use input variables and outputs in Terraform modules.
Input variables accept parameters, and outputs share values across modules (e.g., sharing VM IPs).

66. How do you publish and use Terraform modules from the Terraform Registry?

Publish modules to Terraform Registry with versioning and use them via source = "registry/name".

67. What is the difference between count and for_each in Terraform?

count creates identical resources, while for_each customizes resources for specific items.

68. How do you integrate Terraform with Azure DevOps pipelines?

Integrate Terraform with Azure DevOps by adding Terraform tasks in pipelines for provisioning resources.

69. How do you configure Azure DevOps to trigger a Terraform deployment automatically?
Trigger Terraform deployment automatically using pipeline triggers on Git commits.

70. How do you handle secrets in Terraform scripts while using Azure DevOps pipelines?

Handle secrets securely with Azure Key Vault or environment variables referenced in Terraform.

71. Explain how to manage multiple subscriptions in Azure using Terraform and Azure DevOps.
Manage multiple subscriptions by configuring the Azure provider with subscription_id for each environment.

72. What does the error "resource already exists" mean in Terraform, and how do you resolve it?
Ignore the error and continue deployment.


73. How do you handle circular dependencies in Terraform?
Handle circular dependencies by splitting resources or using depends_on to define explicit order.

74. ******* Explain a scenario where you had to debug a Terraform state lock issue.
Debug state lock issues by checking the backend and releasing locks manually if needed.


75. How do you test Terraform code before deploying it to production?
Follow best practices like modularization, parameterization, and clear folder structures.

76. What is the purpose of the .terraform.lock.hcl file?
.terraform.lock.hcl locks provider versions to ensure consistent behavior across deployments.

77. How do you enforce standards and compliance in Terraform code for Azure resources?
Enforce standards with Sentinel policies, Terraform linters, and Azure Policy integrations.


78. ********* What is the purpose of the terraform taint command? When would you use it?
To mark a resource for recreation in the next apply (e.g., fixing a faulty VM).


79. How do you use Terraform dynamic blocks? Provide a real-world example.
Dynamic blocks create conditional nested blocks (e.g., creating subnets based on a variable).

80. Explain how you manage sensitive data using the sensitive argument in Terraform.
The sensitive argument masks output values (e.g., hiding a password in logs).


81. ******How do you handle blue-green or canary deployments using Terraform in Azure?
By creating two environments and swapping traffic with Terraform.


82. **Explain how to create a custom Terraform provider.
Create a custom provider by implementing Terraform’s SDK and writing Go code.

83. Describe a scenario where you used Terraform to automate a large-scale Azure infrastructure deployment.
Used Terraform to deploy VMs, VNets, and load balancers for a production environment in Azure.

84. How have you handled resource dependencies in Terraform for complex Azure environments?
Managed resource dependencies using explicit depends_on or modules for complex setups.

Overall explanation
resource "azurerm_virtual_network" "vnet" {
  name                = "my-vnet"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}
 
resource "azurerm_subnet" "subnet" {
  name                 = "my-subnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  depends_on           = [azurerm_virtual_network.vnet]
}
Here, depends_on ensures the subnet is created after the VNet.

85. Explain a situation where you used Terraform to reduce deployment errors and improve scalability.
Reduced errors by automating AKS deployments with Terraform modules and parameter files.
Overall explanation
Terraform modules for Azure Kubernetes Service (AKS) help maintain consistent configurations across environments:

module "aks" {
  source              = "./modules/aks"
  cluster_name        = "prod-cluster"
  node_count         = 3
  vm_size             = "Standard_D2_v2"
}
This approach reduces manual errors and improves scalability.

86. How have you implemented Terraform for disaster recovery in Azure?
Used Terraform for disaster recovery by replicating resources in another region using templates.

Overall explanation
Terraform can replicate infrastructure in another region for disaster recovery:

resource "azurerm_storage_account" "dr" {
  name                     = "mystorageaccountdr"
  location                 = "westus"
  resource_group_name      = azurerm_resource_group.rg.name
  account_replication_type = "GRS" # Geo-redundant storage
}
This ensures failover readiness.

87. Share an example where Terraform modules helped you simplify resource creation for Azure.

Overall explanation
A VNet module simplifies network creation across multiple environments:

module "network" {
  source     = "./modules/network"
  vnet_name  = "my-vnet"
  location   = "eastus"
  subnet_ids = ["10.0.1.0/24", "10.0.2.0/24"]
}
Modules improve code reusability and reduce duplication.

88. ******How do you ensure that sensitive data (like passwords and keys) is not exposed in Terraform configurations?

Use Azure Key Vault for secret management in Terraform:

resource "azurerm_key_vault_secret" "example" {
  name         = "db-password"
  value        = "supersecret"
  key_vault_id = azurerm_key_vault.example.id
}
This ensures secrets are securely managed.

89. What are Sentinel policies in Terraform, and how do they help in securing infrastructure?
Sentinel policies are Terraform security tools that enforce compliance by validating Terraform plans against security rules.

Overall explanation
A Sentinel policy can restrict deployments to approved regions:

import "tfplan/v2" as tfplan
 
main = rule {
  all tfplan.resource_changes as r {
    r.change.after.location in ["eastus", "westus"]
  }
}
This ensures governance and compliance.

90. How do you audit changes made to infrastructure through Terraform?

Terraform Cloud records logs for every apply, allowing you to track changes in state files and VCS history.

91. How do you restrict users from directly modifying Azure resources managed by Terraform?
Restrict direct changes by enforcing Terraform workflows and locking critical resources.

Overall explanation
Use RBAC and policy enforcement to restrict modifications:

Assign least privilege IAM roles to Terraform users.

Enable state locking to prevent direct resource modifications.


92. How do you integrate Terraform with Azure Policy for governance?
Integrate Terraform with Azure Policy by deploying policy definitions using templates.


Overall explanation
Deploy an Azure Policy with Terraform to enforce tagging standards:

resource "azurerm_policy_definition" "example" {
  name         = "require-tags"
  policy_type  = "Custom"
  display_name = "Require Resource Tags"
 
  policy_rule = <<POLICY
{
  "if": {
    "field": "tags",
    "equals": ""
  },
  "then": {
    "effect": "deny"
  }
}
POLICY
}
This ensures all Azure resources comply with governance policies.


































