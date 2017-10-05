---
title: "使用 PowerShell 與範本部署資源 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Azure PowerShell，將資源部署至 Azure。 資源會定義在 Resource Manager 範本中。"
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
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="04711-104">使用 Resource Manager 範本與 Azure PowerShell 來部署資源</span><span class="sxs-lookup"><span data-stu-id="04711-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="04711-105">本主題說明如何使用 Azure PowerShell 與 Resource Manager 範本，將您的資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="04711-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="04711-106">如果您不熟悉部署和管理 Azure 解決方案的相關概念，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="04711-107">您所部署的 Resource Manager 範本可以是電腦上的本機檔案，或是位於存放庫 (例如 GitHub) 的外部檔案。</span><span class="sxs-lookup"><span data-stu-id="04711-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="04711-108">在本文的[範例範本](#sample-template)區段中會提供您要部署的範本，也可使用 [GitHub 中的儲存體帳戶範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="04711-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="04711-109">從本機電腦部署範本</span><span class="sxs-lookup"><span data-stu-id="04711-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="04711-110">將資源部署至 Azure 時，您應該：</span><span class="sxs-lookup"><span data-stu-id="04711-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="04711-111">登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="04711-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="04711-112">建立資源群組，作為已部署資源的容器。</span><span class="sxs-lookup"><span data-stu-id="04711-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="04711-113">資源群組的名稱只能包含英數字元、句點 (.)、底線、連字號及括弧。</span><span class="sxs-lookup"><span data-stu-id="04711-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="04711-114">最多可有 90 個字元。</span><span class="sxs-lookup"><span data-stu-id="04711-114">It can be up to 90 characters.</span></span> <span data-ttu-id="04711-115">不能以句點結束。</span><span class="sxs-lookup"><span data-stu-id="04711-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="04711-116">將範本部署至資源群組，範本中定義要建立的資源</span><span class="sxs-lookup"><span data-stu-id="04711-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="04711-117">範本可以包含讓您自訂部署的參數。</span><span class="sxs-lookup"><span data-stu-id="04711-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="04711-118">例如，您可以提供針對特定環境 (例如開發、測試和生產) 量身訂做的值。</span><span class="sxs-lookup"><span data-stu-id="04711-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="04711-119">範例範本會定義儲存體帳戶 SKU 的參數。</span><span class="sxs-lookup"><span data-stu-id="04711-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="04711-120">下列範例會建立資源群組，並從您的本機電腦部署範本：</span><span class="sxs-lookup"><span data-stu-id="04711-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="04711-121">部署需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="04711-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="04711-122">完成後，您會看到包含結果的訊息：</span><span class="sxs-lookup"><span data-stu-id="04711-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="04711-123">從外部來源部署範本</span><span class="sxs-lookup"><span data-stu-id="04711-123">Deploy a template from an external source</span></span>

<span data-ttu-id="04711-124">您可能希望將 Resource Manager 範本儲存在外部位置，而不是儲存在您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="04711-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="04711-125">您可以將範本儲存在原始檔控制存放庫 (例如 GitHub) 中。</span><span class="sxs-lookup"><span data-stu-id="04711-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="04711-126">或者，您可以將它們儲存在 Azure 儲存體帳戶中，讓組織共用存取。</span><span class="sxs-lookup"><span data-stu-id="04711-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="04711-127">若要部署外部範本，請使用 **TemplateUri** 參數。</span><span class="sxs-lookup"><span data-stu-id="04711-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="04711-128">使用範本中的 URI 部署 GitHub 上的範例範本。</span><span class="sxs-lookup"><span data-stu-id="04711-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="04711-129">上述範例針對範本需要可公開存取 URI，這適用於大部分的案例，因為您的範本不應該包含機密資料。</span><span class="sxs-lookup"><span data-stu-id="04711-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="04711-130">如果您需要指定機密資料 (例如系統管理員密碼)，請將該值以安全參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="04711-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="04711-131">不過，如果不希望將範本公開存取，您可以將它儲存在私人儲存體容器中加以保護。</span><span class="sxs-lookup"><span data-stu-id="04711-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="04711-132">如需部署需要共用存取簽章 (SAS) 權杖之範本的相關資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="04711-133">參數檔案</span><span class="sxs-lookup"><span data-stu-id="04711-133">Parameter files</span></span>

