---
title: "使用 Powershell 指令碼的 Azure 搜尋 aaaManage |Microsoft 文件"
description: "使用 PowerShell 指令碼管理 Azure 搜尋服務。 建立或更新 Azure 搜尋服務，並管理 Azure 搜尋服務的系統管理金鑰"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="a6baa-104">使用 PowerShell 管理 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="a6baa-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6baa-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="a6baa-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="a6baa-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6baa-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="a6baa-107">本主題描述 hello PowerShell 命令 tooperform 許多 hello Azure 搜尋服務的管理工作。</span><span class="sxs-lookup"><span data-stu-id="a6baa-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="a6baa-108">我們將逐步建立搜尋服務、調整及管理其 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6baa-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="a6baa-109">這些命令的平行 hello 管理選項提供 hello [Azure 搜尋管理 REST API](http://msdn.microsoft.com/library/dn832684.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a6baa-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6baa-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a6baa-110">Prerequisites</span></span>
* <span data-ttu-id="a6baa-111">您必須有 Azure PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a6baa-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="a6baa-112">如需指示，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a6baa-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a6baa-113">您必須登入 tooyour 如下所述的 PowerShell 中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6baa-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="a6baa-114">首先，您必須使用此命令的登入 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a6baa-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="a6baa-115">Hello Microsoft Azure 登入 對話方塊中指定您的 Azure 帳戶並將其密碼的 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="a6baa-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="a6baa-116">或者，您可以 [非互動的方式使用服務主體登入](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="a6baa-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="a6baa-117">如果您有多個 Azure 訂用帳戶，您需要 tooset 您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6baa-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="a6baa-118">toosee 一份您目前的訂用帳戶，執行此命令。</span><span class="sxs-lookup"><span data-stu-id="a6baa-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="a6baa-119">toospecify hello 訂用帳戶，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="a6baa-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="a6baa-120">在下列範例的 hello，hello 訂用帳戶名稱是`ContosoSubscription`。</span><span class="sxs-lookup"><span data-stu-id="a6baa-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="a6baa-121">命令 toohelp 快速入門</span><span class="sxs-lookup"><span data-stu-id="a6baa-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="a6baa-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6baa-122">Next Steps</span></span>
<span data-ttu-id="a6baa-123">現在，建立您的服務時，您可以採取 hello 接下來的步驟： 建置[索引](search-what-is-an-index.md)，[查詢索引](search-query-overview.md)，最後建立並管理自己的搜尋應用程式使用 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="a6baa-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="a6baa-124">在 hello Azure 入口網站中建立 Azure 搜尋索引</span><span class="sxs-lookup"><span data-stu-id="a6baa-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="a6baa-125">查詢 Azure 搜尋索引使用 hello Azure 入口網站中的搜尋總管</span><span class="sxs-lookup"><span data-stu-id="a6baa-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="a6baa-126">安裝程式從其他服務的索引子 tooload 資料</span><span class="sxs-lookup"><span data-stu-id="a6baa-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="a6baa-127">如何在.NET 中的 toouse Azure 搜尋</span><span class="sxs-lookup"><span data-stu-id="a6baa-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="a6baa-128">分析 Azure 搜尋服務的流量</span><span class="sxs-lookup"><span data-stu-id="a6baa-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

