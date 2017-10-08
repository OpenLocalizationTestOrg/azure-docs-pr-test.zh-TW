---
title: "使用資源管理員範本 aaaKey 保存庫密碼 |Microsoft 文件"
description: "顯示如何 toopass 密碼，以從金鑰保存庫做為參數在部署期間。"
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
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="82836-103">在部署期間使用金鑰保存庫 toopass 安全的參數值</span><span class="sxs-lookup"><span data-stu-id="82836-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="82836-104">當您需要做為參數的 toopass 安全的值 （例如密碼） 在部署期間時，您可以擷取從 hello 值[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="82836-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="82836-105">您可以參考 hello 金鑰保存庫和參數檔案中的密碼擷取 hello 值。</span><span class="sxs-lookup"><span data-stu-id="82836-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="82836-106">hello 值絕不會公開，因為您只能參考其金鑰保存庫識別碼。</span><span class="sxs-lookup"><span data-stu-id="82836-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="82836-107">您不需要 toomanually 輸入 hello 值 hello 密碼每次部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="82836-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="82836-108">hello 金鑰保存庫可以存在於不同的訂用帳戶，於您要部署的 hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="82836-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="82836-109">當參考 hello 金鑰保存庫，您會加入 hello 訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="82836-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="82836-110">在建立 hello 金鑰保存庫時，設定 hello *enabledForTemplateDeployment*屬性太*true*。</span><span class="sxs-lookup"><span data-stu-id="82836-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="82836-111">藉由設定此值 tootrue，您允許存取從資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="82836-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="82836-112">部署金鑰保存庫和密碼</span><span class="sxs-lookup"><span data-stu-id="82836-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="82836-113">toocreate 金鑰保存庫和密碼，請使用 Azure CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="82836-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="82836-114">請注意該 hello 金鑰保存庫都可使用範本部署。</span><span class="sxs-lookup"><span data-stu-id="82836-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="82836-115">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="82836-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="82836-116">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="82836-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="82836-117">啟用存取 toohello 密碼</span><span class="sxs-lookup"><span data-stu-id="82836-117">Enable access toohello secret</span></span>

<span data-ttu-id="82836-118">不論您使用新的金鑰保存庫或其中一個現有，請確定該部署 hello 範本的 hello 使用者可以存取 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="82836-119">部署範本參考密碼的 hello 使用者必須擁有 hello `Microsoft.KeyVault/vaults/deploy/action` hello 金鑰保存庫的權限。</span><span class="sxs-lookup"><span data-stu-id="82836-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="82836-120">hello[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)和[參與者](../active-directory/role-based-access-built-in-roles.md#contributor)這兩種角色會授與此存取權。</span><span class="sxs-lookup"><span data-stu-id="82836-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="82836-121">您也可以建立[自訂角色](../active-directory/role-based-access-control-custom-roles.md)，授與此權限，並新增 hello 使用者 toothat 角色。</span><span class="sxs-lookup"><span data-stu-id="82836-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="82836-122">如需新增使用者 tooa 角色資訊，請參閱[tooadministrator 角色在 Azure Active Directory 中的指派給使用者](../active-directory/active-directory-users-assign-role-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="82836-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="82836-123">使用靜態識別碼參考密碼</span><span class="sxs-lookup"><span data-stu-id="82836-123">Reference a secret with static ID</span></span>

<span data-ttu-id="82836-124">收到金鑰保存庫密碼的 hello 範本就像任何其他範本。</span><span class="sxs-lookup"><span data-stu-id="82836-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="82836-125">這是因為**參考 hello hello 參數檔案，不是 hello 範本中的金鑰保存庫。**</span><span class="sxs-lookup"><span data-stu-id="82836-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="82836-126">例如，下列範本的 hello 部署 SQL 資料庫，其中包含系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="82836-127">hello 密碼參數是設定 tooa 安全字串。</span><span class="sxs-lookup"><span data-stu-id="82836-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="82836-128">但是，hello 範本未指定這個值來自何處。</span><span class="sxs-lookup"><span data-stu-id="82836-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="82836-129">現在，建立 hello 上述範本參數檔案。</span><span class="sxs-lookup"><span data-stu-id="82836-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="82836-130">在 hello 參數檔案中，指定符合 hello hello 範本中的 hello 參數名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="82836-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="82836-131">Hello 參數值，參考 hello hello 金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="82836-132">您藉由傳遞 hello hello 金鑰保存庫資源識別碼和密碼 hello hello 名稱參考 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="82836-133">在下列範例的 hello，hello 金鑰保存庫密碼必須已經存在，而且您提供靜態值其資源 id。</span><span class="sxs-lookup"><span data-stu-id="82836-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="82836-134">使用動態識別碼參考密碼</span><span class="sxs-lookup"><span data-stu-id="82836-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="82836-135">hello 上一節示範了如何 toopass 靜態資源識別碼 hello 金鑰保存庫密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="82836-136">不過，在某些情況下，您需要 tooreference 而異的依據目前部署的 hello 金鑰保存庫密碼。</span><span class="sxs-lookup"><span data-stu-id="82836-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="82836-137">在此情況下，您不能在 hello 參數檔案中的硬式編碼 hello 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="82836-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="82836-138">不幸的是，您無法以動態方式產生 hello 資源識別碼 hello 參數檔案中因為 hello 參數檔案中不允許範本運算式。</span><span class="sxs-lookup"><span data-stu-id="82836-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="82836-139">toodynamically 產生金鑰保存庫密碼 hello 的資源 ID，您必須將移到巢狀範本需要 hello 密碼的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="82836-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="82836-140">在主要範本中，加入 hello 巢狀的樣板和傳入的參數，包含 hello 動態產生的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="82836-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82836-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82836-141">Next steps</span></span>
* <span data-ttu-id="82836-142">如需金鑰保存庫的一般資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="82836-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="82836-143">如需參考金鑰密碼的完整範例，請參閱 [金鑰保存庫範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。</span><span class="sxs-lookup"><span data-stu-id="82836-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

