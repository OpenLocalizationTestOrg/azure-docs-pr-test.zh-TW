---
title: "Azure 堆疊 aaaDevelop 範本 |Microsoft 文件"
description: "了解 Azure Stack 範本最佳做法"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="87ec6-103">Azure Resource Manager 範本考量</span><span class="sxs-lookup"><span data-stu-id="87ec6-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="87ec6-104">當您開發應用程式時，它是 Azure 和 Azure 堆疊之間的重要 tooensure 範本可攜性。</span><span class="sxs-lookup"><span data-stu-id="87ec6-104">As you develop your application, it is important tooensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="87ec6-105">本主題提供開發 Azure 資源管理員的考量[範本](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf)，因此您應用程式和測試部署，並在 Azure 中的沒有存取 tooan Azure 堆疊環境可以原型。</span><span class="sxs-lookup"><span data-stu-id="87ec6-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access tooan Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="87ec6-106">公用命名空間</span><span class="sxs-lookup"><span data-stu-id="87ec6-106">Public namespaces</span></span>
<span data-ttu-id="87ec6-107">因為 Azure 堆疊裝載在您的資料中心，它會有不同的服務端點的命名空間比 hello Azure 公用雲端。</span><span class="sxs-lookup"><span data-stu-id="87ec6-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than hello Azure public cloud.</span></span> <span data-ttu-id="87ec6-108">如此一來，資源管理員範本中的硬式編碼公用端點失敗時嘗試 toodeploy 它們 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="87ec6-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try toodeploy them tooAzure Stack.</span></span> <span data-ttu-id="87ec6-109">相反地，您可以使用 hello*參考*和*串連*函式 toodynamically 建置在部署期間從 hello 資源提供者擷取的值為基礎的 hello 服務端點。</span><span class="sxs-lookup"><span data-stu-id="87ec6-109">Instead, you can use hello *reference* and *concatenate* function toodynamically build hello service endpoint based on values retrieved from hello resource provider during deployment.</span></span> <span data-ttu-id="87ec6-110">例如，而不要指定*account>.blob.core.windows.net*在範本中，擷取 hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically 設定 hello *osDisk.URI*端點：</span><span class="sxs-lookup"><span data-stu-id="87ec6-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically set hello *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="87ec6-111">API 版本控制</span><span class="sxs-lookup"><span data-stu-id="87ec6-111">API versioning</span></span>
<span data-ttu-id="87ec6-112">Azure 服務版本在 Azure 與 Azure Stack 之間可能不同。</span><span class="sxs-lookup"><span data-stu-id="87ec6-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="87ec6-113">每個資源需要 hello api 版本屬性，定義所提供的 hello 能力。</span><span class="sxs-lookup"><span data-stu-id="87ec6-113">Each resource requires hello apiVersion attribute, which defines hello capabilities offered.</span></span> <span data-ttu-id="87ec6-114">Azure 堆疊，遵循 hello tooensure API 版本相容性是有效的應用程式開發介面版本，每個資源提供者：</span><span class="sxs-lookup"><span data-stu-id="87ec6-114">tooensure API version compatibility in Azure Stack, hello following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="87ec6-115">資源提供者</span><span class="sxs-lookup"><span data-stu-id="87ec6-115">Resource Provider</span></span> | <span data-ttu-id="87ec6-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="87ec6-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="87ec6-117">計算</span><span class="sxs-lookup"><span data-stu-id="87ec6-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="87ec6-118">網路</span><span class="sxs-lookup"><span data-stu-id="87ec6-118">Network</span></span> |<span data-ttu-id="87ec6-119">`'2015-06-15'`、`'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="87ec6-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="87ec6-120">儲存體</span><span class="sxs-lookup"><span data-stu-id="87ec6-120">Storage</span></span> |<span data-ttu-id="87ec6-121">`'2016-01-01'`、`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="87ec6-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="87ec6-122">KeyVault</span><span class="sxs-lookup"><span data-stu-id="87ec6-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="87ec6-123">App Service</span><span class="sxs-lookup"><span data-stu-id="87ec6-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="87ec6-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="87ec6-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="87ec6-125">SQL</span><span class="sxs-lookup"><span data-stu-id="87ec6-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="87ec6-126">範本函式</span><span class="sxs-lookup"><span data-stu-id="87ec6-126">Template functions</span></span>
<span data-ttu-id="87ec6-127">資源管理員[函式](../azure-resource-manager/resource-group-template-functions.md)提供功能的必要的 toobuild 動態範本。</span><span class="sxs-lookup"><span data-stu-id="87ec6-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required toobuild dynamic templates.</span></span> <span data-ttu-id="87ec6-128">做為範例，您可以針對如下工作使用函式：</span><span class="sxs-lookup"><span data-stu-id="87ec6-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="87ec6-129">串連或修剪字串</span><span class="sxs-lookup"><span data-stu-id="87ec6-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="87ec6-130">參考來自其他資源的值</span><span class="sxs-lookup"><span data-stu-id="87ec6-130">Reference values from other resources</span></span>
* <span data-ttu-id="87ec6-131">逐一查看資源 toodeploy 上多個執行個體</span><span class="sxs-lookup"><span data-stu-id="87ec6-131">Iterating on resources toodeploy multiple instances</span></span> 

