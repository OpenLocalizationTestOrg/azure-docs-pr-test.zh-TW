---
title: "使用作業記錄檔對 BizTalk 服務進行疑難排解 | Microsoft Docs"
description: "使用作業記錄疑難排解 BizTalk 服務。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c0c83361f94ffd9c30d7fcc551ff4b85ad7d6fa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a><span data-ttu-id="e3326-104">BizTalk 服務：使用作業記錄檔進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e3326-104">BizTalk Services: Troubleshoot using operation logs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-the-operation-logs"></a><span data-ttu-id="e3326-105">什麼是作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="e3326-105">What are the Operation Logs</span></span>
<span data-ttu-id="e3326-106">「作業記錄檔」是 Azure 傳統入口網站提供的一個管理服務功能，可讓您檢視在 Azure 服務上執行的作業 (包括 BizTalk 服務) 的歷程記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e3326-106">Operation Logs is a Management Services feature available in the Azure classic portal that allows you to view historical logs of operations performed on your Azure services, including BizTalk Services.</span></span> <span data-ttu-id="e3326-107">它可讓您檢視與 BizTalk 訂用帳戶的管理作業相關歷程資料，最遠可回溯 180 天。</span><span class="sxs-lookup"><span data-stu-id="e3326-107">This enables you to view historical data related to management operations on your BizTalk Service subscription as far back as 180 days.</span></span>

