---
title: "使用 PowerShell 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和 Azure PowerShell toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="d7047-104">使用 Resource Manager 範本與 Azure PowerShell 來部署資源</span><span class="sxs-lookup"><span data-stu-id="d7047-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="d7047-105">本主題說明如何使用資源管理員範本 toodeploy toouse Azure PowerShell 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d7047-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="d7047-106">如果您不熟悉以部署的 hello 概念，並管理您的 Azure 解決方案，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="d7047-107">您所部署的 hello Resource Manager 範本可為您的電腦上的本機檔案或位於等 GitHub 儲存機制中的外部檔案。</span><span class="sxs-lookup"><span data-stu-id="d7047-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="d7047-108">您在本文中部署的 hello 範本位於 hello[範例範本](#sample-template) 區段中，或為[GitHub 中的儲存體帳戶範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="d7047-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="d7047-109">從本機電腦部署範本</span><span class="sxs-lookup"><span data-stu-id="d7047-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="d7047-110">部署資源 tooAzure 時您：</span><span class="sxs-lookup"><span data-stu-id="d7047-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="d7047-111">登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="d7047-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="d7047-112">建立可做為部署的 hello 資源的 hello 容器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d7047-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="d7047-113">hello hello 資源群組名稱只可包含英數字元、 句號、 底線、 連字號及括號。</span><span class="sxs-lookup"><span data-stu-id="d7047-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="d7047-114">它可以是 too90 字元組成。</span><span class="sxs-lookup"><span data-stu-id="d7047-114">It can be up too90 characters.</span></span> <span data-ttu-id="d7047-115">不能以句點結束。</span><span class="sxs-lookup"><span data-stu-id="d7047-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="d7047-116">部署 toohello 資源群組 hello 範本定義 hello 資源 toocreate</span><span class="sxs-lookup"><span data-stu-id="d7047-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="d7047-117">範本可以包含 toocustomize hello 部署可讓您的參數。</span><span class="sxs-lookup"><span data-stu-id="d7047-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="d7047-118">例如，您可以提供針對特定環境 (例如開發、測試和生產) 量身訂做的值。</span><span class="sxs-lookup"><span data-stu-id="d7047-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="d7047-119">hello 範例範本定義 hello 儲存體帳戶 SKU 的參數。</span><span class="sxs-lookup"><span data-stu-id="d7047-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="d7047-120">hello 下列範例會建立資源群組，並部署範本從本機電腦：</span><span class="sxs-lookup"><span data-stu-id="d7047-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="d7047-121">hello 部署可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="d7047-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="d7047-122">完成時，您會看到訊息，其中包含 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="d7047-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="d7047-123">從外部來源部署範本</span><span class="sxs-lookup"><span data-stu-id="d7047-123">Deploy a template from an external source</span></span>

<span data-ttu-id="d7047-124">而不是儲存在本機電腦上的資源管理員範本，您可能會想 toostore 外部位置中。</span><span class="sxs-lookup"><span data-stu-id="d7047-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="d7047-125">您可以將範本儲存在原始檔控制存放庫 (例如 GitHub) 中。</span><span class="sxs-lookup"><span data-stu-id="d7047-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="d7047-126">或者，您可以將它們儲存在 Azure 儲存體帳戶中，以在組織內共用存取。</span><span class="sxs-lookup"><span data-stu-id="d7047-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="d7047-127">toodeploy 的外部的範本，請使用 hello **TemplateUri**參數。</span><span class="sxs-lookup"><span data-stu-id="d7047-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="d7047-128">使用 hello 範例 toodeploy hello 範例範本從 GitHub 中的 hello URI。</span><span class="sxs-lookup"><span data-stu-id="d7047-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="d7047-129">hello 上述範例要求可公開存取 URI hello 範本，適用於大部分的情況下，因為您的範本不應該包含機密資料。</span><span class="sxs-lookup"><span data-stu-id="d7047-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="d7047-130">如果您需要 toospecify 敏感性資料 （例如系統管理員密碼），將值傳遞做為安全的參數。</span><span class="sxs-lookup"><span data-stu-id="d7047-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="d7047-131">不過，如果您不想範本 toobe 可公開存取，您可以保護它儲存在私人儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="d7047-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="d7047-132">如需部署需要共用存取簽章 (SAS) 權杖之範本的相關資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="d7047-133">參數檔案</span><span class="sxs-lookup"><span data-stu-id="d7047-133">Parameter files</span></span>

