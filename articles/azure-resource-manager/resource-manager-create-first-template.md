---
title: "第一個 Azure Resource Manager 範本 aaaCreate |Microsoft 文件"
description: "逐步指南 toocreating 第一個的 Azure Resource Manager 範本。 它會顯示您如何 toouse hello 範本參考儲存體帳戶 toocreate hello 範本。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="dc213-104">建立及部署第一個 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="dc213-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="dc213-105">本主題會引導您建立第一個的 Azure Resource Manager 範本的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="dc213-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="dc213-106">資源管理員範本是定義您的解決方案需 toodeploy hello 資源的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc213-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="dc213-107">請參閱 < 部署和管理 Azure 解決方案，相關聯的 toounderstand hello 概念[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dc213-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="dc213-108">如果您有現有的資源，並想 tooget 範本，這些資源，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="dc213-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="dc213-109">toocreate 和修訂的範本，您需要 JSON 編輯器。</span><span class="sxs-lookup"><span data-stu-id="dc213-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="dc213-110">[Visual Studio Code](https://code.visualstudio.com/) 是輕量型、開放原始碼、跨平台的程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="dc213-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="dc213-111">強烈建議使用 Visual Studio Code 來建立 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="dc213-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="dc213-112">本主題假設您使用 VS Code；不過，如果您有其他 JSON 編輯器 (如 Visual Studio)，您可以使用該編輯器。</span><span class="sxs-lookup"><span data-stu-id="dc213-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc213-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc213-113">Prerequisites</span></span>