> [!NOTE]
> <span data-ttu-id="e3326-108">這項功能只會在 BizTalk 服務啟動、備份等期間，針對服務的管理作業擷取記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e3326-108">This feature only captures logs for management operations on BizTalk Services, such as when the service was started, backed up, and so on.</span></span> <span data-ttu-id="e3326-109">這類作業無論是從 Azure 傳統入口網站還是透過 [BizTalk 服務 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx) 來執行，都會受到追蹤。</span><span class="sxs-lookup"><span data-stu-id="e3326-109">Such operations are tracked irrespective of whether they are performed from the Azure classic portal or by using the [BizTalk Service REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span> <span data-ttu-id="e3326-110">如需使用管理服務進行追蹤的作業完整清單，請參閱[使用 Azure 管理服務進行追蹤的作業](#bizops)。</span><span class="sxs-lookup"><span data-stu-id="e3326-110">For a complete list of operations that are tracked using Management Services, see [Operations Tracked Using Azure Management Services](#bizops).</span></span><br/><br/>
> <span data-ttu-id="e3326-111">此功能不會對 BizTalk 服務執行階段的相關活動 (例如橋接器等項目所處理的訊息) 擷取記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e3326-111">This does not capture the logs for activities related to BizTalk Service runtime (such as message processed by bridges, and so on.).</span></span> <span data-ttu-id="e3326-112">若要檢視這些記錄檔，請使用 BizTalk 服務入口網站中的 [追蹤] 檢視。</span><span class="sxs-lookup"><span data-stu-id="e3326-112">To view these logs, use the Tracking view from the BizTalk Services portal.</span></span> <span data-ttu-id="e3326-113">如需詳細資訊，請參閱[追蹤訊息](http://msdn.microsoft.com/library/azure/hh949805.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e3326-113">For more information, see [Tracking Messages](http://msdn.microsoft.com/library/azure/hh949805.aspx).</span></span>
> 
> 

## <a name="view-biztalk-services-operation-logs"></a><span data-ttu-id="e3326-114">檢視 BizTalk 服務作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="e3326-114">View BizTalk Services Operation Logs</span></span>
1. <span data-ttu-id="e3326-115">在 Azure 傳統入口網站中，選取 [管理服務]，然後選取 [作業記錄檔] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e3326-115">In the Azure classic portal, select **Management Services**, and then select the **Operation Logs** tab.</span></span>
2. <span data-ttu-id="e3326-116">您可以根據不同的參數篩選記錄檔，例如訂用帳戶、日期範圍、服務類型 (例如 BizTalk 服務)、服務名稱或作業狀態 (例如「成功」、「失敗」)。</span><span class="sxs-lookup"><span data-stu-id="e3326-116">You can filter the logs based on different parameters like subscription, date range, service type (e.g. BizTalk Services), service name, or status of the operation (Succeeded, Failed).</span></span>
3. <span data-ttu-id="e3326-117">選取核取記號以檢視篩選清單。</span><span class="sxs-lookup"><span data-stu-id="e3326-117">Select the checkmark to view the filtered list.</span></span> <span data-ttu-id="e3326-118">下圖顯示 testbiztalkservice 的相關活動：![檢視作業記錄檔][ViewLogs]</span><span class="sxs-lookup"><span data-stu-id="e3326-118">The following image shows activities related to testbiztalkservice: ![View operation logs][ViewLogs]</span></span> 
4. <span data-ttu-id="e3326-119">若要檢視特定作業的詳細資訊，請選取資料列，然後按一下底部工作列中的 [ **詳細資料** ]。</span><span class="sxs-lookup"><span data-stu-id="e3326-119">To view more about a specific operation, select the row, and click **Details** in the task bar at the bottom.</span></span>

## <span data-ttu-id="e3326-120"><a name="bizops"></a>使用 Azure 管理服務進行追蹤的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-120"><a name="bizops"></a>Operations Tracked Using Azure Management Services</span></span>
<span data-ttu-id="e3326-121">下表列出可使用 Azure 管理服務進行追蹤的作業：</span><span class="sxs-lookup"><span data-stu-id="e3326-121">The following table lists the operations that are tracked using the Azure Management Services:</span></span>

| <span data-ttu-id="e3326-122">作業名稱</span><span class="sxs-lookup"><span data-stu-id="e3326-122">Operation Name</span></span> | <span data-ttu-id="e3326-123">工作</span><span class="sxs-lookup"><span data-stu-id="e3326-123">Task</span></span> |
| --- | --- |
| <span data-ttu-id="e3326-124">CreateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-124">CreateBizTalkService</span></span> |<span data-ttu-id="e3326-125">建立新 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-125">Operation to create a new BizTalk Service</span></span> |
| <span data-ttu-id="e3326-126">DeleteBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-126">DeleteBizTalkService</span></span> |<span data-ttu-id="e3326-127">刪除 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-127">Operation to delete a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-128">RestartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-128">RestartBizTalkService</span></span> |<span data-ttu-id="e3326-129">重新啟動 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-129">Operation to restart a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-130">StartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-130">StartBizTalkService</span></span> |<span data-ttu-id="e3326-131">啟動 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-131">Operation to start a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-132">StopBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-132">StopBizTalkService</span></span> |<span data-ttu-id="e3326-133">停止 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-133">Operation to stop a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-134">DisableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-134">DisableBizTalkService</span></span> |<span data-ttu-id="e3326-135">停用 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-135">Operation to disable a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-136">EnableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-136">EnableBizTalkService</span></span> |<span data-ttu-id="e3326-137">啟用 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-137">Operation to enable a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-138">BackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-138">BackupBizTalkService</span></span> |<span data-ttu-id="e3326-139">備份 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-139">Operation to back up a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-140">RestoreBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-140">RestoreBizTalkService</span></span> |<span data-ttu-id="e3326-141">從指定的備份還原 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-141">Operation to restore a BizTalk Service from specified backup</span></span> |
| <span data-ttu-id="e3326-142">SuspendBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-142">SuspendBizTalkService</span></span> |<span data-ttu-id="e3326-143">暫停 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-143">Operation to suspend a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-144">ResumeBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-144">ResumeBizTalkService</span></span> |<span data-ttu-id="e3326-145">繼續 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-145">Operation to resume a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-146">ScaleBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-146">ScaleBizTalkService</span></span> |<span data-ttu-id="e3326-147">擴大或縮小 BizTalk 服務的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-147">Operation to scale a BizTalk Service up or down</span></span> |
| <span data-ttu-id="e3326-148">ConfigUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-148">ConfigUpdateBizTalkService</span></span> |<span data-ttu-id="e3326-149">更新 BizTalk 服務組態的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-149">Operation to update the configuration of a BizTalk Service</span></span> |
| <span data-ttu-id="e3326-150">ServiceUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-150">ServiceUpdateBizTalkService</span></span> |<span data-ttu-id="e3326-151">將 BizTalk 服務升級或降級為不同版本的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-151">Operation to upgrade or downgrade a BizTalk Service to a different version</span></span> |
| <span data-ttu-id="e3326-152">PurgeBackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="e3326-152">PurgeBackupBizTalkService</span></span> |<span data-ttu-id="e3326-153">清除超過保留週期的 BizTalk 服務備份的作業</span><span class="sxs-lookup"><span data-stu-id="e3326-153">Operation to purge backups of the BizTalk Service outside the retention period</span></span> |

## <a name="see-also"></a><span data-ttu-id="e3326-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3326-154">See Also</span></span>
* [<span data-ttu-id="e3326-155">備份 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="e3326-155">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="e3326-156">從備份還原 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="e3326-156">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="e3326-157">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="e3326-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="e3326-158">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="e3326-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="e3326-159">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="e3326-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="e3326-160">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="e3326-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="e3326-161">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="e3326-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="e3326-162">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="e3326-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="e3326-163">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="e3326-163">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