<span data-ttu-id="04711-134">相對於在您的指令碼中將參數做為內嵌值傳遞，使用包含該參數值的 JSON 檔案可能較為容易。</span><span class="sxs-lookup"><span data-stu-id="04711-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="04711-135">參數檔必須是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="04711-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="04711-136">請注意，參數區段包含符合於範本中所定義之參數 (storageAccountType) 的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="04711-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="04711-137">參數檔案包含參數的值。</span><span class="sxs-lookup"><span data-stu-id="04711-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="04711-138">這個值會在部署期間自動傳遞至範本。</span><span class="sxs-lookup"><span data-stu-id="04711-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="04711-139">您可以針對不同的部署案例建立多個參數檔案，然後傳遞適當的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="04711-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="04711-140">複製上述的範例，然後另存檔案，名稱為 `storage.parameters.json`。</span><span class="sxs-lookup"><span data-stu-id="04711-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="04711-141">若要傳遞本機參數檔案，請使用 **TemplateParameterFile** 參數︰</span><span class="sxs-lookup"><span data-stu-id="04711-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="04711-142">若要傳遞外部參數檔案，請使用 **TemplateParameterUri** 參數︰</span><span class="sxs-lookup"><span data-stu-id="04711-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="04711-143">您可以在相同的部署作業中使用內嵌參數和本機參數檔案。</span><span class="sxs-lookup"><span data-stu-id="04711-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="04711-144">例如，您可以在部署期間指定本機參數檔案中的某些值，並新增其他內嵌值。</span><span class="sxs-lookup"><span data-stu-id="04711-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="04711-145">如果您同時為本機檔案中和內嵌的參數提供值，內嵌值的優先順序較高。</span><span class="sxs-lookup"><span data-stu-id="04711-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="04711-146">不過，當使用外部參數檔案時，您無法傳遞內嵌或本機檔案的其他值。</span><span class="sxs-lookup"><span data-stu-id="04711-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="04711-147">當您指定 **TemplateParameterUri** 參數中的參數檔案時，所有內嵌參數都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="04711-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="04711-148">請提供外部檔案中的所有參數值。</span><span class="sxs-lookup"><span data-stu-id="04711-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="04711-149">如果您的範本包含不能包含在參數檔案中的機密值，請將該值新增至金鑰保存庫，或以動態方式提供所有內嵌參數值。</span><span class="sxs-lookup"><span data-stu-id="04711-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="04711-150">如果您範本所含的參數名稱與 PowerShell 命令中的其中一個參數一樣，PowerShell 會以加上後置 **FromTemplate** 的方式呈現您範本中的參數。</span><span class="sxs-lookup"><span data-stu-id="04711-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="04711-151">例如，範本中名為 **ResourceGroupName** 的參數會與 [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) Cmdlet 中的 **ResourceGroupName** 參數發生衝突。</span><span class="sxs-lookup"><span data-stu-id="04711-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="04711-152">系統會提示您為 **ResourceGroupNameFromTemplate** 提供值。</span><span class="sxs-lookup"><span data-stu-id="04711-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="04711-153">一般而言，在為參數命名時，請勿使用與部署作業所用參數相同的名稱，以避免發生這種混淆的情形。</span><span class="sxs-lookup"><span data-stu-id="04711-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="04711-154">測試範本部署</span><span class="sxs-lookup"><span data-stu-id="04711-154">Test a template deployment</span></span>

<span data-ttu-id="04711-155">若要測試您的範本和參數值而不實際部署任何資源，請使用 [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment)。</span><span class="sxs-lookup"><span data-stu-id="04711-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="04711-156">如果未偵測到錯誤，命令即完成，不會有回應。</span><span class="sxs-lookup"><span data-stu-id="04711-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="04711-157">如果偵測到錯誤，命令會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="04711-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="04711-158">例如，嘗試針對儲存體帳戶 SKU 傳遞不正確的值，則會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="04711-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="04711-159">如果您的範本有語法錯誤，命令會傳回錯誤，指出無法剖析範本。</span><span class="sxs-lookup"><span data-stu-id="04711-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="04711-160">訊息會指出剖析錯誤的行號和位置。</span><span class="sxs-lookup"><span data-stu-id="04711-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="04711-161">若要使用完整模式，請使用 `Mode` 參數︰</span><span class="sxs-lookup"><span data-stu-id="04711-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="04711-162">範例範本</span><span class="sxs-lookup"><span data-stu-id="04711-162">Sample template</span></span>

<span data-ttu-id="04711-163">下列範本適用於本主題中的範例。</span><span class="sxs-lookup"><span data-stu-id="04711-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="04711-164">請複製它並另存為名叫 storage.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="04711-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="04711-165">若要了解如何建立此範本，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="04711-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04711-166">Next steps</span></span>
* <span data-ttu-id="04711-167">本主題中的範例會將資源部署到您預設訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="04711-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="04711-168">若要使用不同的訂用帳戶，請參閱[管理多個 Azure 訂用帳戶](/powershell/azure/manage-subscriptions-azureps)。</span><span class="sxs-lookup"><span data-stu-id="04711-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="04711-169">如需部署範本的完整範例指令碼，請參閱 [Resource Manager 範本部署指令碼](resource-manager-samples-powershell-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="04711-170">若要了解如何在您的範本中定義參數，請參閱[了解 Azure Resource Manager 範本的結構和語法](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="04711-171">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="04711-172">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="04711-173">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="04711-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

