---
title: "使用「範本驗證程式」來檢查 Azure Stack 的範本 | Microsoft Docs"
description: "檢查要部署到 Azure Stack 的範本"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: bb1d624f4c73bcd5f41dde2d0b13c57c880eca05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="756e6-103">使用「範本驗證程式」來檢查 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="756e6-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="756e6-104">您可以使用範本驗證工具來檢查您的 Azure Resource Manager [範本](azure-stack-arm-templates.md)是否準備好供 Azure Stack 使用。</span><span class="sxs-lookup"><span data-stu-id="756e6-104">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="756e6-105">範本驗證工具是 Azure Stack 工具的一部分。</span><span class="sxs-lookup"><span data-stu-id="756e6-105">The template validation tool is available as a part of the Azure Stack tools.</span></span> <span data-ttu-id="756e6-106">使用[從 GitHub 下載工具](azure-stack-powershell-download.md)文章中所述的步驟下載 Azure Stack 工具。</span><span class="sxs-lookup"><span data-stu-id="756e6-106">Download the Azure Stack tools by using the steps described in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="756e6-107">若要驗證範本，您必須使用位於 [TemplateValidator] 與 [CloudCapabilities] 資料夾的下列 PowerShell 模組與 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="756e6-107">To validate templates, you use the following PowerShell modules and the JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="756e6-108">AzureRM.CloudCapabilities.psm1 會建立雲端功能 JSON 檔案，該檔案代表雲端 (例如 Azure Stack) 中的服務與版本。</span><span class="sxs-lookup"><span data-stu-id="756e6-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="756e6-109">AzureRM.TemplateValidator.psm1 使用雲端功能 JSON 檔案來測試將在 Azure Stack 中部署的範本。</span><span class="sxs-lookup"><span data-stu-id="756e6-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="756e6-110">AzureStackCloudCapabilities_with_AddOns_20170627.json 是預設的雲端功能檔案。</span><span class="sxs-lookup"><span data-stu-id="756e6-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="756e6-111">您可以自行建立檔案，或從此檔案開始。</span><span class="sxs-lookup"><span data-stu-id="756e6-111">You can create your own, or use this file to get started.</span></span> 