<span data-ttu-id="d7047-134">而不是傳遞參數做為內嵌指令碼中的值，您可能會發現它更容易 toouse 包含 hello 參數值的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="d7047-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="d7047-135">hello 參數檔案必須是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d7047-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="d7047-136">請注意 hello 參數 > 一節包含符合您的範本 (storageAccountType) 中定義的 hello 參數的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="d7047-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="d7047-137">hello 參數檔案包含 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="d7047-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="d7047-138">這個值會自動在部署期間傳遞 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="d7047-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="d7047-139">您可以建立不同部署案例中，多個參數檔案，並接著傳入 hello 適當的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="d7047-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="d7047-140">複製 hello 前面範例中，然後將它儲存為檔案命名為`storage.parameters.json`。</span><span class="sxs-lookup"><span data-stu-id="d7047-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="d7047-141">toopass 本機參數檔案中，使用 hello **TemplateParameterFile**參數：</span><span class="sxs-lookup"><span data-stu-id="d7047-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="d7047-142">toopass 的外部參數檔案，使用 hello **TemplateParameterUri**參數：</span><span class="sxs-lookup"><span data-stu-id="d7047-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="d7047-143">您可以使用內嵌參數與本機參數檔案中 hello 相同部署作業。</span><span class="sxs-lookup"><span data-stu-id="d7047-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="d7047-144">比方說，您可以在 hello 本機參數檔案中指定某些值，並新增其他值內嵌在部署期間。</span><span class="sxs-lookup"><span data-stu-id="d7047-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="d7047-145">如果您提供參數的值在 hello 本機參數檔案和內嵌，hello 內嵌值的優先順序較高。</span><span class="sxs-lookup"><span data-stu-id="d7047-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="d7047-146">不過，當使用外部參數檔案時，您無法傳遞內嵌或本機檔案的其他值。</span><span class="sxs-lookup"><span data-stu-id="d7047-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="d7047-147">當您指定的參數檔案中 hello **TemplateParameterUri**參數，所有內嵌參數被忽略。</span><span class="sxs-lookup"><span data-stu-id="d7047-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="d7047-148">提供 hello 外部檔案中的所有參數值。</span><span class="sxs-lookup"><span data-stu-id="d7047-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="d7047-149">如果您的範本包含機密值，您不能包含 hello 參數檔案中，新增該值 tooa 金鑰保存庫，或是以動態方式提供所有參數值內嵌。</span><span class="sxs-lookup"><span data-stu-id="d7047-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="d7047-150">如果您的範本包含具有相同的名稱，做為其中一個 hello PowerShell 命令中的 hello 參數 hello 的參數，PowerShell 會顯示 hello 參數，從您的範本與 hello 後置**FromTemplate**。</span><span class="sxs-lookup"><span data-stu-id="d7047-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="d7047-151">例如，名為的參數**ResourceGroupName**在您範本與 hello 衝突**ResourceGroupName**中 hello 參數[新增 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d7047-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="d7047-152">值是提示的 tooprovide **ResourceGroupNameFromTemplate**。</span><span class="sxs-lookup"><span data-stu-id="d7047-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="d7047-153">一般情況下，您應該避免混淆，未指名參數，以做為部署作業所使用的參數名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d7047-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="d7047-154">測試範本部署</span><span class="sxs-lookup"><span data-stu-id="d7047-154">Test a template deployment</span></span>

<span data-ttu-id="d7047-155">您的範本和參數值，而不實際部署任何資源，使用 tootest[測試 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment)。</span><span class="sxs-lookup"><span data-stu-id="d7047-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="d7047-156">如果偵測不到任何錯誤，hello 命令執行完成，無回應。</span><span class="sxs-lookup"><span data-stu-id="d7047-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="d7047-157">如果偵測到錯誤時，hello 命令會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d7047-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="d7047-158">例如，嘗試 toopass hello 儲存體帳戶 SKU 不正確的值會傳回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="d7047-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="d7047-159">如果您的範本有語法錯誤，hello 命令會傳回錯誤，指出無法剖析 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="d7047-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="d7047-160">hello 訊息表示 hello 行號和 hello 剖析錯誤的位置。</span><span class="sxs-lookup"><span data-stu-id="d7047-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="d7047-161">toouse 完成模式中，使用 hello`Mode`參數：</span><span class="sxs-lookup"><span data-stu-id="d7047-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="d7047-162">範例範本</span><span class="sxs-lookup"><span data-stu-id="d7047-162">Sample template</span></span>

<span data-ttu-id="d7047-163">hello 下列範本會用於本主題中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d7047-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="d7047-164">請複製它並另存為名叫 storage.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="d7047-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="d7047-165">toounderstand 如何 toocreate 此範本，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="d7047-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7047-166">Next steps</span></span>
* <span data-ttu-id="d7047-167">本文中的 hello 範例部署中預設訂用帳戶資源 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d7047-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="d7047-168">toouse 不同的訂用帳戶，請參閱[管理多個 Azure 訂用帳戶](/powershell/azure/manage-subscriptions-azureps)。</span><span class="sxs-lookup"><span data-stu-id="d7047-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="d7047-169">如需部署範本的完整範例指令碼，請參閱 [Resource Manager 範本部署指令碼](resource-manager-samples-powershell-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="d7047-170">如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d7047-171">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="d7047-172">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="d7047-173">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="d7047-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

