---
title: "關於 BizTalk 服務的節流 aaaLearn |Microsoft 文件"
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="9b050-105">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="9b050-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="9b050-106">Azure BizTalk 服務會實作兩個條件為基礎的服務節流： 記憶體使用量和 hello 同時處理的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="9b050-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="9b050-107">本主題列出 hello 節流臨界值，並說明 hello 執行階段行為，當發生節流狀況。</span><span class="sxs-lookup"><span data-stu-id="9b050-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="9b050-108">節流閾值</span><span class="sxs-lookup"><span data-stu-id="9b050-108">Throttling Thresholds</span></span>
<span data-ttu-id="9b050-109">下表將列出 hello hello 節流的來源和臨界值：</span><span class="sxs-lookup"><span data-stu-id="9b050-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="9b050-110">說明</span><span class="sxs-lookup"><span data-stu-id="9b050-110">Description</span></span> | <span data-ttu-id="9b050-111">低閾值</span><span class="sxs-lookup"><span data-stu-id="9b050-111">Low Threshold</span></span> | <span data-ttu-id="9b050-112">高閾值</span><span class="sxs-lookup"><span data-stu-id="9b050-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9b050-113">記憶體</span><span class="sxs-lookup"><span data-stu-id="9b050-113">Memory</span></span> |<span data-ttu-id="9b050-114">可用系統記憶體總計的 %/PageFileBytes。</span><span class="sxs-lookup"><span data-stu-id="9b050-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="9b050-115">總計的可用 PageFileBytes 大約是 hello 系統的 2 倍 hello RAM。</span><span class="sxs-lookup"><span data-stu-id="9b050-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="9b050-116">60%</span><span class="sxs-lookup"><span data-stu-id="9b050-116">60%</span></span> |<span data-ttu-id="9b050-117">70%</span><span class="sxs-lookup"><span data-stu-id="9b050-117">70%</span></span> |
| <span data-ttu-id="9b050-118">訊息處理</span><span class="sxs-lookup"><span data-stu-id="9b050-118">Message Processing</span></span> |<span data-ttu-id="9b050-119">同時處理的訊息數目</span><span class="sxs-lookup"><span data-stu-id="9b050-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="9b050-120">40 * 核心數目</span><span class="sxs-lookup"><span data-stu-id="9b050-120">40 * number of cores</span></span> |<span data-ttu-id="9b050-121">100 * 核心數目</span><span class="sxs-lookup"><span data-stu-id="9b050-121">100 * number of cores</span></span> |

<span data-ttu-id="9b050-122">當達到高的閾值時，Azure BizTalk 服務會啟動 toothrottle。</span><span class="sxs-lookup"><span data-stu-id="9b050-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="9b050-123">當達到 hello 低的閾值時，節流設定停駐點。</span><span class="sxs-lookup"><span data-stu-id="9b050-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="9b050-124">例如，服務使用 65% 系統記憶體。</span><span class="sxs-lookup"><span data-stu-id="9b050-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="9b050-125">在此情況下，不會不會節流 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="9b050-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="9b050-126">服務開始使用 70% 系統記憶體。</span><span class="sxs-lookup"><span data-stu-id="9b050-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="9b050-127">在此情況下，hello 服務節流處理，並繼續 toothrottle 直到 hello 服務會使用 60%（下限臨界值） 的系統記憶體。</span><span class="sxs-lookup"><span data-stu-id="9b050-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="9b050-128">Azure BizTalk 服務會追蹤節流狀態 （一般狀態與節流狀態） 的 hello 與 hello 節流期間。</span><span class="sxs-lookup"><span data-stu-id="9b050-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="9b050-129">執行階段行為</span><span class="sxs-lookup"><span data-stu-id="9b050-129">Runtime Behavior</span></span>
<span data-ttu-id="9b050-130">Azure BizTalk 服務便會進入節流狀態，當 hello 會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="9b050-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="9b050-131">依每一角色執行個體來節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-131">Throttling is per role instance.</span></span> <span data-ttu-id="9b050-132">例如：</span><span class="sxs-lookup"><span data-stu-id="9b050-132">For example:</span></span><br/>
  <span data-ttu-id="9b050-133">RoleInstanceA 節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="9b050-134">RoleInstanceB 未節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="9b050-135">在此情況下，RoleInstanceB 中的訊息如預期般地處理。</span><span class="sxs-lookup"><span data-stu-id="9b050-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="9b050-136">RoleInstanceA 中的訊息都會被捨棄，並會因下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="9b050-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="9b050-137">
  **伺服器忙碌中。請再試一次。**</span><span class="sxs-lookup"><span data-stu-id="9b050-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="9b050-138">所有提取來源不會輪詢或下載訊息。</span><span class="sxs-lookup"><span data-stu-id="9b050-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="9b050-139">例如：</span><span class="sxs-lookup"><span data-stu-id="9b050-139">For example:</span></span><br/>
  <span data-ttu-id="9b050-140">管線會從外部 FTP 來源提取訊息。</span><span class="sxs-lookup"><span data-stu-id="9b050-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="9b050-141">執行 hello 提取 hello 角色執行個體取得節流狀態。</span><span class="sxs-lookup"><span data-stu-id="9b050-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="9b050-142">在此情況下，hello 管線就會停止下載額外的訊息，直到 hello 角色執行個體停止節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="9b050-143">回應會傳送 toohello 用戶端，因此 hello 用戶端可以再重新送出 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="9b050-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="9b050-144">您必須等到 hello 節流設定所解析。</span><span class="sxs-lookup"><span data-stu-id="9b050-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="9b050-145">具體來說，您必須等到達到 hello 低臨界值。</span><span class="sxs-lookup"><span data-stu-id="9b050-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="9b050-146">重要事項</span><span class="sxs-lookup"><span data-stu-id="9b050-146">Important notes</span></span>
* <span data-ttu-id="9b050-147">無法停用節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="9b050-148">無法修改節流閾值。</span><span class="sxs-lookup"><span data-stu-id="9b050-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="9b050-149">節流的實作以全系統為範圍。</span><span class="sxs-lookup"><span data-stu-id="9b050-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="9b050-150">hello Azure SQL Database 伺服器也有內建的節流。</span><span class="sxs-lookup"><span data-stu-id="9b050-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="9b050-151">其他 Azure BizTalk 服務主題</span><span class="sxs-lookup"><span data-stu-id="9b050-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="9b050-152">安裝 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="9b050-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="9b050-153">教學課程：Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="9b050-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="9b050-154">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="9b050-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="9b050-155">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="9b050-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="9b050-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9b050-156">See Also</span></span>
* [<span data-ttu-id="9b050-157">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="9b050-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="9b050-158">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="9b050-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="9b050-159">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="9b050-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="9b050-160">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="9b050-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="9b050-161">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="9b050-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="9b050-162">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="9b050-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

