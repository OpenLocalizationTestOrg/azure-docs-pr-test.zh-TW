---
title: "Azure 堆疊 aaaUse 範本驗證程式 toocheck 範本 |Microsoft 文件"
description: "檢查部署 tooAzure 堆疊的範本"
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
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="53cf4-103">使用「範本驗證程式」來檢查 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="53cf4-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="53cf4-104">您可以使用 hello 範本驗證工具 toocheck，如果您的 Azure 資源管理員[範本](azure-stack-arm-templates.md)已準備好進行 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="53cf4-104">You can use hello template validation tool toocheck if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="53cf4-105">hello 範本驗證工具會提供 hello Azure 堆疊工具的一部分。</span><span class="sxs-lookup"><span data-stu-id="53cf4-105">hello template validation tool is available as a part of hello Azure Stack tools.</span></span> <span data-ttu-id="53cf4-106">使用 hello hello 中所述的步驟來下載 hello Azure 堆疊工具[從 GitHub 下載工具](azure-stack-powershell-download.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="53cf4-106">Download hello Azure Stack tools by using hello steps described in hello [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="53cf4-107">toovalidate 範本，您可以使用下列 PowerShell 模組的 hello 和 hello JSON 檔案位於**TemplateValidator**和**CloudCapabilities**資料夾：</span><span class="sxs-lookup"><span data-stu-id="53cf4-107">toovalidate templates, you use hello following PowerShell modules and hello JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="53cf4-108">AzureRM.CloudCapabilities.psm1 建立雲端功能 JSON 檔案代表 hello 服務和 Azure 堆疊等雲端中的版本。</span><span class="sxs-lookup"><span data-stu-id="53cf4-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing hello services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="53cf4-109">AzureRM.TemplateValidator.psm1 用雲端功能 JSON 檔案 tootest 範本來進行 Azure 堆疊中的部署。</span><span class="sxs-lookup"><span data-stu-id="53cf4-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file tootest templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="53cf4-110">AzureStackCloudCapabilities_with_AddOns_20170627.json 是預設的雲端功能檔案。</span><span class="sxs-lookup"><span data-stu-id="53cf4-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="53cf4-111">您可以建立您自己，或啟動此檔案 tooget。</span><span class="sxs-lookup"><span data-stu-id="53cf4-111">You can create your own, or use this file tooget started.</span></span> 

<span data-ttu-id="53cf4-112">在此主題中，您會為您的範本執行驗證，而且可以選擇性建置雲端功能檔案。</span><span class="sxs-lookup"><span data-stu-id="53cf4-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="53cf4-113">驗證範本</span><span class="sxs-lookup"><span data-stu-id="53cf4-113">Validate templates</span></span>
<span data-ttu-id="53cf4-114">在這些步驟中，您可以驗證範本使用 hello AzureRM.TemplateValidator PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="53cf4-114">In these steps, you validate templates by using hello AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="53cf4-115">您可以使用您自己的範本，或驗證 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)。</span><span class="sxs-lookup"><span data-stu-id="53cf4-115">You can use your own templates, or validate hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="53cf4-116">匯入 hello AzureRM.TemplateValidator.psm1 PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="53cf4-116">Import hello AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="53cf4-117">執行 hello 範本驗證程式：</span><span class="sxs-lookup"><span data-stu-id="53cf4-117">Run hello template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="53cf4-118">任何範本驗證警告或錯誤記錄的 toohello PowerShell 主控台中，而且也會記錄的 tooan hello 來源目錄中的 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="53cf4-118">Any template validation warnings or errors are logged toohello PowerShell console, and are also logged tooan HTML file in hello source directory.</span></span> <span data-ttu-id="53cf4-119">Hello 驗證報表輸出的範例看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="53cf4-119">An example of hello validation report output looks like this:</span></span>

