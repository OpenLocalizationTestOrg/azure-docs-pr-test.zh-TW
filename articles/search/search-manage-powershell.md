---
title: "使用 Powershell 指令碼管理 Azure 搜尋服務 | Microsoft Docs"
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
ms.openlocfilehash: aa51c846efef12461ec382274199bc049c42aaa3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="678fd-104">使用 PowerShell 管理 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="678fd-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="678fd-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="678fd-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="678fd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="678fd-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="678fd-107">本主題說明用來執行多種 Azure 搜尋服務管理工作的 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="678fd-107">This topic describes the PowerShell commands to perform many of the management tasks for Azure Search services.</span></span> <span data-ttu-id="678fd-108">我們將逐步建立搜尋服務、調整及管理其 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="678fd-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="678fd-109">這些命令和 [Azure 搜尋管理 REST API](http://msdn.microsoft.com/library/dn832684.aspx)中提供的管理選項相同。</span><span class="sxs-lookup"><span data-stu-id="678fd-109">These commands parallel the management options available in the [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="678fd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="678fd-110">Prerequisites</span></span>
* <span data-ttu-id="678fd-111">您必須有 Azure PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="678fd-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="678fd-112">如需指示，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="678fd-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="678fd-113">您必須在 PowerShell 中登入 Azure 訂用帳戶，如下所述。</span><span class="sxs-lookup"><span data-stu-id="678fd-113">You must be logged in to your Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="678fd-114">首先，您必須使用此命令登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="678fd-114">First, you must login to Azure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="678fd-115">在 [Microsoft Azure 登入] 對話方塊中，指定 Azure 帳戶的電子郵件地址和密碼。</span><span class="sxs-lookup"><span data-stu-id="678fd-115">Specify the email address of your Azure account and its password in the Microsoft Azure login dialog.</span></span>

<span data-ttu-id="678fd-116">或者，您可以 [非互動的方式使用服務主體登入](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="678fd-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="678fd-117">如果您有多個 Azure 訂用帳戶，您必須設定 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="678fd-117">If you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="678fd-118">如果想查看目前的訂閱帳戶清單，請執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="678fd-118">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="678fd-119">若要指定訂用帳戶，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="678fd-119">To specify the subscription, run the following command.</span></span> <span data-ttu-id="678fd-120">在下列範例中，訂用帳戶的名稱為 `ContosoSubscription`。</span><span class="sxs-lookup"><span data-stu-id="678fd-120">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-to-help-you-get-started"></a><span data-ttu-id="678fd-121">可協助您開始使用的命令</span><span class="sxs-lookup"><span data-stu-id="678fd-121">Commands to help you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register the ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once the service is fully created
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

    # Get the primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate the secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access to your indexes
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
    # This command will not return until the operation is finished
    # It can take 15 minutes or more to provision the additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in the service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="678fd-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="678fd-122">Next Steps</span></span>
<span data-ttu-id="678fd-123">您現已建立服務，接著可以採取後續步驟：建立[索引](search-what-is-an-index.md)、[查詢索引](search-query-overview.md)，最後建立並管理使用 Azure 搜尋服務的搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="678fd-123">Now that your service is created, you can take the next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="678fd-124">在 Azure 入口網站中建立 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="678fd-124">Create an Azure Search index in the Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="678fd-125">在 Azure 入口網站中使用搜尋總管查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="678fd-125">Query an Azure Search index using Search Explorer in the Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="678fd-126">設定索引子以從其他服務載入資料</span><span class="sxs-lookup"><span data-stu-id="678fd-126">Setup an indexer to load data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="678fd-127">如何以 .NET 使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="678fd-127">How to use Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="678fd-128">分析 Azure 搜尋服務的流量</span><span class="sxs-lookup"><span data-stu-id="678fd-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

