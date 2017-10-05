---
title: "了解 BizTalk 服務中的節流 | Microsoft Docs"
description: "了解 BizTalk 服務的節流閾值和產生的執行階段行為。 節流是以記憶體使用量和訊息數為依據。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="70697-105">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="70697-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="70697-106">Azure BizTalk 服務根據兩個條件實作服務節流：記憶體使用量和同時訊息處理的數量。</span><span class="sxs-lookup"><span data-stu-id="70697-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="70697-107">本主題列出節流閾值，並說明發生節流狀況時的執行階段行為。</span><span class="sxs-lookup"><span data-stu-id="70697-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="70697-108">節流閾值</span><span class="sxs-lookup"><span data-stu-id="70697-108">Throttling Thresholds</span></span>
<span data-ttu-id="70697-109">下表列出節流來源和閾值：</span><span class="sxs-lookup"><span data-stu-id="70697-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="70697-110">說明</span><span class="sxs-lookup"><span data-stu-id="70697-110">Description</span></span> | <span data-ttu-id="70697-111">低閾值</span><span class="sxs-lookup"><span data-stu-id="70697-111">Low Threshold</span></span> | <span data-ttu-id="70697-112">高閾值</span><span class="sxs-lookup"><span data-stu-id="70697-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="70697-113">記憶體</span><span class="sxs-lookup"><span data-stu-id="70697-113">Memory</span></span> |<span data-ttu-id="70697-114">可用系統記憶體總計的 %/PageFileBytes。</span><span class="sxs-lookup"><span data-stu-id="70697-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="70697-115">可用的 PageFileBytes 總計大約是系統 RAM 的 2 倍。</span><span class="sxs-lookup"><span data-stu-id="70697-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="70697-116">60%</span><span class="sxs-lookup"><span data-stu-id="70697-116">60%</span></span> |<span data-ttu-id="70697-117">70%</span><span class="sxs-lookup"><span data-stu-id="70697-117">70%</span></span> |
| <span data-ttu-id="70697-118">訊息處理</span><span class="sxs-lookup"><span data-stu-id="70697-118">Message Processing</span></span> |<span data-ttu-id="70697-119">同時處理的訊息數目</span><span class="sxs-lookup"><span data-stu-id="70697-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="70697-120">40 * 核心數目</span><span class="sxs-lookup"><span data-stu-id="70697-120">40 * number of cores</span></span> |<span data-ttu-id="70697-121">100 * 核心數目</span><span class="sxs-lookup"><span data-stu-id="70697-121">100 * number of cores</span></span> |

<span data-ttu-id="70697-122">達到高閾值時，Azure BizTalk 服務就會開始節流。</span><span class="sxs-lookup"><span data-stu-id="70697-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="70697-123">達到低閾值時會停止節流。</span><span class="sxs-lookup"><span data-stu-id="70697-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="70697-124">例如，服務使用 65% 系統記憶體。</span><span class="sxs-lookup"><span data-stu-id="70697-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="70697-125">在此情況下，服務不會節流。</span><span class="sxs-lookup"><span data-stu-id="70697-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="70697-126">服務開始使用 70% 系統記憶體。</span><span class="sxs-lookup"><span data-stu-id="70697-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="70697-127">在此情況下，服務會節流，並持續節流直到服務使用 60% (低閾值) 系統記憶體為止。</span><span class="sxs-lookup"><span data-stu-id="70697-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="70697-128">Azure BizTalk 服務會追蹤節流狀態 (正常狀態與節流狀態) 和節流持續時間。</span><span class="sxs-lookup"><span data-stu-id="70697-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="70697-129">執行階段行為</span><span class="sxs-lookup"><span data-stu-id="70697-129">Runtime Behavior</span></span>
<span data-ttu-id="70697-130">Azure BizTalk 服務進入節流狀態時會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="70697-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="70697-131">依每一角色執行個體來節流。</span><span class="sxs-lookup"><span data-stu-id="70697-131">Throttling is per role instance.</span></span> <span data-ttu-id="70697-132">例如：</span><span class="sxs-lookup"><span data-stu-id="70697-132">For example:</span></span><br/>
  <span data-ttu-id="70697-133">RoleInstanceA 節流。</span><span class="sxs-lookup"><span data-stu-id="70697-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="70697-134">RoleInstanceB 未節流。</span><span class="sxs-lookup"><span data-stu-id="70697-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="70697-135">在此情況下，RoleInstanceB 中的訊息如預期般地處理。</span><span class="sxs-lookup"><span data-stu-id="70697-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="70697-136">RoleInstanceA 中的訊息會捨棄且失敗，並傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="70697-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="70697-137">
  **伺服器忙碌中。請再試一次。**</span><span class="sxs-lookup"><span data-stu-id="70697-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="70697-138">所有提取來源不會輪詢或下載訊息。</span><span class="sxs-lookup"><span data-stu-id="70697-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="70697-139">例如：</span><span class="sxs-lookup"><span data-stu-id="70697-139">For example:</span></span><br/>
  <span data-ttu-id="70697-140">管線會從外部 FTP 來源提取訊息。</span><span class="sxs-lookup"><span data-stu-id="70697-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="70697-141">進行提取的角色執行個體會進入節流狀態。</span><span class="sxs-lookup"><span data-stu-id="70697-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="70697-142">在此情況下，在角色執行個體停止節流之前，管線會停止下載其他訊息。</span><span class="sxs-lookup"><span data-stu-id="70697-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="70697-143">回應會傳送給用戶端，讓用戶端可以重新提交訊息。</span><span class="sxs-lookup"><span data-stu-id="70697-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="70697-144">您必須等待節流情況解決為止。</span><span class="sxs-lookup"><span data-stu-id="70697-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="70697-145">尤其，您必須等待到達到低閾值為止。</span><span class="sxs-lookup"><span data-stu-id="70697-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="70697-146">重要事項</span><span class="sxs-lookup"><span data-stu-id="70697-146">Important notes</span></span>
* <span data-ttu-id="70697-147">無法停用節流。</span><span class="sxs-lookup"><span data-stu-id="70697-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="70697-148">無法修改節流閾值。</span><span class="sxs-lookup"><span data-stu-id="70697-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="70697-149">節流的實作以全系統為範圍。</span><span class="sxs-lookup"><span data-stu-id="70697-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="70697-150">Azure SQL Database Server 也有內建的節流。</span><span class="sxs-lookup"><span data-stu-id="70697-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="70697-151">其他 Azure BizTalk 服務主題</span><span class="sxs-lookup"><span data-stu-id="70697-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="70697-152">安裝 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="70697-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="70697-153">教學課程：Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="70697-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="70697-154">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="70697-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="70697-155">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="70697-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="70697-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70697-156">See Also</span></span>
* [<span data-ttu-id="70697-157">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="70697-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="70697-158">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="70697-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="70697-159">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="70697-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="70697-160">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="70697-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="70697-161">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="70697-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="70697-162">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="70697-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

