---
title: "使用 PowerShell 來管理 Azure 事件中樞資源 | Microsoft Docs"
description: "使用 PowerShell 模組來建立和管理事件中樞"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="e0aca-103">使用 PowerShell 來管理事件中樞資源</span><span class="sxs-lookup"><span data-stu-id="e0aca-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="e0aca-104">Microsoft Azure PowerShell 是一種指令碼環境，可讓您用來控制及自動化 Azure 服務的部署和管理。</span><span class="sxs-lookup"><span data-stu-id="e0aca-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="e0aca-105">本文說明如何使用本機 Azure PowerShell 主控台或指令碼，運用[事件中樞 Resource Manager PowerShell 模組](/powershell/module/azurerm.eventhub)來佈建和管理事件中樞實體 (命名空間、個別事件中樞和取用者群組)。</span><span class="sxs-lookup"><span data-stu-id="e0aca-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="e0aca-106">您也可以使用 Azure Resource Manager 範本來管理事件中樞資源。</span><span class="sxs-lookup"><span data-stu-id="e0aca-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="e0aca-107">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本建立事件中樞命名空間與事件中樞和取用者群組](event-hubs-resource-manager-namespace-event-hub.md)文章。</span><span class="sxs-lookup"><span data-stu-id="e0aca-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0aca-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="e0aca-108">Prerequisites</span></span>

<span data-ttu-id="e0aca-109">在開始之前，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e0aca-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="e0aca-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0aca-110">An Azure subscription.</span></span> <span data-ttu-id="e0aca-111">如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。</span><span class="sxs-lookup"><span data-stu-id="e0aca-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="e0aca-112">具備 Azure PowerShell 的電腦。</span><span class="sxs-lookup"><span data-stu-id="e0aca-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="e0aca-113">如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="e0aca-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="e0aca-114">大致了解 PowerShell 指令碼、NuGet 封裝和 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="e0aca-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="e0aca-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="e0aca-115">Get started</span></span>

<span data-ttu-id="e0aca-116">第一個步驟是使用 PowerShell 來登入 Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0aca-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="e0aca-117">遵循[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps) 中的指示登入您的 Azure 帳戶，然後擷取及存取 Azure 訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="e0aca-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="e0aca-118">佈建事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="e0aca-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="e0aca-119">使用事件中樞命名空間時，您可以使用 [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace)、[New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace)、[Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) 和 [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e0aca-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="e0aca-120">這個範例會在指令碼中建立幾個區域變數：`$Namespace` 和 `$Location`。</span><span class="sxs-lookup"><span data-stu-id="e0aca-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="e0aca-121">`$Namespace` 為我們想要使用之事件中樞命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0aca-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="e0aca-122">`$Location` 會識別我們將在其中佈建命名空間的資料中心。</span><span class="sxs-lookup"><span data-stu-id="e0aca-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="e0aca-123">`$CurrentNamespace` 會儲存我們擷取 (或建立) 的參考命名空間。</span><span class="sxs-lookup"><span data-stu-id="e0aca-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="e0aca-124">在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="e0aca-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="e0aca-125">這部分的指令碼會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="e0aca-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="e0aca-126">嘗試擷取具有指定名稱的事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="e0aca-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="e0aca-127">如果找到命名空間，它會回報找到的項目。</span><span class="sxs-lookup"><span data-stu-id="e0aca-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="e0aca-128">如果找不到命名空間，它會建立命名空間，然後擷取新建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="e0aca-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="e0aca-129">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="e0aca-129">Create an event hub</span></span>

<span data-ttu-id="e0aca-130">若要建立事件中樞，請使用上一節中的指令碼來執行命名空間檢查。</span><span class="sxs-lookup"><span data-stu-id="e0aca-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="e0aca-131">然後使用 [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) Cmdlet，以建立事件中樞：</span><span class="sxs-lookup"><span data-stu-id="e0aca-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="e0aca-132">建立取用者群組</span><span class="sxs-lookup"><span data-stu-id="e0aca-132">Create a consumer group</span></span>

<span data-ttu-id="e0aca-133">若要在事件中樞內建立取用者群組，請使用上一節中的指令碼來執行命名空間和事件中樞檢查。</span><span class="sxs-lookup"><span data-stu-id="e0aca-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="e0aca-134">然後使用 [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) Cmdlet，以在事件中樞內建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="e0aca-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="e0aca-135">例如：</span><span class="sxs-lookup"><span data-stu-id="e0aca-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="e0aca-136">設定使用者中繼資料</span><span class="sxs-lookup"><span data-stu-id="e0aca-136">Set user metadata</span></span>

<span data-ttu-id="e0aca-137">執行先前各節中的指令碼之後，您可以使用 [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) Cmdlet 來更新取用者群組的屬性，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="e0aca-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="e0aca-138">移除事件中樞</span><span class="sxs-lookup"><span data-stu-id="e0aca-138">Remove event hub</span></span>

<span data-ttu-id="e0aca-139">若要移除您所建立的事件中樞，可以使用 `Remove-*` Cmdlet，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="e0aca-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="e0aca-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0aca-140">Next steps</span></span>

- <span data-ttu-id="e0aca-141">請在[這裡](/powershell/module/azurerm.eventhub)參閱完整的事件中樞 Resource Manager PowerShell 模組文件。</span><span class="sxs-lookup"><span data-stu-id="e0aca-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="e0aca-142">此頁面會列出所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e0aca-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="e0aca-143">如需使用 Azure Resource Manager 範本的相關資訊，請參閱[使用 Azure Resource Manager 範本建立事件中樞命名空間與事件中樞和取用者群組](event-hubs-resource-manager-namespace-event-hub.md)文章。</span><span class="sxs-lookup"><span data-stu-id="e0aca-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="e0aca-144">[事件中樞 .NET 管理程式庫](event-hubs-management-libraries.md)的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e0aca-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
