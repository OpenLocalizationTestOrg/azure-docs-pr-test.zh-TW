---
title: "aaaMounting Azure 容器執行個體中的 Azure 檔案磁碟區"
description: "了解如何 toomount Azure 檔案磁碟區 toopersist 狀態時，使用 Azure 容器執行個體"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>使用 Azure 容器執行個體來掛接 Azure 檔案共用

根據預設，Azure 容器執行個體都是無狀態的。 如果 hello 容器損毀或停止時，它的所有狀態都會遺失。 toopersist 狀態到超出 hello 存留期間 hello 容器，您必須從外部存放區來掛接磁碟區。 本文將說明如何 toomount Azure 的檔案共用 Azure 容器執行個體搭配使用。

## <a name="create-an-azure-file-share"></a>建立 Azure 檔案共用

在搭配使用 Azure 檔案共用與 Azure 容器執行個體前，您必須先建立 Azure 檔案共用。 執行下列指令碼 toocreate hello 的儲存體帳戶 toohost hello 檔案共用和 hello 共用本身。 請注意該 hello 儲存體帳戶名稱必須是全域唯一的因此 hello 指令碼會新增的隨機值 toohello 基底的字串。

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>取得儲存體帳戶的存取詳細資料

toomount Azure 容器執行個體在 Azure 的檔案共用做為磁碟區，您需要三個值： hello 儲存體帳戶名稱、 hello 共用名稱和 hello 儲存體存取金鑰。 

如果您使用上述的 hello 指令碼，在 hello 結尾隨機的值建立 hello 儲存體帳戶名稱。 tooquery hello 最終字串 （包括 hello 隨機部分），請使用下列命令的 hello:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

hello 共用名稱，就已經知道 (它是*acishare*上述 hello 指令碼中)，因此會維持為 hello 儲存體帳戶金鑰，您可以使用找到的所有 hello 下列命令：

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>使用 Azure 金鑰保存庫來儲存儲存體帳戶的存取詳細資料

儲存體帳戶金鑰保護存取 tooyour 資料，因此我們建議您將其儲存在 Azure 金鑰保存庫。 

建立金鑰保存庫以 hello Azure CLI:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

hello`enabled-for-template-deployment`參數允許 Azure 資源管理員 toopull 從金鑰保存庫密碼在部署階段。

存放區 hello 儲存體帳戶金鑰做為 hello 金鑰保存庫中的新密碼：

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>掛接 hello 磁碟區

在容器中掛接 Azure 檔案共用來作為磁碟區的程序需要兩個步驟。 首先，您提供定義 hello 容器群組的一部分的 hello 共用 hello 詳細資料，接著，您可以指定您想掛接一個或多個 hello 群組中的 hello 容器內的 hello 磁碟區的方式。

您想要裝載、 toomake 可用 toodefine hello 磁碟區加入`volumes`陣列 toohello 容器群組定義在 hello Azure Resource Manager 範本中，然後在 hello hello 個別容器定義中參考它們。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

hello 範本包含 hello 儲存體帳戶名稱和金鑰做為參數，可提供不同的參數檔案中。 toopopulate hello 參數檔案，您將需要三個值： hello 儲存體帳戶名稱、 hello Azure 金鑰保存庫、 資源識別碼和 hello 您使用 toostore hello 儲存體金鑰的金鑰保存庫秘密名稱。 如果您有遵循上述步驟，您可以使用下列指令碼的 hello 取得這些值：

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

插入 hello 參數檔案中的 hello 值：

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>部署 hello 容器及管理檔案

Hello 範本定義時，您可以建立 hello 容器，並使用 Azure CLI hello 其磁碟區裝載。 假設 hello 範本檔案會命名為*azuredeploy.json* hello 參數檔案稱為*azuredeploy.parameters.json*，則 hello 命令列是：

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

一旦 hello 容器啟動時，您可以使用 hello 簡單 web 應用程式透過 hello 部署**seanmckenna/aci-hellofiles**映像，toohello 管理 hello Azure 檔案共用，在您指定的 hello 掛接路徑中的檔案。 取得 hello hello web 應用程式透過 hello 下列的 ip 位址：

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

您可以使用這類工具 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)tooretrieve 並檢查 hello 檔案寫入 toohello 檔案共用。

>[!NOTE]
> 請參閱深入了解使用 Azure Resource Manager 範本參數檔案和部署以 hello Azure CLI toolearn[部署資源，資源管理員範本與 Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)。

## <a name="next-steps"></a>後續步驟

- 部署您使用 hello Azure 容器執行個體的第一個容器[快速入門](container-instances-quickstart.md)
- 深入了解 hello[容器 orchestrators Azure 容器執行個體之間的關聯性](container-instances-orchestrator-relationship.md)