<span data-ttu-id="87ec6-132">當您建置範本時，某些函式在 Azure Stack 開發套件中不提供，因此不應該使用這些函式。</span><span class="sxs-lookup"><span data-stu-id="87ec6-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="87ec6-133">這些函式是：</span><span class="sxs-lookup"><span data-stu-id="87ec6-133">These functions are:</span></span>

* <span data-ttu-id="87ec6-134">Skip</span><span class="sxs-lookup"><span data-stu-id="87ec6-134">Skip</span></span>
* <span data-ttu-id="87ec6-135">Take</span><span class="sxs-lookup"><span data-stu-id="87ec6-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="87ec6-136">資源位置</span><span class="sxs-lookup"><span data-stu-id="87ec6-136">Resource location</span></span>
<span data-ttu-id="87ec6-137">資源管理員範本在部署期間使用的位置屬性 tooplace 資源。</span><span class="sxs-lookup"><span data-stu-id="87ec6-137">Resource Manager templates use a location attribute tooplace resources during deployment.</span></span> <span data-ttu-id="87ec6-138">在 Azure 中，位置，請參閱南美洲西部等 tooa 區域。</span><span class="sxs-lookup"><span data-stu-id="87ec6-138">In Azure, locations refer tooa region like West US or South America.</span></span> <span data-ttu-id="87ec6-139">在 Azure Stack 中，位置則不同，因為 Azure Stack 位於您的資料中心。</span><span class="sxs-lookup"><span data-stu-id="87ec6-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="87ec6-140">tooensure 範本可在 Azure 與 Azure 堆疊之間傳輸，您應該參考 hello 資源群組的位置，在您將部署個別的資源。</span><span class="sxs-lookup"><span data-stu-id="87ec6-140">tooensure templates are transferrable between Azure and Azure Stack, you should reference hello resource group location as you deploy individual resources.</span></span> <span data-ttu-id="87ec6-141">您可以使用`[resourceGroup().Location]`tooensure 繼承的所有資源 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="87ec6-141">You can do this using `[resourceGroup().Location]` tooensure all resources inherit hello resource group location.</span></span>  <span data-ttu-id="87ec6-142">hello 下列資源管理員範本摘錄是部署的儲存體帳戶時使用此函式的範例：</span><span class="sxs-lookup"><span data-stu-id="87ec6-142">hello following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="87ec6-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87ec6-143">Next steps</span></span>
* [<span data-ttu-id="87ec6-144">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="87ec6-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="87ec6-145">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="87ec6-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="87ec6-146">使用 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="87ec6-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