![範例驗證報告](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="53cf4-121">參數</span><span class="sxs-lookup"><span data-stu-id="53cf4-121">Parameters</span></span>

| <span data-ttu-id="53cf4-122">參數</span><span class="sxs-lookup"><span data-stu-id="53cf4-122">Parameter</span></span> | <span data-ttu-id="53cf4-123">說明</span><span class="sxs-lookup"><span data-stu-id="53cf4-123">Description</span></span> | <span data-ttu-id="53cf4-124">必要</span><span class="sxs-lookup"><span data-stu-id="53cf4-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="53cf4-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="53cf4-125">TemplatePath</span></span> | <span data-ttu-id="53cf4-126">指定 hello 路徑 toorecursively 尋找資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="53cf4-126">Specifies hello path toorecursively find Resource Manager templates</span></span> | <span data-ttu-id="53cf4-127">是</span><span class="sxs-lookup"><span data-stu-id="53cf4-127">Yes</span></span> | 
| <span data-ttu-id="53cf4-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="53cf4-128">TemplatePattern</span></span> | <span data-ttu-id="53cf4-129">指定範本檔案 toomatch hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="53cf4-129">Specifies hello name of template files toomatch.</span></span> | <span data-ttu-id="53cf4-130">否</span><span class="sxs-lookup"><span data-stu-id="53cf4-130">No</span></span> |
| <span data-ttu-id="53cf4-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="53cf4-131">CapabilitiesPath</span></span> | <span data-ttu-id="53cf4-132">指定 hello 路徑 toocloud 功能 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="53cf4-132">Specifies hello path toocloud capabilities JSON file</span></span> | <span data-ttu-id="53cf4-133">是</span><span class="sxs-lookup"><span data-stu-id="53cf4-133">Yes</span></span> | 
| <span data-ttu-id="53cf4-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="53cf4-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="53cf4-135">包括 IaaS 資源 (例如 VM 大小與 VM 擴充功能) 的評估</span><span class="sxs-lookup"><span data-stu-id="53cf4-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="53cf4-136">否</span><span class="sxs-lookup"><span data-stu-id="53cf4-136">No</span></span> |
| <span data-ttu-id="53cf4-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="53cf4-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="53cf4-138">包括儲存體資源 (例如 SKU 類型) 的評估</span><span class="sxs-lookup"><span data-stu-id="53cf4-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="53cf4-139">否</span><span class="sxs-lookup"><span data-stu-id="53cf4-139">No</span></span> |
| <span data-ttu-id="53cf4-140">報告</span><span class="sxs-lookup"><span data-stu-id="53cf4-140">Report</span></span> | <span data-ttu-id="53cf4-141">指定名稱的 hello 產生 HTML 報表</span><span class="sxs-lookup"><span data-stu-id="53cf4-141">Specifies name of hello generated HTML report</span></span> | <span data-ttu-id="53cf4-142">否</span><span class="sxs-lookup"><span data-stu-id="53cf4-142">No</span></span> |
| <span data-ttu-id="53cf4-143">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="53cf4-143">Verbose</span></span> | <span data-ttu-id="53cf4-144">記錄錯誤和警告 toohello 主控台</span><span class="sxs-lookup"><span data-stu-id="53cf4-144">Logs errors and warnings toohello console</span></span> | <span data-ttu-id="53cf4-145">否</span><span class="sxs-lookup"><span data-stu-id="53cf4-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="53cf4-146">範例</span><span class="sxs-lookup"><span data-stu-id="53cf4-146">Examples</span></span>
<span data-ttu-id="53cf4-147">這個範例會驗證所有 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates)下載至本機，並也會都驗證 hello VM 大小和擴充功能，針對 Azure 堆疊開發套件功能。</span><span class="sxs-lookup"><span data-stu-id="53cf4-147">This example validates all hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates hello VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="53cf4-148">建置雲端功能檔案</span><span class="sxs-lookup"><span data-stu-id="53cf4-148">Build cloud capabilities file</span></span>
<span data-ttu-id="53cf4-149">hello 下載的檔案包含預設值*AzureStackCloudCapabilities_with_AddOns_20170627.json*檔案，其中描述 Azure 堆疊開發套件中可用的 hello 服務版本與安裝的 PaaS 服務。</span><span class="sxs-lookup"><span data-stu-id="53cf4-149">hello downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes hello service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="53cf4-150">如果您安裝額外的資源提供者，您可以使用 hello AzureRM.CloudCapabilities PowerShell 模組 toobuild 包括 hello 新服務的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="53cf4-150">If you install additional Resource Providers, you can use hello AzureRM.CloudCapabilities PowerShell module toobuild a JSON file including hello new services.</span></span>  

1.  <span data-ttu-id="53cf4-151">請確定您已連線 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="53cf4-151">Make sure you have connectivity tooAzure Stack.</span></span>  <span data-ttu-id="53cf4-152">您可以從 hello Azure 堆疊開發套件主機，執行下列步驟，或者您可以使用[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect 從您的工作站。</span><span class="sxs-lookup"><span data-stu-id="53cf4-152">These steps can be performed from hello Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect from your workstation.</span></span> 
2.  <span data-ttu-id="53cf4-153">匯入 hello AzureRM.CloudCapabilities PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="53cf4-153">Import hello AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="53cf4-154">使用 Get CloudCapabilities hello cmdlet tooretrieve 服務版本，並建立的雲端功能的 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="53cf4-154">Use hello Get-CloudCapabilities cmdlet tooretrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="53cf4-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53cf4-155">Next steps</span></span>
 - [<span data-ttu-id="53cf4-156">部署範本 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="53cf4-156">Deploy templates tooAzure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="53cf4-157">[部署 Azure Stack 的範本] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="53cf4-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

