---
title: "使用 PowerShell 來管理 Azure 服務匯流排資源 | Microsoft Docs"
description: "使用 PowerShell 模組來建立及管理服務匯流排資源"
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
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="6d553-103">使用 PowerShell 來管理服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="6d553-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="6d553-104">Microsoft Azure PowerShell 是一種指令碼環境，可讓您用來控制及自動化 Azure 服務的部署和管理。</span><span class="sxs-lookup"><span data-stu-id="6d553-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="6d553-105">本文說明如何使用本機 Azure PowerShell 主控台或指令碼，運用[服務匯流排 Resource Manager PowerShell 模組](/powershell/module/azurerm.servicebus)來佈建及管理服務匯流排實體 (命名空間、佇列、主題和訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="6d553-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="6d553-106">您也可以使用 Azure Resource Manager 範本來管理服務匯流排實體。</span><span class="sxs-lookup"><span data-stu-id="6d553-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="6d553-107">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)文章。</span><span class="sxs-lookup"><span data-stu-id="6d553-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d553-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d553-108">Prerequisites</span></span>

<span data-ttu-id="6d553-109">在開始之前，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6d553-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="6d553-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d553-110">An Azure subscription.</span></span> <span data-ttu-id="6d553-111">如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。</span><span class="sxs-lookup"><span data-stu-id="6d553-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="6d553-112">具備 Azure PowerShell 的電腦。</span><span class="sxs-lookup"><span data-stu-id="6d553-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="6d553-113">如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="6d553-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="6d553-114">大致了解 PowerShell 指令碼、NuGet 封裝和 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="6d553-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="6d553-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="6d553-115">Get started</span></span>

<span data-ttu-id="6d553-116">第一個步驟是使用 PowerShell 來登入 Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d553-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="6d553-117">遵循[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps) 中的指示登入您的 Azure 帳戶，並擷取及存取 Azure 訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="6d553-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="6d553-118">佈建服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="6d553-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="6d553-119">使用服務匯流排命名空間時，您可以使用 [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace)、[New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace)、[Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) 和 [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d553-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="6d553-120">這個範例會在指令碼中建立幾個區域變數：`$Namespace` 和 `$Location`。</span><span class="sxs-lookup"><span data-stu-id="6d553-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="6d553-121">`$Namespace` 為我們想要使用之服務匯流排命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d553-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="6d553-122">`$Location` 會識別我們將在其中佈建命名空間的資料中心。</span><span class="sxs-lookup"><span data-stu-id="6d553-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="6d553-123">`$CurrentNamespace` 會儲存我們擷取 (或建立) 的參考命名空間。</span><span class="sxs-lookup"><span data-stu-id="6d553-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="6d553-124">在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="6d553-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="6d553-125">這部分的指令碼會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="6d553-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="6d553-126">嘗試擷取具有指定名稱的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="6d553-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="6d553-127">如果找到命名空間，它會回報找到的項目。</span><span class="sxs-lookup"><span data-stu-id="6d553-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="6d553-128">如果找不到命名空間，它會建立命名空間，然後擷取新建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="6d553-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="6d553-129">建立命名空間授權規則</span><span class="sxs-lookup"><span data-stu-id="6d553-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="6d553-130">下列範例示範如何使用 [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule)、[Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule)、[Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) 和 [Remove-AzureRmServiceBusNamespaceAuthorizationRule Cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule) 來管理命名空間授權規則。</span><span class="sxs-lookup"><span data-stu-id="6d553-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="6d553-131">建立佇列</span><span class="sxs-lookup"><span data-stu-id="6d553-131">Create a queue</span></span>

<span data-ttu-id="6d553-132">若要建立佇列或主題，請使用上一節的指令碼來執行命名空間檢查。</span><span class="sxs-lookup"><span data-stu-id="6d553-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="6d553-133">然後，建立佇列：</span><span class="sxs-lookup"><span data-stu-id="6d553-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="6d553-134">修改佇列屬性</span><span class="sxs-lookup"><span data-stu-id="6d553-134">Modify queue properties</span></span>

<span data-ttu-id="6d553-135">在執行上一節的指令碼後，您可以使用 [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) Cmdlet 來更新佇列的屬性，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="6d553-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="6d553-136">佈建其他服務匯流排實體</span><span class="sxs-lookup"><span data-stu-id="6d553-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="6d553-137">您可以使用[服務匯流排 PowerShell 模組](/powershell/module/azurerm.servicebus)來佈建其他實體，例如主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d553-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="6d553-138">這些 Cmdlet 在語法上類似於上一節中所示範的佇列建立 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d553-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d553-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d553-139">Next steps</span></span>

- <span data-ttu-id="6d553-140">請在[這裡](/powershell/module/azurerm.servicebus)參閱完整的服務匯流排 Resource Manager PowerShell 模組文件。</span><span class="sxs-lookup"><span data-stu-id="6d553-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="6d553-141">此頁面會列出所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d553-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="6d553-142">如需使用 Azure Resource Manager 範本的相關資訊，請參閱[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)文章。</span><span class="sxs-lookup"><span data-stu-id="6d553-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="6d553-143">[服務匯流排 .NET 管理程式庫](service-bus-management-libraries.md)的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d553-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="6d553-144">管理服務匯流排實體有一些替代方式，如這些部落格文章中所述︰</span><span class="sxs-lookup"><span data-stu-id="6d553-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="6d553-145">如何使用 PowerShell 指令碼來建立服務匯流排佇列、主題及訂閱</span><span class="sxs-lookup"><span data-stu-id="6d553-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="6d553-146">如何使用 PowerShell 指令碼來建立服務匯流排命名空間與事件中樞</span><span class="sxs-lookup"><span data-stu-id="6d553-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="6d553-147">服務匯流排 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="6d553-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