<span data-ttu-id="756e6-112">在此主題中，您會為您的範本執行驗證，而且可以選擇性建置雲端功能檔案。</span><span class="sxs-lookup"><span data-stu-id="756e6-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="756e6-113">驗證範本</span><span class="sxs-lookup"><span data-stu-id="756e6-113">Validate templates</span></span>
<span data-ttu-id="756e6-114">在這些步驟中，您會使用 AzureRM.TemplateValidator PowerShell 模組來驗證範本。</span><span class="sxs-lookup"><span data-stu-id="756e6-114">In these steps, you validate templates by using the AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="756e6-115">您可以使用您自己的範本，或驗證 [Azure Stack 快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)。</span><span class="sxs-lookup"><span data-stu-id="756e6-115">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="756e6-116">匯入 AzureRM.TemplateValidator.psm1 PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="756e6-116">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="756e6-117">執行範本驗證程式：</span><span class="sxs-lookup"><span data-stu-id="756e6-117">Run the template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path to template.json or template folder> `
    -CapabilitiesPath <path to cloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="756e6-118">所有範本驗證警告或錯誤都會記錄到 PowerShell 主控台，而且也會記錄到來源目錄中的 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="756e6-118">Any template validation warnings or errors are logged to the PowerShell console, and are also logged to an HTML file in the source directory.</span></span> <span data-ttu-id="756e6-119">驗證報告輸出的範例看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="756e6-119">An example of the validation report output looks like this:</span></span>

![範例驗證報告](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="756e6-121">參數</span><span class="sxs-lookup"><span data-stu-id="756e6-121">Parameters</span></span>

| <span data-ttu-id="756e6-122">參數</span><span class="sxs-lookup"><span data-stu-id="756e6-122">Parameter</span></span> | <span data-ttu-id="756e6-123">說明</span><span class="sxs-lookup"><span data-stu-id="756e6-123">Description</span></span> | <span data-ttu-id="756e6-124">必要</span><span class="sxs-lookup"><span data-stu-id="756e6-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="756e6-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="756e6-125">TemplatePath</span></span> | <span data-ttu-id="756e6-126">指定要在其中遞迴尋找 Resource Manager 範本的路徑</span><span class="sxs-lookup"><span data-stu-id="756e6-126">Specifies the path to recursively find Resource Manager templates</span></span> | <span data-ttu-id="756e6-127">是</span><span class="sxs-lookup"><span data-stu-id="756e6-127">Yes</span></span> | 
| <span data-ttu-id="756e6-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="756e6-128">TemplatePattern</span></span> | <span data-ttu-id="756e6-129">指定要比對的範本檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="756e6-129">Specifies the name of template files to match.</span></span> | <span data-ttu-id="756e6-130">否</span><span class="sxs-lookup"><span data-stu-id="756e6-130">No</span></span> |
| <span data-ttu-id="756e6-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="756e6-131">CapabilitiesPath</span></span> | <span data-ttu-id="756e6-132">指定雲端功能 JSON 檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="756e6-132">Specifies the path to cloud capabilities JSON file</span></span> | <span data-ttu-id="756e6-133">是</span><span class="sxs-lookup"><span data-stu-id="756e6-133">Yes</span></span> | 
| <span data-ttu-id="756e6-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="756e6-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="756e6-135">包括 IaaS 資源 (例如 VM 大小與 VM 擴充功能) 的評估</span><span class="sxs-lookup"><span data-stu-id="756e6-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="756e6-136">否</span><span class="sxs-lookup"><span data-stu-id="756e6-136">No</span></span> |
| <span data-ttu-id="756e6-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="756e6-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="756e6-138">包括儲存體資源 (例如 SKU 類型) 的評估</span><span class="sxs-lookup"><span data-stu-id="756e6-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="756e6-139">否</span><span class="sxs-lookup"><span data-stu-id="756e6-139">No</span></span> |
| <span data-ttu-id="756e6-140">報告</span><span class="sxs-lookup"><span data-stu-id="756e6-140">Report</span></span> | <span data-ttu-id="756e6-141">指定所產生之 HTML 報告的名稱</span><span class="sxs-lookup"><span data-stu-id="756e6-141">Specifies name of the generated HTML report</span></span> | <span data-ttu-id="756e6-142">否</span><span class="sxs-lookup"><span data-stu-id="756e6-142">No</span></span> |
| <span data-ttu-id="756e6-143">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="756e6-143">Verbose</span></span> | <span data-ttu-id="756e6-144">將錯誤與警告記錄到主控台</span><span class="sxs-lookup"><span data-stu-id="756e6-144">Logs errors and warnings to the console</span></span> | <span data-ttu-id="756e6-145">否</span><span class="sxs-lookup"><span data-stu-id="756e6-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="756e6-146">範例</span><span class="sxs-lookup"><span data-stu-id="756e6-146">Examples</span></span>
<span data-ttu-id="756e6-147">此範例會驗證所有下載到本機的 [Azure Stack 快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)，而且也會驗證 VM 大小與擴充功能是否符合 Azure Stack 開發套件功能。</span><span class="sxs-lookup"><span data-stu-id="756e6-147">This example validates all the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates the VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="756e6-148">建置雲端功能檔案</span><span class="sxs-lookup"><span data-stu-id="756e6-148">Build cloud capabilities file</span></span>
<span data-ttu-id="756e6-149">下載的檔案包括預設的 *AzureStackCloudCapabilities_with_AddOns_20170627.json* 檔案，此檔案描述 Azure Stack 開發套件中可用的服務版本 (在已安裝 PaaS 服務的情況下)。</span><span class="sxs-lookup"><span data-stu-id="756e6-149">The downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes the service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="756e6-150">若您安裝其他資源提供者，您可以使用 AzureRM.CloudCapabilities PowerShell 模組來建置 JSON 檔案 (包括新服務)。</span><span class="sxs-lookup"><span data-stu-id="756e6-150">If you install additional Resource Providers, you can use the AzureRM.CloudCapabilities PowerShell module to build a JSON file including the new services.</span></span>  

1.  <span data-ttu-id="756e6-151">確定您能順利連線到 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="756e6-151">Make sure you have connectivity to Azure Stack.</span></span>  <span data-ttu-id="756e6-152">這些步驟可從 Azure Stack 開發套件主機執行，或者您可以使用 [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) 從您的工作站連線。</span><span class="sxs-lookup"><span data-stu-id="756e6-152">These steps can be performed from the Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) to connect from your workstation.</span></span> 
2.  <span data-ttu-id="756e6-153">匯入 AzureRM.CloudCapabilities PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="756e6-153">Import the AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="756e6-154">使用 Get-CloudCapabilities Cmdlet 來擷取服務版本並建立雲端功能 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="756e6-154">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="756e6-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="756e6-155">Next steps</span></span>
 - [<span data-ttu-id="756e6-156">將範本部署到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="756e6-156">Deploy templates to Azure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="756e6-157">[部署 Azure Stack 的範本] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="756e6-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

