---
title: "Azure Stack 中的客戶帳務與退款 | Microsoft Docs"
description: "了解如何從 Azure Stack 擷取資源使用量資訊。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: fd2db137948490707a2f4799535062aeef4509e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="dc50a-103">Azure Stack 中的使用量與計費</span><span class="sxs-lookup"><span data-stu-id="dc50a-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="dc50a-104">使用量代表使用者取用的資源數量。</span><span class="sxs-lookup"><span data-stu-id="dc50a-104">Usage represents the quantity of resources consumed by a user.</span></span> <span data-ttu-id="dc50a-105">Azure Stack 會收集每個使用者的使用量資訊，並使用該資訊向使用者收費。</span><span class="sxs-lookup"><span data-stu-id="dc50a-105">Azure Stack collects usage information for each user and uses it to bill them.</span></span> <span data-ttu-id="dc50a-106">此文章說明如何針對資源使用量向 Azure Stack 使用者收費，以及如何存取帳單資訊以進行分析、退款等作業。</span><span class="sxs-lookup"><span data-stu-id="dc50a-106">This article describes how Azure Stack users are billed for resource usage, and how the billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="dc50a-107">Azure Stack 包含針對所有資源收集並彙總使用量資料的基礎架構。</span><span class="sxs-lookup"><span data-stu-id="dc50a-107">Azure Stack contains the infrastructure to collect and aggregate usage data for all resources.</span></span> <span data-ttu-id="dc50a-108">您可以使用帳單配接器存取此資料，並將資料匯出到帳單系統，或將資料匯出到像 Microsoft Power BI 這樣的商務智慧工具。</span><span class="sxs-lookup"><span data-stu-id="dc50a-108">You can access this data and export it to a billing system by using a billing adapter, or export it to a business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="dc50a-109">匯出之後，此帳單資訊就會用於分析，或傳送到退款系統。</span><span class="sxs-lookup"><span data-stu-id="dc50a-109">After exporting, this billing information is used for analytics or transferred to a chargeback system.</span></span>

![將 Azure Stack 連接至帳單應用程式之帳單配接器的概念模型](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="dc50a-111">我可以找到哪些使用量資訊，以及如何尋找？</span><span class="sxs-lookup"><span data-stu-id="dc50a-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="dc50a-112">Azure Stack 資源提供者 (例如計算、儲存體及網路) 會以每小時為間隔，針對每個訂用帳戶產生使用量資料。</span><span class="sxs-lookup"><span data-stu-id="dc50a-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="dc50a-113">使用量資料包含和所使用資源有關的資訊，例如資源名稱、計量名稱、計量識別碼、已使用數量等等。若要深入了解計量識別碼資源，請參閱[使用情況 API 常見問題集](azure-stack-usage-related-faq.md)文章。</span><span class="sxs-lookup"><span data-stu-id="dc50a-113">The usage data contains information about the resource used such as resource name, meter name, meter ID, quantity used etc. To learn about the meters ID resources, refer to the [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="dc50a-114">收集到使用量資料之後，就會將資料[回報給 Azure](azure-stack-usage-reporting.md)，以產生可透過 Azure 計費入口網站檢視的帳單。</span><span class="sxs-lookup"><span data-stu-id="dc50a-114">After the usage data has been collected, it is [reported to Azure](azure-stack-usage-reporting.md) to generate a bill, which can be viewed through the Azure billing portal.</span></span> <span data-ttu-id="dc50a-115">Azure 計費入口網站只會顯示可收費資源的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="dc50a-115">The Azure billing portal shows the usage data only for the chargeable resources.</span></span> <span data-ttu-id="dc50a-116">除了可收費資源之外，Azure Stack 可擷取更廣泛資源的使用量資料，您可以透過 REST API 或 PowerShell，在 Azure Stack 環境中存取那些資料。</span><span class="sxs-lookup"><span data-stu-id="dc50a-116">In addition to the chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="dc50a-117">Azure Stack 雲端系統管理員可以擷取所有使用者訂用帳戶的使用量資料，而使用者則只能取得他們自己的使用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dc50a-117">Azure Stack cloud administrators can retrieve the usage data for all user subscriptions whereas a user can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="dc50a-118">擷取使用量資訊</span><span class="sxs-lookup"><span data-stu-id="dc50a-118">Retrieve usage information</span></span>

<span data-ttu-id="dc50a-119">若要產生使用量資料，您應該有正在執行並使用系統的資源。</span><span class="sxs-lookup"><span data-stu-id="dc50a-119">To generate the usage data, you should have resources that are running and actively using the system.</span></span> <span data-ttu-id="dc50a-120">如果不確定您是否有任何資源正在 Azure Stack Marketplace 中執行，請部署虛擬機器 (VM)，並檢查 VM 監控刀鋒視窗以確定它正在執行。</span><span class="sxs-lookup"><span data-stu-id="dc50a-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify the VM monitoring blade to make sure it’s running.</span></span> <span data-ttu-id="dc50a-121">請使用下列 PowerShell Cmdlet 檢視使用量資料：</span><span class="sxs-lookup"><span data-stu-id="dc50a-121">Use the following PowerShell cmdlets to view the usage data:</span></span>

1. [<span data-ttu-id="dc50a-122">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc50a-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. * <span data-ttu-id="dc50a-123">[設定 Azure Stack 使用者](azure-stack-powershell-configure-user.md)或 [Azure Stack 操作員](azure-stack-powershell-configure-admin.md) 的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="dc50a-123">[Configure the Azure Stack user's](azure-stack-powershell-configure-user.md) or the [Azure Stack operator's](azure-stack-powershell-configure-admin.md) PowerShell environment</span></span> 
3. <span data-ttu-id="dc50a-124">若要擷取使用量資料，請使用 [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dc50a-124">To retrieve the usage data, use the [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="dc50a-125">如果有使用量資料，就會傳回資料，如以下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="dc50a-125">If usage data is available, it’s returned in as shown in the following screenshot:</span></span> 
   
   ![使用量彙總](media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="dc50a-127">PowerShell 針對每個呼叫傳回 1,000 行使用量。</span><span class="sxs-lookup"><span data-stu-id="dc50a-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="dc50a-128">您可以使用連續參數擷取超過 1,000 行</span><span class="sxs-lookup"><span data-stu-id="dc50a-128">You can use the continuation parameter to retrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc50a-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc50a-129">Next steps</span></span>

[<span data-ttu-id="dc50a-130">向 Azure 回報 Azure Stack 使用量資料</span><span class="sxs-lookup"><span data-stu-id="dc50a-130">Report Azure Stack usage data to Azure</span></span>](azure-stack-usage-reporting.md)

[<span data-ttu-id="dc50a-131">提供者資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="dc50a-131">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="dc50a-132">租用戶資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="dc50a-132">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="dc50a-133">使用量相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="dc50a-133">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

