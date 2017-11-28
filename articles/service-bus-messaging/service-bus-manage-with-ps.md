---
title: "aaaUse PowerShell toomanage Azure 服務匯流排資源 |Microsoft 文件"
description: "使用 PowerShell 模組 toocreate 和管理服務匯流排資源"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="70067-103">使用 PowerShell toomanage 服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="70067-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="70067-104">Microsoft Azure PowerShell 是指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="70067-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="70067-105">本文說明如何 toouse hello[服務匯流排資源管理員 PowerShell 模組](/powershell/module/azurerm.servicebus)tooprovision 和管理服務匯流排實體 （命名空間、 佇列、 主題和訂用帳戶） 使用本機的 Azure PowerShell 主控台或指令碼。</span><span class="sxs-lookup"><span data-stu-id="70067-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="70067-106">您也可以使用 Azure Resource Manager 範本來管理服務匯流排實體。</span><span class="sxs-lookup"><span data-stu-id="70067-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="70067-107">如需詳細資訊，請參閱 hello 文章[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70067-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70067-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="70067-108">Prerequisites</span></span>

<span data-ttu-id="70067-109">開始之前，您必須先 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="70067-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="70067-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70067-110">An Azure subscription.</span></span> <span data-ttu-id="70067-111">如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。</span><span class="sxs-lookup"><span data-stu-id="70067-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="70067-112">具備 Azure PowerShell 的電腦。</span><span class="sxs-lookup"><span data-stu-id="70067-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="70067-113">如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="70067-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="70067-114">PowerShell 指令碼及 NuGet 套件 hello.NET Framework 的基本認識。</span><span class="sxs-lookup"><span data-stu-id="70067-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="70067-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="70067-115">Get started</span></span>

<span data-ttu-id="70067-116">hello 第一個步驟是 toouse PowerShell toolog 中 tooyour Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70067-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="70067-117">請依照下列中的 hello 指示[開始使用 Azure PowerShell cmdlet](/powershell/azure/get-started-azureps) toolog tooyour Azure 帳戶和擷取及存取您的 Azure 訂用帳戶中的 hello 資源中。</span><span class="sxs-lookup"><span data-stu-id="70067-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="70067-118">佈建服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="70067-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="70067-119">當使用服務匯流排命名空間，您可以使用 hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace)，[新增 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace)，[移除 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace)，和[組 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="70067-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="70067-120">此範例會建立一些區域變數中 hello 指令碼。`$Namespace`和`$Location`。</span><span class="sxs-lookup"><span data-stu-id="70067-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="70067-121">`$Namespace`這是 hello 我們想 toowork hello 服務匯流排命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="70067-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="70067-122">`$Location`識別 hello 資料中心中的我們將會佈建 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="70067-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="70067-123">`$CurrentNamespace`儲存 hello 參考命名空間中，我們擷取 （或建立）。</span><span class="sxs-lookup"><span data-stu-id="70067-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="70067-124">在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="70067-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="70067-125">Hello 指令碼的這個部分未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="70067-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="70067-126">嘗試 tooretrieve hello 與服務匯流排命名空間指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="70067-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="70067-127">如果找到 hello 命名空間，它會報告找到的項目。</span><span class="sxs-lookup"><span data-stu-id="70067-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="70067-128">如果找不到 hello 命名空間，它會建立 hello 命名空間，並接著會擷取新建立的命名空間的 hello。</span><span class="sxs-lookup"><span data-stu-id="70067-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="70067-129">建立命名空間授權規則</span><span class="sxs-lookup"><span data-stu-id="70067-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="70067-130">hello 下列範例示範如何使用 toomanage 命名空間授權規則 hello[新增 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule)， [Get AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule)，[組 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule)，和[移除 AzureRmServiceBusNamespaceAuthorizationRule cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule)。</span><span class="sxs-lookup"><span data-stu-id="70067-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="70067-131">建立佇列</span><span class="sxs-lookup"><span data-stu-id="70067-131">Create a queue</span></span>

<span data-ttu-id="70067-132">toocreate 佇列或主題時，執行使用 hello 前一節中的 hello 指令碼的命名空間檢查。</span><span class="sxs-lookup"><span data-stu-id="70067-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="70067-133">然後，建立 hello 佇列：</span><span class="sxs-lookup"><span data-stu-id="70067-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="70067-134">修改佇列屬性</span><span class="sxs-lookup"><span data-stu-id="70067-134">Modify queue properties</span></span>

<span data-ttu-id="70067-135">在執行之後 hello 指令碼 hello 前面一節中，您可以使用 hello[組 AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello 佇列，如 hello 下列範例所示的屬性：</span><span class="sxs-lookup"><span data-stu-id="70067-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="70067-136">佈建其他服務匯流排實體</span><span class="sxs-lookup"><span data-stu-id="70067-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="70067-137">您可以使用 hello[服務匯流排 PowerShell 模組](/powershell/module/azurerm.servicebus)tooprovision 其他實體，例如主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="70067-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="70067-138">這些指令程式是語法類似 toohello 佇列建立指令程式 hello 上一節所示。</span><span class="sxs-lookup"><span data-stu-id="70067-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70067-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70067-139">Next steps</span></span>

- <span data-ttu-id="70067-140">請參閱 hello 完整服務匯流排資源管理員 PowerShell 模組的文件[這裡](/powershell/module/azurerm.servicebus)。</span><span class="sxs-lookup"><span data-stu-id="70067-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="70067-141">此頁面會列出所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="70067-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="70067-142">如需使用 Azure Resource Manager 範本資訊，請參閱 hello 文章[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70067-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="70067-143">[服務匯流排 .NET 管理程式庫](service-bus-management-libraries.md)的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="70067-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="70067-144">有一些替代 toomanage 服務匯流排實體，如下列部落格文章所述：</span><span class="sxs-lookup"><span data-stu-id="70067-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="70067-145">如何 toocreate 服務匯流排佇列、 主題和訂用帳戶的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="70067-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="70067-146">如何為服務匯流排命名空間，並使用 PowerShell 指令碼的事件中樞的 toocreate</span><span class="sxs-lookup"><span data-stu-id="70067-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="70067-147">服務匯流排 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="70067-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
