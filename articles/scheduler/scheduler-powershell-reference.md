---
title: "排程器 PowerShell Cmdlet 參考"
description: "排程器 PowerShell Cmdlet 參考"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 141919ab4506b3de4c4a69670dcf54c60ee6409c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="4fd38-103">排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="4fd38-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="4fd38-104">下表說明並連結至 Azure 排程器中每個主要 Cmdlet 的參考頁面。</span><span class="sxs-lookup"><span data-stu-id="4fd38-104">The following table describes and links to the reference page of each of the major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="4fd38-105">若要安裝 Azure PowerShell，並將它與 Azure 訂用帳戶建立關聯，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4fd38-105">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="4fd38-106">如需 [Azure Resource Manager Cmdlet](/powershell/azure/overview) 的詳細資訊，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="4fd38-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="4fd38-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="4fd38-107">Cmdlet</span></span> | <span data-ttu-id="4fd38-108">Cmdlet 說明</span><span class="sxs-lookup"><span data-stu-id="4fd38-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="4fd38-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-110">停用工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="4fd38-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-112">啟用工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="4fd38-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="4fd38-114">取得排程器作業。</span><span class="sxs-lookup"><span data-stu-id="4fd38-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="4fd38-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-116">取得工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-116">Gets job collections.</span></span> |
| [<span data-ttu-id="4fd38-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="4fd38-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="4fd38-118">取得工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="4fd38-118">Gets job history.</span></span> |
| [<span data-ttu-id="4fd38-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="4fd38-120">建立 HTTP 工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="4fd38-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-122">建立工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="4fd38-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="4fd38-124">建立服務匯流排佇列工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="4fd38-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="4fd38-126">建立服務匯流排主題工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="4fd38-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="4fd38-128">建立儲存體佇列工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="4fd38-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="4fd38-130">移除排程器工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="4fd38-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-132">移除工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="4fd38-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="4fd38-134">修改排程器 HTTP 工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="4fd38-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="4fd38-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="4fd38-136">修改工作集合。</span><span class="sxs-lookup"><span data-stu-id="4fd38-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="4fd38-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="4fd38-138">修改服務匯流排佇列工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="4fd38-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="4fd38-140">修改服務匯流排主題工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="4fd38-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="4fd38-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="4fd38-142">修改儲存體佇列工作。</span><span class="sxs-lookup"><span data-stu-id="4fd38-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="4fd38-143">如需更多詳細資訊，您可以執行下列任何 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="4fd38-143">For more detailed information, you can run any of the following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="4fd38-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4fd38-144">See Also</span></span>
 [<span data-ttu-id="4fd38-145">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="4fd38-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="4fd38-146">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="4fd38-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="4fd38-147">在 Azure 入口網站中開始使用排程器</span><span class="sxs-lookup"><span data-stu-id="4fd38-147">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="4fd38-148">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="4fd38-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="4fd38-149">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="4fd38-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="4fd38-150">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="4fd38-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="4fd38-151">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="4fd38-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="4fd38-152">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="4fd38-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

