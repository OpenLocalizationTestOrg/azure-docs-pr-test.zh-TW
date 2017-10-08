---
title: "aaaUse PowerShell toomanage Azure 事件中樞資源 |Microsoft 文件"
description: "使用 PowerShell 模組 toocreate 和管理事件中心"
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
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="5c119-103">使用 PowerShell toomanage 事件中心的資源</span><span class="sxs-lookup"><span data-stu-id="5c119-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="5c119-104">Microsoft Azure PowerShell 是指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="5c119-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="5c119-105">本文說明如何 toouse hello[事件中樞資源管理員 PowerShell 模組](/powershell/module/azurerm.eventhub)tooprovision 和管理事件中心的實體 （命名空間，個別的事件中樞取用者群組） 使用本機的 Azure PowerShell 主控台或指令碼。</span><span class="sxs-lookup"><span data-stu-id="5c119-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="5c119-106">您也可以使用 Azure Resource Manager 範本來管理事件中樞資源。</span><span class="sxs-lookup"><span data-stu-id="5c119-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="5c119-107">如需詳細資訊，請參閱 hello 文章[建立事件中樞命名空間與使用 Azure Resource Manager 範本事件中樞與取用者群組](event-hubs-resource-manager-namespace-event-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="5c119-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c119-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c119-108">Prerequisites</span></span>

<span data-ttu-id="5c119-109">開始之前，您必須先 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5c119-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="5c119-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c119-110">An Azure subscription.</span></span> <span data-ttu-id="5c119-111">如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。</span><span class="sxs-lookup"><span data-stu-id="5c119-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="5c119-112">具備 Azure PowerShell 的電腦。</span><span class="sxs-lookup"><span data-stu-id="5c119-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="5c119-113">如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="5c119-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="5c119-114">PowerShell 指令碼及 NuGet 套件 hello.NET Framework 的基本認識。</span><span class="sxs-lookup"><span data-stu-id="5c119-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="5c119-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="5c119-115">Get started</span></span>

<span data-ttu-id="5c119-116">hello 第一個步驟是 toouse PowerShell toolog 中 tooyour Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c119-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="5c119-117">請依照下列中的 hello 指示[開始使用 Azure PowerShell cmdlet](/powershell/azure/get-started-azureps) toolog 中 tooyour Azure 帳戶，然後擷取並存取您的 Azure 訂用帳戶中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5c119-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="5c119-118">佈建事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="5c119-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="5c119-119">當使用事件中樞命名空間，您可以使用 hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace)，[新增 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace)，[移除 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace)與[組 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5c119-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="5c119-120">此範例會建立一些區域變數中 hello 指令碼。`$Namespace`和`$Location`。</span><span class="sxs-lookup"><span data-stu-id="5c119-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="5c119-121">`$Namespace`這是 hello 我們想 toowork hello 事件中樞命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="5c119-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="5c119-122">`$Location`識別 hello 資料中心中的我們將會佈建 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="5c119-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="5c119-123">`$CurrentNamespace`儲存 hello 參考命名空間中，我們擷取 （或建立）。</span><span class="sxs-lookup"><span data-stu-id="5c119-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="5c119-124">在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="5c119-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="5c119-125">Hello 指令碼的這個部分未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5c119-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="5c119-126">嘗試 tooretrieve hello 的事件中樞命名空間指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="5c119-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="5c119-127">如果找到 hello 命名空間，它會報告找到的項目。</span><span class="sxs-lookup"><span data-stu-id="5c119-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="5c119-128">如果找不到 hello 命名空間，它會建立 hello 命名空間，並接著會擷取新建立的命名空間的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c119-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="5c119-129">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="5c119-129">Create an event hub</span></span>

<span data-ttu-id="5c119-130">toocreate 事件中心，執行使用 hello 前一節中的 hello 指令碼命名空間檢查。</span><span class="sxs-lookup"><span data-stu-id="5c119-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="5c119-131">然後，使用 hello[新增 AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello 事件中心：</span><span class="sxs-lookup"><span data-stu-id="5c119-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="5c119-132">建立取用者群組</span><span class="sxs-lookup"><span data-stu-id="5c119-132">Create a consumer group</span></span>

<span data-ttu-id="5c119-133">toocreate 取用者群組內的事件中心執行 hello 命名空間和事件中樞檢查 hello 前一節中使用 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5c119-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="5c119-134">然後，使用 hello[新增 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello hello 事件中心內的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="5c119-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="5c119-135">例如：</span><span class="sxs-lookup"><span data-stu-id="5c119-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="5c119-136">設定使用者中繼資料</span><span class="sxs-lookup"><span data-stu-id="5c119-136">Set user metadata</span></span>

<span data-ttu-id="5c119-137">在執行之後 hello 指令碼 hello 前幾節中，您可以使用 hello[組 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello 屬性的取用者群組，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5c119-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="5c119-138">移除事件中樞</span><span class="sxs-lookup"><span data-stu-id="5c119-138">Remove event hub</span></span>

<span data-ttu-id="5c119-139">您建立 tooremove hello 事件中心，您可以使用 hello `Remove-*` cmdlet，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5c119-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="5c119-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c119-140">Next steps</span></span>

- <span data-ttu-id="5c119-141">請參閱 hello 完整事件中樞資源管理員 PowerShell 模組的文件[這裡](/powershell/module/azurerm.eventhub)。</span><span class="sxs-lookup"><span data-stu-id="5c119-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="5c119-142">此頁面會列出所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5c119-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="5c119-143">如需使用 Azure Resource Manager 範本資訊，請參閱 hello 文章[建立事件中樞命名空間與使用 Azure Resource Manager 範本事件中樞與取用者群組](event-hubs-resource-manager-namespace-event-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="5c119-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="5c119-144">[事件中樞 .NET 管理程式庫](event-hubs-management-libraries.md)的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5c119-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
