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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>在部署期間使用金鑰保存庫 toopass 安全的參數值

當您需要做為參數的 toopass 安全的值 （例如密碼） 在部署期間時，您可以擷取從 hello 值[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。 您可以參考 hello 金鑰保存庫和參數檔案中的密碼擷取 hello 值。 hello 值絕不會公開，因為您只能參考其金鑰保存庫識別碼。 您不需要 toomanually 輸入 hello 值 hello 密碼每次部署 hello 資源。 hello 金鑰保存庫可以存在於不同的訂用帳戶，於您要部署的 hello 資源群組中。 當參考 hello 金鑰保存庫，您會加入 hello 訂用帳戶 id。

在建立 hello 金鑰保存庫時，設定 hello *enabledForTemplateDeployment*屬性太*true*。 藉由設定此值 tootrue，您允許存取從資源管理員範本部署期間。  

## <a name="deploy-a-key-vault-and-secret"></a>部署金鑰保存庫和密碼

toocreate 金鑰保存庫和密碼，請使用 Azure CLI 或 PowerShell。 請注意該 hello 金鑰保存庫都可使用範本部署。 

對於 Azure CLI，請使用：

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

對於 PowerShell，請使用：

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>啟用存取 toohello 密碼

不論您使用新的金鑰保存庫或其中一個現有，請確定該部署 hello 範本的 hello 使用者可以存取 hello 密碼。 部署範本參考密碼的 hello 使用者必須擁有 hello `Microsoft.KeyVault/vaults/deploy/action` hello 金鑰保存庫的權限。 hello[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)和[參與者](../active-directory/role-based-access-built-in-roles.md#contributor)這兩種角色會授與此存取權。 您也可以建立[自訂角色](../active-directory/role-based-access-control-custom-roles.md)，授與此權限，並新增 hello 使用者 toothat 角色。 如需新增使用者 tooa 角色資訊，請參閱[tooadministrator 角色在 Azure Active Directory 中的指派給使用者](../active-directory/active-directory-users-assign-role-azure-portal.md)。


## <a name="reference-a-secret-with-static-id"></a>使用靜態識別碼參考密碼

收到金鑰保存庫密碼的 hello 範本就像任何其他範本。 這是因為**參考 hello hello 參數檔案，不是 hello 範本中的金鑰保存庫。** 例如，下列範本的 hello 部署 SQL 資料庫，其中包含系統管理員密碼。 hello 密碼參數是設定 tooa 安全字串。 但是，hello 範本未指定這個值來自何處。

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

現在，建立 hello 上述範本參數檔案。 在 hello 參數檔案中，指定符合 hello hello 範本中的 hello 參數名稱的參數。 Hello 參數值，參考 hello hello 金鑰保存庫中的密碼。 您藉由傳遞 hello hello 金鑰保存庫資源識別碼和密碼 hello hello 名稱參考 hello 密碼。 在下列範例的 hello，hello 金鑰保存庫密碼必須已經存在，而且您提供靜態值其資源 id。

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

## <a name="reference-a-secret-with-dynamic-id"></a>使用動態識別碼參考密碼

hello 上一節示範了如何 toopass 靜態資源識別碼 hello 金鑰保存庫密碼。 不過，在某些情況下，您需要 tooreference 而異的依據目前部署的 hello 金鑰保存庫密碼。 在此情況下，您不能在 hello 參數檔案中的硬式編碼 hello 資源識別碼。 不幸的是，您無法以動態方式產生 hello 資源識別碼 hello 參數檔案中因為 hello 參數檔案中不允許範本運算式。

toodynamically 產生金鑰保存庫密碼 hello 的資源 ID，您必須將移到巢狀範本需要 hello 密碼的 hello 資源。 在主要範本中，加入 hello 巢狀的樣板和傳入的參數，包含 hello 動態產生的資源識別碼。

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

## <a name="next-steps"></a>後續步驟
* 如需金鑰保存庫的一般資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。
* 如需參考金鑰密碼的完整範例，請參閱 [金鑰保存庫範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。

