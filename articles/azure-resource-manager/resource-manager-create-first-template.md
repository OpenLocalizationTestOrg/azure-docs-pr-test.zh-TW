---
title: "建立第一個 Azure Resource Manager 範本 | Microsoft Docs"
description: "說明如何建立第一個 Azure Resource Manager 範本的逐步指南。 它說明如何使用儲存體帳戶的範本參考來建立範本。"
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
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="f444f-104">建立及部署第一個 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="f444f-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="f444f-105">本主題會逐步引導您完成建立第一個 Azure Resource Manager 範本的步驟。</span><span class="sxs-lookup"><span data-stu-id="f444f-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="f444f-106">Resource Manager 範本是 JSON 檔案，該檔案定義您需要為您的解決方案部署的資源。</span><span class="sxs-lookup"><span data-stu-id="f444f-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="f444f-107">若要了解部署和管理 Azure 解決方案的相關概念，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f444f-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="f444f-108">如果您有現成的資源且想要取得這些資源的範本，請參閱[從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="f444f-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="f444f-109">若要建立並修改範本，您需要 JSON 編輯器。</span><span class="sxs-lookup"><span data-stu-id="f444f-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="f444f-110">[Visual Studio Code](https://code.visualstudio.com/) 是輕量型、開放原始碼、跨平台的程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="f444f-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="f444f-111">強烈建議使用 Visual Studio Code 來建立 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="f444f-112">本主題假設您使用 VS Code；不過，如果您有其他 JSON 編輯器 (如 Visual Studio)，您可以使用該編輯器。</span><span class="sxs-lookup"><span data-stu-id="f444f-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f444f-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f444f-113">Prerequisites</span></span>

