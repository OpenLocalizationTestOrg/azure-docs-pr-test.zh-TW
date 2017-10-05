---
title: "在 Azure 容器執行個體中掛接 Azure 檔案磁碟區"
description: "了解如何掛接 Azure 檔案磁碟區來保存 Azure 容器執行個體的狀態"
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
ms.openlocfilehash: 4248a3769ba8a0fb067b3904d55d487fe67e5778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="67646-103">使用 Azure 容器執行個體來掛接 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="67646-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="67646-104">根據預設，Azure 容器執行個體都是無狀態的。</span><span class="sxs-lookup"><span data-stu-id="67646-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="67646-105">如果容器損毀或停止，其所有狀態都會遺失。</span><span class="sxs-lookup"><span data-stu-id="67646-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="67646-106">若要在容器超過存留期後保存其狀態，您必須從外部存放區掛接磁碟區。</span><span class="sxs-lookup"><span data-stu-id="67646-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="67646-107">本文說明如何掛接 Azure 檔案共用以便與 Azure 容器執行個體搭配使用。</span><span class="sxs-lookup"><span data-stu-id="67646-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="67646-108">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="67646-108">Create an Azure file share</span></span>

<span data-ttu-id="67646-109">在搭配使用 Azure 檔案共用與 Azure 容器執行個體前，您必須先建立 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="67646-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="67646-110">請執行下列指令碼來建立儲存體帳戶，以裝載檔案共用和共用本身。</span><span class="sxs-lookup"><span data-stu-id="67646-110">Run the following script to create a storage account to host the file share and the share itself.</span></span> <span data-ttu-id="67646-111">請注意，儲存體帳戶名稱必須是全域唯一的，因此指令碼會在基底字串中加上隨機值。</span><span class="sxs-lookup"><span data-stu-id="67646-111">Note that the storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="67646-112">取得儲存體帳戶的存取詳細資料</span><span class="sxs-lookup"><span data-stu-id="67646-112">Acquire storage account access details</span></span>

<span data-ttu-id="67646-113">若要在 Azure 容器執行個體中掛接 Azure 檔案共用來作為磁碟區，您需要三個值：儲存體帳戶名稱、共用名稱和儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="67646-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span> 