* <span data-ttu-id="dc213-114">Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="dc213-114">Visual Studio Code.</span></span> <span data-ttu-id="dc213-115">如有需要，請從 [https://code.visualstudio.com/](https://code.visualstudio.com/) 進行安裝。</span><span class="sxs-lookup"><span data-stu-id="dc213-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="dc213-116">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc213-116">An Azure subscription.</span></span> <span data-ttu-id="dc213-117">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="dc213-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="dc213-118">建立範本</span><span class="sxs-lookup"><span data-stu-id="dc213-118">Create template</span></span>

<span data-ttu-id="dc213-119">讓我們開始與簡單的範本部署儲存體帳戶 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc213-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="dc213-120">選取 [檔案] > [新增檔案]。</span><span class="sxs-lookup"><span data-stu-id="dc213-120">Select **File** > **New File**.</span></span> 

   ![新增檔案](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="dc213-122">複製並貼到您的檔案使用下列 JSON 語法 hello:</span><span class="sxs-lookup"><span data-stu-id="dc213-122">Copy and paste hello following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="dc213-123">儲存體帳戶名稱中有許多限制，使其難以 tooset。</span><span class="sxs-lookup"><span data-stu-id="dc213-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="dc213-124">hello 名稱必須介於 3 到 24 個字元，長度、 使用數字和小寫字母，而且是唯一。</span><span class="sxs-lookup"><span data-stu-id="dc213-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="dc213-125">hello 上述範本使用 hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式 toogenerate 雜湊值。</span><span class="sxs-lookup"><span data-stu-id="dc213-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="dc213-126">此雜湊值表示多 toogive，便會新增 hello 前置詞*儲存體*。</span><span class="sxs-lookup"><span data-stu-id="dc213-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="dc213-127">將此檔案儲存為**azuredeploy.json** tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc213-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![儲存範本](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="dc213-129">部署範本</span><span class="sxs-lookup"><span data-stu-id="dc213-129">Deploy template</span></span>

<span data-ttu-id="dc213-130">您已準備好 toodeploy 此範本。</span><span class="sxs-lookup"><span data-stu-id="dc213-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="dc213-131">您使用 PowerShell 或 Azure CLI toocreate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="dc213-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="dc213-132">接著，您將部署的儲存體帳戶 toothat 資源群組。</span><span class="sxs-lookup"><span data-stu-id="dc213-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="dc213-133">如需 PowerShell，使用 hello hello 包含 hello 範本的資料夾中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="dc213-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="dc213-134">使用 Azure CLI 是本機安裝，hello hello 包含 hello 範本的資料夾中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="dc213-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="dc213-135">當部署完成時，則會在 hello 資源群組中有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc213-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="dc213-136">從 Cloud Shell 部署範本</span><span class="sxs-lookup"><span data-stu-id="dc213-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="dc213-137">您可以使用[雲端殼層](../cloud-shell/overview.md)toorun hello Azure CLI 命令來部署您的範本。</span><span class="sxs-lookup"><span data-stu-id="dc213-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="dc213-138">不過，您必須先載入您的範本 hello 檔案共用雲端 shell。</span><span class="sxs-lookup"><span data-stu-id="dc213-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="dc213-139">如果您尚未使用 Cloud Shell，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)以取得如何設定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="dc213-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="dc213-140">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="dc213-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="dc213-141">選取您的 Cloud Shell 資源群組。</span><span class="sxs-lookup"><span data-stu-id="dc213-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="dc213-142">hello 名稱模式`cloud-shell-storage-<region>`。</span><span class="sxs-lookup"><span data-stu-id="dc213-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![選取資源群組](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="dc213-144">選取您的雲端 Shell hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc213-144">Select hello storage account for your Cloud Shell.</span></span>

   ![選取儲存體帳戶](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="dc213-146">選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="dc213-146">Select **Files**.</span></span>

   ![選取檔案](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="dc213-148">選取雲端殼層 hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc213-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="dc213-149">hello 名稱模式`cs-<user>-<domain>-com-<uniqueGuid>`。</span><span class="sxs-lookup"><span data-stu-id="dc213-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![選取檔案共用](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="dc213-151">選取 [新增目錄]。</span><span class="sxs-lookup"><span data-stu-id="dc213-151">Select **Add directory**.</span></span>

   ![新增目錄](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="dc213-153">將它命名為 **templates**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="dc213-153">Name it **templates**, and select **Okay**.</span></span>

   ![命名目錄](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="dc213-155">選取您的新目錄。</span><span class="sxs-lookup"><span data-stu-id="dc213-155">Select your new directory.</span></span>

   ![選取目錄](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="dc213-157">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="dc213-157">Select **Upload**.</span></span>

   ![選取上傳](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="dc213-159">尋找並上傳您的範本。</span><span class="sxs-lookup"><span data-stu-id="dc213-159">Find and upload your template.</span></span>

   ![上傳檔案](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="dc213-161">開啟 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="dc213-161">Open hello prompt.</span></span>

   ![開啟 Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="dc213-163">輸入 hello 遵循 hello 雲端殼層中的命令：</span><span class="sxs-lookup"><span data-stu-id="dc213-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="dc213-164">當部署完成時，則會在 hello 資源群組中有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc213-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="dc213-165">自訂 hello 範本</span><span class="sxs-lookup"><span data-stu-id="dc213-165">Customize hello template</span></span>

<span data-ttu-id="dc213-166">hello 範本可正常運作，但不是有彈性。</span><span class="sxs-lookup"><span data-stu-id="dc213-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="dc213-167">一律將部署本機備援儲存體 tooSouth 美國中部。</span><span class="sxs-lookup"><span data-stu-id="dc213-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="dc213-168">hello 名稱永遠是*儲存體*後面雜湊值。</span><span class="sxs-lookup"><span data-stu-id="dc213-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="dc213-169">tooenable hello 範本使用不同的情況下，新增參數 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="dc213-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="dc213-170">hello 下列範例示範具有兩個參數的 hello 參數 > 一節。</span><span class="sxs-lookup"><span data-stu-id="dc213-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="dc213-171">hello 第一個參數`storageSKU`可讓您的備援 toospecify hello 型別。</span><span class="sxs-lookup"><span data-stu-id="dc213-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="dc213-172">它會限制您可以傳入有效的儲存體帳戶 toovalues hello 值。</span><span class="sxs-lookup"><span data-stu-id="dc213-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="dc213-173">它也會指定預設值。</span><span class="sxs-lookup"><span data-stu-id="dc213-173">It also specifies a default value.</span></span> <span data-ttu-id="dc213-174">hello 第二個參數`storageNamePrefix`是集 tooallow 11 個字元的最大值。</span><span class="sxs-lookup"><span data-stu-id="dc213-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="dc213-175">它會指定預設值。</span><span class="sxs-lookup"><span data-stu-id="dc213-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="dc213-176">在 hello 變數區段中，加入名為的變數`storageName`。</span><span class="sxs-lookup"><span data-stu-id="dc213-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="dc213-177">它會結合 hello hello 參數前置詞值和雜湊值從 hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式。</span><span class="sxs-lookup"><span data-stu-id="dc213-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="dc213-178">它會使用 hello [toLower](resource-group-template-functions-string.md#tolower)函式 tooconvert 所有字元 toolowercase。</span><span class="sxs-lookup"><span data-stu-id="dc213-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="dc213-179">toouse 儲存體帳戶，這些新值會變更 hello 資源定義：</span><span class="sxs-lookup"><span data-stu-id="dc213-179">toouse these new values for your storage account, change hello resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="dc213-180">請注意該 hello hello 儲存體帳戶名稱現在已設定您加入的 toohello 變數。</span><span class="sxs-lookup"><span data-stu-id="dc213-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="dc213-181">hello SKU 名稱設定 toohello hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="dc213-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="dc213-182">hello 位置會設定 hello 與 hello 資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="dc213-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="dc213-183">儲存您的檔案。</span><span class="sxs-lookup"><span data-stu-id="dc213-183">Save your file.</span></span> 

<span data-ttu-id="dc213-184">完成本文章中的 hello 步驟之後，您範本現在看起來像：</span><span class="sxs-lookup"><span data-stu-id="dc213-184">After completing hello steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="dc213-185">重新部署範本</span><span class="sxs-lookup"><span data-stu-id="dc213-185">Redeploy template</span></span>

<span data-ttu-id="dc213-186">重新部署 hello 範本有不同的值。</span><span class="sxs-lookup"><span data-stu-id="dc213-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="dc213-187">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="dc213-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="dc213-188">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="dc213-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="dc213-189">Hello 雲端殼層上, 傳您已變更的範本 toohello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="dc213-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="dc213-190">覆寫 hello 現有檔案。</span><span class="sxs-lookup"><span data-stu-id="dc213-190">Overwrite hello existing file.</span></span> <span data-ttu-id="dc213-191">然後，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc213-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="dc213-192">清除資源</span><span class="sxs-lookup"><span data-stu-id="dc213-192">Clean up resources</span></span>

<span data-ttu-id="dc213-193">當不再需要請清除您藉由刪除 hello 資源群組部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="dc213-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="dc213-194">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="dc213-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="dc213-195">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="dc213-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="dc213-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc213-196">Next steps</span></span>
* <span data-ttu-id="dc213-197">toolearn 進一步了解 hello 結構的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="dc213-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="dc213-198">toolearn 有關 hello 屬性儲存體帳戶，請參閱[儲存體帳戶的範本參考](/azure/templates/microsoft.storage/storageaccounts)。</span><span class="sxs-lookup"><span data-stu-id="dc213-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="dc213-199">tooview 完成範本的許多不同類型的方案，請參閱 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="dc213-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
