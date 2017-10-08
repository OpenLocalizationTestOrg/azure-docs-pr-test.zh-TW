---
title: "使用 Azure CLI 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和 Azure CLI toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="2d76d-104">使用 Resource Manager 範本與 Azure CLI 部署資源</span><span class="sxs-lookup"><span data-stu-id="2d76d-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="2d76d-105">本主題說明如何使用資源管理員範本 toodeploy toouse Azure CLI 2.0 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2d76d-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="2d76d-106">如果您不熟悉以部署的 hello 概念，並管理您的 Azure 解決方案，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="2d76d-107">您所部署的 hello Resource Manager 範本可為您的電腦上的本機檔案或位於等 GitHub 儲存機制中的外部檔案。</span><span class="sxs-lookup"><span data-stu-id="2d76d-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="2d76d-108">您在本文中部署的 hello 範本位於 hello[範例範本](#sample-template) 區段中，或為[GitHub 中的儲存體帳戶範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="2d76d-109">如果您沒有 Azure CLI 安裝，您可以使用 hello[雲端殼層](#deploy-template-from-cloud-shell)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="2d76d-110">部署本機範本</span><span class="sxs-lookup"><span data-stu-id="2d76d-110">Deploy local template</span></span>

<span data-ttu-id="2d76d-111">部署資源 tooAzure 時您：</span><span class="sxs-lookup"><span data-stu-id="2d76d-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="2d76d-112">登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="2d76d-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="2d76d-113">建立可做為部署的 hello 資源的 hello 容器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2d76d-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="2d76d-114">hello hello 資源群組名稱只可包含英數字元、 句號、 底線、 連字號及括號。</span><span class="sxs-lookup"><span data-stu-id="2d76d-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="2d76d-115">它可以是 too90 字元組成。</span><span class="sxs-lookup"><span data-stu-id="2d76d-115">It can be up too90 characters.</span></span> <span data-ttu-id="2d76d-116">不能以句點結束。</span><span class="sxs-lookup"><span data-stu-id="2d76d-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="2d76d-117">部署 toohello 資源群組 hello 範本定義 hello 資源 toocreate</span><span class="sxs-lookup"><span data-stu-id="2d76d-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="2d76d-118">範本可以包含 toocustomize hello 部署可讓您的參數。</span><span class="sxs-lookup"><span data-stu-id="2d76d-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="2d76d-119">例如，您可以提供針對特定環境 (例如開發、測試和生產) 量身訂做的值。</span><span class="sxs-lookup"><span data-stu-id="2d76d-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="2d76d-120">hello 範例範本定義 hello 儲存體帳戶 SKU 的參數。</span><span class="sxs-lookup"><span data-stu-id="2d76d-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="2d76d-121">hello 下列範例會建立資源群組，並部署範本從本機電腦：</span><span class="sxs-lookup"><span data-stu-id="2d76d-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="2d76d-122">hello 部署可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2d76d-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="2d76d-123">完成時，您會看到訊息，其中包含 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="2d76d-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="2d76d-124">部署外部範本</span><span class="sxs-lookup"><span data-stu-id="2d76d-124">Deploy external template</span></span>

