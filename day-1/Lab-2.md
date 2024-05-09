#### Lab 2

>Pre-requite : must have an azure subscription. plesase register to [Azure Portal](https://portal.azure.com/#home) and try to get a trial subscription which is free for a month.

1. Go to azure portal and open cloud shell and run below command/script

```bash
#!/usr/bin/env bash

subscription_id="00000000-0000-0000-0000-000000000000" 
az ad sp create-for-rbac --name myServicePrincipalName1 \
    --role reader \
    --scopes /subscriptions/${subscription_id}  #/resourceGroups/${resource_group} 
```
2. Save the results of the above command as they will not shown later in future.
3. Go to azure portal and create below resources manually. (required to store the terraform state file)

```
resource_group_name  = "TerraformStateRG"
storage_account_name = "tfstate1395347833" (adjust the name if needed as this require a global unique name)
container_name       = "tfstate"
```
  
4. Fork [this](https://github.com/hclpandv/terraform-azure-github-actions) repository into your github account.
5. Add the below secrets in repository settings under *secrets and variables->actions* get the values with the help of saved values from step2.

```
CLIENT_ID
CLIENT_SECRET
SUBSCRIPTION_ID
TENANT_ID
```
6. Now go to actions tab in the repository and run the github workflow with the name of *TerraformDeploy*