<span data-ttu-id="67646-114">如果您使用上述指令碼，所建立的儲存體帳戶名稱尾端會加上隨機值。</span><span class="sxs-lookup"><span data-stu-id="67646-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="67646-115">若要查詢最終字串 (包括隨機部分)，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="67646-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="67646-116">我們已知道共用名稱 (在上述指令碼中是 acishare)，因此只差儲存體帳戶金鑰，此金鑰可以使用下列命令來找到：</span><span class="sxs-lookup"><span data-stu-id="67646-116">The share name is already known (it is *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="67646-117">使用 Azure 金鑰保存庫來儲存儲存體帳戶的存取詳細資料</span><span class="sxs-lookup"><span data-stu-id="67646-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="67646-118">儲存體帳戶金鑰可保護資料的存取，因此建議您將金鑰儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="67646-118">Storage account keys protect access to your data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="67646-119">使用 Azure CLI 來建立金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="67646-119">Create a key vault with the Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="67646-120">在部署時，`enabled-for-template-deployment` 參數可讓 Azure Resource Manager 從金鑰保存庫提取祕密。</span><span class="sxs-lookup"><span data-stu-id="67646-120">The `enabled-for-template-deployment` switch allows Azure Resource Manager to pull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="67646-121">將儲存體帳戶金鑰儲存為金鑰保存庫中的新祕密：</span><span class="sxs-lookup"><span data-stu-id="67646-121">Store the storage account key as a new secret in the key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-the-volume"></a><span data-ttu-id="67646-122">掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="67646-122">Mount the volume</span></span>

<span data-ttu-id="67646-123">在容器中掛接 Azure 檔案共用來作為磁碟區的程序需要兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="67646-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="67646-124">首先，您要提供共用的詳細資料，以在定義容器群組時輸入，然後您要指定您想要如何在群組的一或多個容器內掛接磁碟區。</span><span class="sxs-lookup"><span data-stu-id="67646-124">First, you provide the details of the share as part of defining the container group, then you specify how you want the volume mounted within one or more of the containers in the group.</span></span>

<span data-ttu-id="67646-125">若要定義想要可供掛接的磁碟區，請將 `volumes` 陣列新增到 Azure Resource Manager 範本中的容器群組定義，然後在個別容器的定義中參考這些磁碟區。</span><span class="sxs-lookup"><span data-stu-id="67646-125">To define the volumes you want to make available for mounting, add a `volumes` array to the container group definition in the Azure Resource Manager template, then reference them in the definition of the individual containers.</span></span>

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

<span data-ttu-id="67646-126">範本中會納入儲存體帳戶名稱和金鑰來作為參數，並可在不同的參數檔案中提供。</span><span class="sxs-lookup"><span data-stu-id="67646-126">The template includes the storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="67646-127">若要填入參數檔案，您需要三個值：儲存體帳戶名稱、Azure 金鑰保存庫的資源識別碼，以及您用來儲存儲存體金鑰的金鑰保存庫祕密名稱。</span><span class="sxs-lookup"><span data-stu-id="67646-127">To populate the parameters file, you will need three values: the storage account name, the resource ID of your Azure key vault, and the key vault secret name that you used to store the storage key.</span></span> <span data-ttu-id="67646-128">如果您有遵循上述步驟，您可以使用下列指令碼取得這些值：</span><span class="sxs-lookup"><span data-stu-id="67646-128">If you have followed previous steps, you can get these values with the following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="67646-129">將這些值插入參數檔案中：</span><span class="sxs-lookup"><span data-stu-id="67646-129">Insert the values into the parameters file:</span></span>

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

## <a name="deploy-the-container-and-manage-files"></a><span data-ttu-id="67646-130">部署容器及管理檔案</span><span class="sxs-lookup"><span data-stu-id="67646-130">Deploy the container and manage files</span></span>

<span data-ttu-id="67646-131">透過定義的範本，您可以使用 Azure CLI 建立容器並掛接其磁碟區。</span><span class="sxs-lookup"><span data-stu-id="67646-131">With the template defined, you can create the container and mount its volume using the Azure CLI.</span></span> <span data-ttu-id="67646-132">假設範本檔案的名稱為 azuredeploy.json，參數檔案的名稱為 azuredeploy.parameters.json，則命令列如下：</span><span class="sxs-lookup"><span data-stu-id="67646-132">Assuming that the template file is named *azuredeploy.json* and that the parameters file is named *azuredeploy.parameters.json*, then the command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="67646-133">一旦啟動容器，您即可使用透過 **seanmckenna/aci-hellofiles** 映像部署的簡單 Web 應用程式，以管理位於指定掛接路徑之 Azure 檔案共用中的檔案。</span><span class="sxs-lookup"><span data-stu-id="67646-133">Once the container starts up, you can use the simple web app deployed via the **seanmckenna/aci-hellofiles** image, to the manage files in the Azure file share at the mount path that you specified.</span></span> <span data-ttu-id="67646-134">透過下列操作取得 Web 應用程式的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="67646-134">Obtain the ip address for the web app via the following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="67646-135">您可以使用像 [Microsoft Azure 儲存體總管](http://storageexplorer.com)這類工具擷取及檢查寫入至檔案共用的檔案。</span><span class="sxs-lookup"><span data-stu-id="67646-135">You can use a tool like the [Microsoft Azure Storage Explorer](http://storageexplorer.com) to retrieve and inspect the file writen to the file share.</span></span>

>[!NOTE]
> <span data-ttu-id="67646-136">若要深入了解如何使用 Azure Resource Manager 範本、參數檔案以及使用 Azure CLI 進行部署，請參閱[使用 Resource Manager 範本與 Azure CLI 部署資源](../azure-resource-manager/resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="67646-136">To learn more about using Azure Resource Manager templates, parameter files, and deploying with the Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67646-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67646-137">Next steps</span></span>

- <span data-ttu-id="67646-138">使用 Azure 容器執行個體部署您的第一個容器[快速入門](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="67646-138">Deploy for your first container using the Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="67646-139">了解 [Azure 容器執行個體與容器 Orchestrator 之間的關聯性](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="67646-139">Learn about the [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