<span data-ttu-id="2d76d-125">而不是儲存在本機電腦上的資源管理員範本，您可能會想 toostore 外部位置中。</span><span class="sxs-lookup"><span data-stu-id="2d76d-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="2d76d-126">您可以將範本儲存在原始檔控制存放庫 (例如 GitHub) 中。</span><span class="sxs-lookup"><span data-stu-id="2d76d-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="2d76d-127">或者，您可以將它們儲存在 Azure 儲存體帳戶中，以在組織內共用存取。</span><span class="sxs-lookup"><span data-stu-id="2d76d-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="2d76d-128">toodeploy 的外部的範本，請使用 hello**範本 uri**參數。</span><span class="sxs-lookup"><span data-stu-id="2d76d-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="2d76d-129">使用 hello 範例 toodeploy hello 範例範本從 GitHub 中的 hello URI。</span><span class="sxs-lookup"><span data-stu-id="2d76d-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="2d76d-130">hello 上述範例要求可公開存取 URI hello 範本，適用於大部分的情況下，因為您的範本不應該包含機密資料。</span><span class="sxs-lookup"><span data-stu-id="2d76d-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="2d76d-131">如果您需要 toospecify 敏感性資料 （例如系統管理員密碼），將值傳遞做為安全的參數。</span><span class="sxs-lookup"><span data-stu-id="2d76d-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="2d76d-132">不過，如果您不想範本 toobe 可公開存取，您可以保護它儲存在私人儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="2d76d-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="2d76d-133">如需部署需要共用存取簽章 (SAS) 權杖之範本的相關資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="2d76d-134">從 Cloud Shell 部署範本</span><span class="sxs-lookup"><span data-stu-id="2d76d-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="2d76d-135">您可以使用[雲端殼層](../cloud-shell/overview.md)toorun hello Azure CLI 命令來部署您的範本。</span><span class="sxs-lookup"><span data-stu-id="2d76d-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="2d76d-136">不過，您必須先載入您的範本 hello 檔案共用雲端 shell。</span><span class="sxs-lookup"><span data-stu-id="2d76d-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="2d76d-137">如果您尚未使用 Cloud Shell，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)以取得如何設定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2d76d-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="2d76d-138">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="2d76d-139">選取您的 Cloud Shell 資源群組。</span><span class="sxs-lookup"><span data-stu-id="2d76d-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="2d76d-140">hello 名稱模式`cloud-shell-storage-<region>`。</span><span class="sxs-lookup"><span data-stu-id="2d76d-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![選取資源群組](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="2d76d-142">選取您的雲端 Shell hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d76d-142">Select hello storage account for your Cloud Shell.</span></span>

   ![選取儲存體帳戶](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="2d76d-144">選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="2d76d-144">Select **Files**.</span></span>

   ![選取檔案](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="2d76d-146">選取雲端殼層 hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="2d76d-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="2d76d-147">hello 名稱模式`cs-<user>-<domain>-com-<uniqueGuid>`。</span><span class="sxs-lookup"><span data-stu-id="2d76d-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![選取檔案共用](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="2d76d-149">選取 [新增目錄]。</span><span class="sxs-lookup"><span data-stu-id="2d76d-149">Select **Add directory**.</span></span>

   ![新增目錄](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="2d76d-151">將它命名為 **templates**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d76d-151">Name it **templates**, and select **Okay**.</span></span>

   ![命名目錄](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="2d76d-153">選取您的新目錄。</span><span class="sxs-lookup"><span data-stu-id="2d76d-153">Select your new directory.</span></span>

   ![選取目錄](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="2d76d-155">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="2d76d-155">Select **Upload**.</span></span>

   ![選取上傳](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="2d76d-157">尋找並上傳您的範本。</span><span class="sxs-lookup"><span data-stu-id="2d76d-157">Find and upload your template.</span></span>

   ![上傳檔案](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="2d76d-159">開啟 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="2d76d-159">Open hello prompt.</span></span>

   ![開啟 Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="2d76d-161">輸入 hello 遵循 hello 雲端殼層中的命令：</span><span class="sxs-lookup"><span data-stu-id="2d76d-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="2d76d-162">參數檔案</span><span class="sxs-lookup"><span data-stu-id="2d76d-162">Parameter files</span></span>

<span data-ttu-id="2d76d-163">而不是傳遞參數做為內嵌指令碼中的值，您可能會發現它更容易 toouse 包含 hello 參數值的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2d76d-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="2d76d-164">hello 參數檔案必須是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="2d76d-164">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="2d76d-165">請注意 hello 參數 > 一節包含符合您的範本 (storageAccountType) 中定義的 hello 參數的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2d76d-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="2d76d-166">hello 參數檔案包含 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2d76d-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="2d76d-167">這個值會自動在部署期間傳遞 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="2d76d-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="2d76d-168">您可以建立不同部署案例中，多個參數檔案，並接著傳入 hello 適當的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="2d76d-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="2d76d-169">複製 hello 前面範例中，然後將它儲存為檔案命名為`storage.parameters.json`。</span><span class="sxs-lookup"><span data-stu-id="2d76d-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="2d76d-170">toopass 本機參數檔案中，使用`@`toospecify 名為 storage.parameters.json 的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="2d76d-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="2d76d-171">測試範本部署</span><span class="sxs-lookup"><span data-stu-id="2d76d-171">Test a template deployment</span></span>

<span data-ttu-id="2d76d-172">您的範本和參數值，而不實際部署任何資源，使用 tootest [az 群組部署驗證](/cli/azure/group/deployment#validate)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="2d76d-173">如果偵測不到任何錯誤，hello 命令會傳回 hello 測試部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2d76d-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="2d76d-174">特別是，請注意該 hello**錯誤**值為 null。</span><span class="sxs-lookup"><span data-stu-id="2d76d-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="2d76d-175">如果偵測到錯誤時，hello 命令會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2d76d-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="2d76d-176">例如，嘗試 toopass hello 儲存體帳戶 SKU 不正確的值會傳回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="2d76d-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="2d76d-177">如果您的範本有語法錯誤，hello 命令會傳回錯誤，指出無法剖析 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="2d76d-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="2d76d-178">hello 訊息表示 hello 行號和 hello 剖析錯誤的位置。</span><span class="sxs-lookup"><span data-stu-id="2d76d-178">hello message indicates hello line number and position of hello parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="2d76d-179">toouse 完成模式中，使用 hello`mode`參數：</span><span class="sxs-lookup"><span data-stu-id="2d76d-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="2d76d-180">範例範本</span><span class="sxs-lookup"><span data-stu-id="2d76d-180">Sample template</span></span>

<span data-ttu-id="2d76d-181">hello 下列範本會用於本主題中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="2d76d-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="2d76d-182">請複製它並另存為名叫 storage.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="2d76d-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="2d76d-183">toounderstand 如何 toocreate 此範本，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2d76d-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d76d-184">Next steps</span></span>
* <span data-ttu-id="2d76d-185">本文中的 hello 範例部署中預設訂用帳戶資源 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="2d76d-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="2d76d-186">toouse 不同的訂用帳戶，請參閱[管理多個 Azure 訂用帳戶](/cli/azure/manage-azure-subscriptions-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="2d76d-187">如需部署範本的完整範例指令碼，請參閱 [Resource Manager 範本部署指令碼](resource-manager-samples-cli-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="2d76d-188">如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2d76d-189">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2d76d-190">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="2d76d-191">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="2d76d-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