* <span data-ttu-id="f444f-114">Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="f444f-114">Visual Studio Code.</span></span> <span data-ttu-id="f444f-115">如有需要，請從 [https://code.visualstudio.com/](https://code.visualstudio.com/) 進行安裝。</span><span class="sxs-lookup"><span data-stu-id="f444f-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="f444f-116">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f444f-116">An Azure subscription.</span></span> <span data-ttu-id="f444f-117">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="f444f-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="f444f-118">建立範本</span><span class="sxs-lookup"><span data-stu-id="f444f-118">Create template</span></span>

<span data-ttu-id="f444f-119">讓我們從將儲存體帳戶部署到訂用帳戶的簡單範本著手。</span><span class="sxs-lookup"><span data-stu-id="f444f-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="f444f-120">選取 [檔案] > [新增檔案]。</span><span class="sxs-lookup"><span data-stu-id="f444f-120">Select **File** > **New File**.</span></span> 

   ![新增檔案](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="f444f-122">複製以下 JSON 語法並貼到您的檔案中：</span><span class="sxs-lookup"><span data-stu-id="f444f-122">Copy and paste the following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="f444f-123">儲存體帳戶名稱有幾項限制，以致它們難以設定。</span><span class="sxs-lookup"><span data-stu-id="f444f-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="f444f-124">名稱的長度必須介於 3 到 24 個字元，只能使用數字和小寫字母，而且必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f444f-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="f444f-125">前述版本會使用 [uniqueString](resource-group-template-functions-string.md#uniquestring) 函式來產生雜湊值。</span><span class="sxs-lookup"><span data-stu-id="f444f-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="f444f-126">為了要讓此雜湊值更有意義，它會新增前置詞*storage*。</span><span class="sxs-lookup"><span data-stu-id="f444f-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="f444f-127">將此檔案儲存為本機資料夾的 azuredeploy.json。</span><span class="sxs-lookup"><span data-stu-id="f444f-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![儲存範本](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="f444f-129">部署範本</span><span class="sxs-lookup"><span data-stu-id="f444f-129">Deploy template</span></span>

<span data-ttu-id="f444f-130">您已準備好部署此範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-130">You are ready to deploy this template.</span></span> <span data-ttu-id="f444f-131">您可以使用 PowerShell 或 Azure CLI 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f444f-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="f444f-132">然後，將儲存體帳戶部署到該資源群組。</span><span class="sxs-lookup"><span data-stu-id="f444f-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="f444f-133">對於 PowerShell，從包含範本的資料夾使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="f444f-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="f444f-134">對於 Azure CLI 的本機安裝，從包含範本的資料夾使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="f444f-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="f444f-135">部署完成時，您的儲存體帳戶會儲存在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="f444f-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="f444f-136">從 Cloud Shell 部署範本</span><span class="sxs-lookup"><span data-stu-id="f444f-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="f444f-137">您可以使用 [Cloud Shell](../cloud-shell/overview.md) 執行 Azure CLI 命令，以便部署範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="f444f-138">不過，您必須先將範本載入 Cloud Shell 的檔案共用中。</span><span class="sxs-lookup"><span data-stu-id="f444f-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="f444f-139">如果您尚未使用 Cloud Shell，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)以取得如何設定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f444f-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="f444f-140">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f444f-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="f444f-141">選取您的 Cloud Shell 資源群組。</span><span class="sxs-lookup"><span data-stu-id="f444f-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="f444f-142">名稱模式為 `cloud-shell-storage-<region>`。</span><span class="sxs-lookup"><span data-stu-id="f444f-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![選取資源群組](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="f444f-144">選取 Cloud Shell 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f444f-144">Select the storage account for your Cloud Shell.</span></span>

   ![選取儲存體帳戶](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="f444f-146">選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="f444f-146">Select **Files**.</span></span>

   ![選取檔案](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="f444f-148">選取 Cloud Shell 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f444f-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="f444f-149">名稱模式為 `cs-<user>-<domain>-com-<uniqueGuid>`。</span><span class="sxs-lookup"><span data-stu-id="f444f-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![選取檔案共用](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="f444f-151">選取 [新增目錄]。</span><span class="sxs-lookup"><span data-stu-id="f444f-151">Select **Add directory**.</span></span>

   ![新增目錄](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="f444f-153">將它命名為 **templates**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f444f-153">Name it **templates**, and select **Okay**.</span></span>

   ![命名目錄](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="f444f-155">選取您的新目錄。</span><span class="sxs-lookup"><span data-stu-id="f444f-155">Select your new directory.</span></span>

   ![選取目錄](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="f444f-157">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="f444f-157">Select **Upload**.</span></span>

   ![選取上傳](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="f444f-159">尋找並上傳您的範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-159">Find and upload your template.</span></span>

   ![上傳檔案](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="f444f-161">開啟提示字元。</span><span class="sxs-lookup"><span data-stu-id="f444f-161">Open the prompt.</span></span>

   ![開啟 Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="f444f-163">在 Cloud Shell 中輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f444f-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="f444f-164">部署完成時，您的儲存體帳戶會儲存在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="f444f-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="f444f-165">自訂範本</span><span class="sxs-lookup"><span data-stu-id="f444f-165">Customize the template</span></span>

<span data-ttu-id="f444f-166">範本正常運作，但不具彈性。</span><span class="sxs-lookup"><span data-stu-id="f444f-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="f444f-167">它一律會將本機備援儲存體部署至美國中南部。</span><span class="sxs-lookup"><span data-stu-id="f444f-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="f444f-168">名稱一律為 *storage* 後面接著雜湊值。</span><span class="sxs-lookup"><span data-stu-id="f444f-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="f444f-169">若要讓範本能使用於不同的案例，請將參數新增至範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="f444f-170">以下範例顯示包含兩個參數的 parameters 區段。</span><span class="sxs-lookup"><span data-stu-id="f444f-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="f444f-171">第一個參數 `storageSKU` 可讓您指定備援類型。</span><span class="sxs-lookup"><span data-stu-id="f444f-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="f444f-172">它會將您可傳入的值限制為對儲存體帳戶有效的值。</span><span class="sxs-lookup"><span data-stu-id="f444f-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="f444f-173">它也會指定預設值。</span><span class="sxs-lookup"><span data-stu-id="f444f-173">It also specifies a default value.</span></span> <span data-ttu-id="f444f-174">第二個參數 `storageNamePrefix` 會設定為最多允許 11 個字元。</span><span class="sxs-lookup"><span data-stu-id="f444f-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="f444f-175">它會指定預設值。</span><span class="sxs-lookup"><span data-stu-id="f444f-175">It specifies a default value.</span></span>

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
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="f444f-176">在 variables 區段中，新增名為 `storageName` 的變數。</span><span class="sxs-lookup"><span data-stu-id="f444f-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="f444f-177">它結合了來自 parameters 的前置詞值與來自 [uniqueString](resource-group-template-functions-string.md#uniquestring) 函式的雜湊值。</span><span class="sxs-lookup"><span data-stu-id="f444f-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="f444f-178">它會使用 [toLower](resource-group-template-functions-string.md#tolower) 函式，將所有字元轉換成小寫。</span><span class="sxs-lookup"><span data-stu-id="f444f-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="f444f-179">若要對您的儲存體帳戶使用這些新值，請變更資源定義：</span><span class="sxs-lookup"><span data-stu-id="f444f-179">To use these new values for your storage account, change the resource definition:</span></span>

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

<span data-ttu-id="f444f-180">請注意，儲存體帳戶的名稱現在會設定為您新增的變數。</span><span class="sxs-lookup"><span data-stu-id="f444f-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="f444f-181">SKU 名稱會設定為參數的值。</span><span class="sxs-lookup"><span data-stu-id="f444f-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="f444f-182">位置會設定為與資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="f444f-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="f444f-183">儲存您的檔案。</span><span class="sxs-lookup"><span data-stu-id="f444f-183">Save your file.</span></span> 

<span data-ttu-id="f444f-184">完成本文中的步驟之後，您的範本現在如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f444f-184">After completing the steps in this article, your template now looks like:</span></span>

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
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="f444f-185">重新部署範本</span><span class="sxs-lookup"><span data-stu-id="f444f-185">Redeploy template</span></span>

<span data-ttu-id="f444f-186">使用不同的值重新部署範本。</span><span class="sxs-lookup"><span data-stu-id="f444f-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="f444f-187">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="f444f-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="f444f-188">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="f444f-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="f444f-189">對於 Cloud Shell，將已變更的範本上傳到檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f444f-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="f444f-190">覆寫現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="f444f-190">Overwrite the existing file.</span></span> <span data-ttu-id="f444f-191">然後，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="f444f-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="f444f-192">清除資源</span><span class="sxs-lookup"><span data-stu-id="f444f-192">Clean up resources</span></span>

<span data-ttu-id="f444f-193">不再需要資源時，可藉由刪除資源群組來清除您所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="f444f-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="f444f-194">對於 PowerShell，請使用：</span><span class="sxs-lookup"><span data-stu-id="f444f-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="f444f-195">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="f444f-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="f444f-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f444f-196">Next steps</span></span>
* <span data-ttu-id="f444f-197">若要深入了解範本的結構，請參閱 [編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f444f-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f444f-198">若要了解儲存體帳戶的屬性，請參閱[儲存體帳戶範本參考](/azure/templates/microsoft.storage/storageaccounts)。</span><span class="sxs-lookup"><span data-stu-id="f444f-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="f444f-199">若要檢視許多不同類型解決方案的完整範本，請參閱 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="f444f-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
