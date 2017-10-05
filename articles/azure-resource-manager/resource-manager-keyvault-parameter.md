---
title: "金鑰保存庫密碼與 Resource Manager 範本 | Microsoft Docs"
description: "示範如何在部署期間從金鑰保存庫中傳遞密碼做為參數。"
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 1ca72599e67e79d42a3d430dbb13e89ea7265334
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="376dd-103">在部署期間使用 Key Vault 以傳送安全的參數值</span><span class="sxs-lookup"><span data-stu-id="376dd-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="376dd-104">當您需要在部署期間，傳送安全值 (例如密碼) 做為參數時，您可以從 [Azure Key Vault](../key-vault/key-vault-whatis.md) 擷取值。</span><span class="sxs-lookup"><span data-stu-id="376dd-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="376dd-105">您可以藉由參考金鑰保存庫和參數檔案中的密碼來擷取值。</span><span class="sxs-lookup"><span data-stu-id="376dd-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="376dd-106">您只參考其金鑰保存庫識別碼，因此該值絕不會公開。</span><span class="sxs-lookup"><span data-stu-id="376dd-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="376dd-107">您不需要在每次部署資源時手動輸入密碼的值。</span><span class="sxs-lookup"><span data-stu-id="376dd-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="376dd-108">金鑰保存庫可以存在於與您部署的資源群組的不同訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="376dd-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="376dd-109">當參考金鑰保存庫時，您納入訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="376dd-110">建立金鑰保存庫時，將 *enabledForTemplateDeployment* 屬性設定為 *true*。</span><span class="sxs-lookup"><span data-stu-id="376dd-110">When creating the key vault, set the *enabledForTemplateDeployment* property to *true*.</span></span> <span data-ttu-id="376dd-111">將此值設定為 true，即表示您允許在部署期間從 Resource Manager 範本存取。</span><span class="sxs-lookup"><span data-stu-id="376dd-111">By setting this value to true, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="376dd-112">部署金鑰保存庫和密碼</span><span class="sxs-lookup"><span data-stu-id="376dd-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="376dd-113">若要建立金鑰保存庫與密碼，請使用 Azure CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="376dd-113">To create a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="376dd-114">請注意，金鑰保存庫會針對範本部署啟用。</span><span class="sxs-lookup"><span data-stu-id="376dd-114">Notice that the key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="376dd-115">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="376dd-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="376dd-116">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="376dd-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="376dd-117">啟用密碼的存取權</span><span class="sxs-lookup"><span data-stu-id="376dd-117">Enable access to the secret</span></span>

<span data-ttu-id="376dd-118">不論您使用新的金鑰保存庫或現有的金鑰保存庫，請確定使用者部署的範本可以存取密碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-118">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="376dd-119">部署範本以參考密碼的使用者必須具有金鑰保存庫的 `Microsoft.KeyVault/vaults/deploy/action` 權限。</span><span class="sxs-lookup"><span data-stu-id="376dd-119">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="376dd-120">[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)和[參與者](../active-directory/role-based-access-built-in-roles.md#contributor)角色皆可授與此權限。</span><span class="sxs-lookup"><span data-stu-id="376dd-120">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="376dd-121">您也可以建立會授與此權限的[自訂角色](../active-directory/role-based-access-control-custom-roles.md)，並將使用者新增至該角色。</span><span class="sxs-lookup"><span data-stu-id="376dd-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="376dd-122">如需有關將使用者新增至角色的資訊，請參閱[在 Azure Active Directory 中將使用者指派給系統管理員角色](../active-directory/active-directory-users-assign-role-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="376dd-122">For information about adding a user to a role, see [Assign a user to administrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="376dd-123">使用靜態識別碼參考密碼</span><span class="sxs-lookup"><span data-stu-id="376dd-123">Reference a secret with static ID</span></span>

<span data-ttu-id="376dd-124">接收金鑰保存庫密碼的範本與其他任何範本都很像。</span><span class="sxs-lookup"><span data-stu-id="376dd-124">The template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="376dd-125">這是因為**您參考了參數檔案中的金鑰保存庫，而非範本。**</span><span class="sxs-lookup"><span data-stu-id="376dd-125">That's because **you reference the key vault in the parameter file, not the template.**</span></span> <span data-ttu-id="376dd-126">例如，下列範本部署了包含系統管理員密碼的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="376dd-126">For example, the following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="376dd-127">密碼參數會設定為安全字串。</span><span class="sxs-lookup"><span data-stu-id="376dd-127">The password parameter is set to a secure string.</span></span> <span data-ttu-id="376dd-128">但是，範本並未指定該值來自何處。</span><span class="sxs-lookup"><span data-stu-id="376dd-128">But, the template does not specify where that value comes from.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

<span data-ttu-id="376dd-129">現在，請為前述範本建立參數檔案。</span><span class="sxs-lookup"><span data-stu-id="376dd-129">Now, create a parameter file for the preceding template.</span></span> <span data-ttu-id="376dd-130">在參數檔案中，指定符合範本中參數名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="376dd-130">In the parameter file, specify a parameter that matches the name of the parameter in the template.</span></span> <span data-ttu-id="376dd-131">針對參數值，參考來自金鑰保存庫的密碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-131">For the parameter value, reference the secret from the key vault.</span></span> <span data-ttu-id="376dd-132">您可以藉由傳遞金鑰保存庫的資源識別碼和密碼的名稱來參考密碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-132">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="376dd-133">在下列範例中，金鑰保存庫密碼必須已經存在，而且您要針對其資源識別碼提供靜態值。</span><span class="sxs-lookup"><span data-stu-id="376dd-133">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="376dd-134">使用動態識別碼參考密碼</span><span class="sxs-lookup"><span data-stu-id="376dd-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="376dd-135">上一節已說明如何傳遞金鑰保存庫密碼的靜態資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-135">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="376dd-136">不過，在某些情況下，您需要參考會隨目前的部署而變化的金鑰保存庫密碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-136">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="376dd-137">在該情況下，您將無法在參數檔中硬式編碼資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-137">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="376dd-138">不幸的是，因為參數檔中不允許使用範本運算式，因此您無法在參數檔中以動態方式產生資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="376dd-138">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="376dd-139">若要以動態方式產生金鑰保存庫密碼的資源識別碼，您必須將需要密碼的資源移動到巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="376dd-139">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="376dd-140">在主要範本中，您必須新增巢狀範本，並傳入包含動態產生的資源識別碼的參數。</span><span class="sxs-lookup"><span data-stu-id="376dd-140">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a><span data-ttu-id="376dd-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="376dd-141">Next steps</span></span>
* <span data-ttu-id="376dd-142">如需金鑰保存庫的一般資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="376dd-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="376dd-143">如需參考金鑰密碼的完整範例，請參閱 [金鑰保存庫範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。</span><span class="sxs-lookup"><span data-stu-id="376dd-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

