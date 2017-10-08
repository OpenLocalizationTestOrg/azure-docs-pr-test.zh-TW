---
title: "aaaCustomer 計費和計費中 Azure 堆疊 |Microsoft 文件"
description: "深入了解如何從 Azure 堆疊 tooretrieve 資源使用量資訊。"
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
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="50f41-103">Azure Stack 中的使用量與計費</span><span class="sxs-lookup"><span data-stu-id="50f41-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="50f41-104">使用方式代表 hello 由使用者所使用的資源數量。</span><span class="sxs-lookup"><span data-stu-id="50f41-104">Usage represents hello quantity of resources consumed by a user.</span></span> <span data-ttu-id="50f41-105">Azure 堆疊會收集使用資訊的每個使用者，並使用它 toobill 它們。</span><span class="sxs-lookup"><span data-stu-id="50f41-105">Azure Stack collects usage information for each user and uses it toobill them.</span></span> <span data-ttu-id="50f41-106">本文說明如何將 Azure 堆疊使用者計費資源使用量和分析、 計費等 hello 帳單資訊的存取方式。</span><span class="sxs-lookup"><span data-stu-id="50f41-106">This article describes how Azure Stack users are billed for resource usage, and how hello billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="50f41-107">Azure 堆疊會包含 hello 基礎結構 toocollect 和彙總使用量資料的所有資源。</span><span class="sxs-lookup"><span data-stu-id="50f41-107">Azure Stack contains hello infrastructure toocollect and aggregate usage data for all resources.</span></span> <span data-ttu-id="50f41-108">您可以存取此資料並將它匯出 tooa 帳務系統使用帳務配接器，或將它匯出 tooa 商務智慧工具，例如 Microsoft Power BI。</span><span class="sxs-lookup"><span data-stu-id="50f41-108">You can access this data and export it tooa billing system by using a billing adapter, or export it tooa business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="50f41-109">匯出之後，此計費的資訊會用於分析，或傳送 tooa 計費系統。</span><span class="sxs-lookup"><span data-stu-id="50f41-109">After exporting, this billing information is used for analytics or transferred tooa chargeback system.</span></span>

![連接 Azure 堆疊 tooa 帳務配接器的概念模型計費應用程式](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="50f41-111">我可以找到哪些使用量資訊，以及如何尋找？</span><span class="sxs-lookup"><span data-stu-id="50f41-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="50f41-112">Azure Stack 資源提供者 (例如計算、儲存體及網路) 會以每小時為間隔，針對每個訂用帳戶產生使用量資料。</span><span class="sxs-lookup"><span data-stu-id="50f41-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="50f41-113">hello 使用量資料包含 hello 資源，例如資源名稱的相關資訊、 使用計量名稱、 計量器識別碼的數量等 toolearn 有關 hello 公尺識別碼資源，請參閱 toohello[使用量 API 常見問題集](azure-stack-usage-related-faq.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="50f41-113">hello usage data contains information about hello resource used such as resource name, meter name, meter ID, quantity used etc. toolearn about hello meters ID resources, refer toohello [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="50f41-114">在收集 hello 使用量資料之後，它是[回報 tooAzure](azure-stack-usage-reporting.md) toogenerate 可以透過 hello Azure 計費入口網站檢視帳單。</span><span class="sxs-lookup"><span data-stu-id="50f41-114">After hello usage data has been collected, it is [reported tooAzure](azure-stack-usage-reporting.md) toogenerate a bill, which can be viewed through hello Azure billing portal.</span></span> <span data-ttu-id="50f41-115">hello Azure 計費入口網站顯示 hello 使用量資料只 hello 收費的資源。</span><span class="sxs-lookup"><span data-stu-id="50f41-115">hello Azure billing portal shows hello usage data only for hello chargeable resources.</span></span> <span data-ttu-id="50f41-116">此外 toohello 收費的資源，Azure 堆疊擷取廣泛的資源，您可以存取您透過 REST Api 或 PowerShell 的 Azure 堆疊環境中的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="50f41-116">In addition toohello chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="50f41-117">Azure 堆疊雲端系統管理員可以擷取所有使用者訂用帳戶的 hello 使用量資料，而使用者也可以取得只有其使用方式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="50f41-117">Azure Stack cloud administrators can retrieve hello usage data for all user subscriptions whereas a user can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="50f41-118">擷取使用量資訊</span><span class="sxs-lookup"><span data-stu-id="50f41-118">Retrieve usage information</span></span>

<span data-ttu-id="50f41-119">toogenerate hello 使用量資料，您應該確認執行，且目前正在使用 hello 系統資源。</span><span class="sxs-lookup"><span data-stu-id="50f41-119">toogenerate hello usage data, you should have resources that are running and actively using hello system.</span></span> <span data-ttu-id="50f41-120">如果您不確定是否有 Marketplace</堆疊中執行的任何資源，部署虛擬機器 (VM)，並確認 hello VM 監視刀鋒視窗 toomake 確定它正在執行。</span><span class="sxs-lookup"><span data-stu-id="50f41-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify hello VM monitoring blade toomake sure it’s running.</span></span> <span data-ttu-id="50f41-121">使用下列 PowerShell cmdlet tooview hello 使用量資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="50f41-121">Use hello following PowerShell cmdlets tooview hello usage data:</span></span>

1. [<span data-ttu-id="50f41-122">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="50f41-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. * <span data-ttu-id="50f41-123">[設定 hello Azure 堆疊使用者的](azure-stack-powershell-configure-user.md)或 hello [Azure 堆疊運算子](azure-stack-powershell-configure-admin.md)PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="50f41-123">[Configure hello Azure Stack user's](azure-stack-powershell-configure-user.md) or hello [Azure Stack operator's](azure-stack-powershell-configure-admin.md) PowerShell environment</span></span> 
3. <span data-ttu-id="50f41-124">tooretrieve hello 使用量資料，請使用 hello [Get UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50f41-124">tooretrieve hello usage data, use hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="50f41-125">如果使用方式資料功能，它會傳回在 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="50f41-125">If usage data is available, it’s returned in as shown in hello following screenshot:</span></span> 
   
   ![使用量彙總](media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="50f41-127">PowerShell 針對每個呼叫傳回 1,000 行使用量。</span><span class="sxs-lookup"><span data-stu-id="50f41-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="50f41-128">您可以使用 hello 接續參數 tooretrieve 超過 1,000 個線條</span><span class="sxs-lookup"><span data-stu-id="50f41-128">You can use hello continuation parameter tooretrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="50f41-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50f41-129">Next steps</span></span>

[<span data-ttu-id="50f41-130">報告 Azure 堆疊使用方式資料 tooAzure</span><span class="sxs-lookup"><span data-stu-id="50f41-130">Report Azure Stack usage data tooAzure</span></span>](azure-stack-usage-reporting.md)

[<span data-ttu-id="50f41-131">提供者資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="50f41-131">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="50f41-132">租用戶資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="50f41-132">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="50f41-133">使用量相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="50f41-133">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

