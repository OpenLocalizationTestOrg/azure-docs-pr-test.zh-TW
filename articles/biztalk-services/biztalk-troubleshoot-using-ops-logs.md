---
title: "aaaTroubleshoot BizTalk 服務使用作業記錄 |Microsoft 文件"
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
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a><span data-ttu-id="ff47f-104">BizTalk 服務：使用作業記錄檔進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ff47f-104">BizTalk Services: Troubleshoot using operation logs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a><span data-ttu-id="ff47f-105">Hello 作業記錄檔有哪些？</span><span class="sxs-lookup"><span data-stu-id="ff47f-105">What are hello Operation Logs</span></span>
<span data-ttu-id="ff47f-106">作業記錄檔也提供 hello tooview 您的 Azure 服務，包括 BizTalk 服務上執行的作業歷程記錄檔可讓您的 Azure 傳統入口網站的管理服務功能。</span><span class="sxs-lookup"><span data-stu-id="ff47f-106">Operation Logs is a Management Services feature available in hello Azure classic portal that allows you tooview historical logs of operations performed on your Azure services, including BizTalk Services.</span></span> <span data-ttu-id="ff47f-107">這可讓您 tooview 歷程記錄資料相關的 BizTalk 服務訂用帳戶早在 180 天的 toomanagement 作業。</span><span class="sxs-lookup"><span data-stu-id="ff47f-107">This enables you tooview historical data related toomanagement operations on your BizTalk Service subscription as far back as 180 days.</span></span>

> [!NOTE]
> <span data-ttu-id="ff47f-108">在 BizTalk 服務的管理作業，例如 hello 服務啟動時，記錄備份最多，依此類推，只會擷取這項功能。</span><span class="sxs-lookup"><span data-stu-id="ff47f-108">This feature only captures logs for management operations on BizTalk Services, such as when hello service was started, backed up, and so on.</span></span> <span data-ttu-id="ff47f-109">這類作業會受到追蹤，不論它們是否會執行從 hello Azure 傳統入口網站或使用 hello [BizTalk 服務 REST Api](http://msdn.microsoft.com/library/azure/dn232347.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ff47f-109">Such operations are tracked irrespective of whether they are performed from hello Azure classic portal or by using hello [BizTalk Service REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span> <span data-ttu-id="ff47f-110">如需使用管理服務進行追蹤的作業完整清單，請參閱[使用 Azure 管理服務進行追蹤的作業](#bizops)。</span><span class="sxs-lookup"><span data-stu-id="ff47f-110">For a complete list of operations that are tracked using Management Services, see [Operations Tracked Using Azure Management Services](#bizops).</span></span><br/><br/>
> <span data-ttu-id="ff47f-111">這不會擷取 hello 記錄檔中的活動相關 tooBizTalk 服務執行階段 （例如訊息處理橋接器等。）。</span><span class="sxs-lookup"><span data-stu-id="ff47f-111">This does not capture hello logs for activities related tooBizTalk Service runtime (such as message processed by bridges, and so on.).</span></span> <span data-ttu-id="ff47f-112">tooview 這些記錄檔時，使用 hello 從 hello BizTalk 服務入口網站的追蹤檢視。</span><span class="sxs-lookup"><span data-stu-id="ff47f-112">tooview these logs, use hello Tracking view from hello BizTalk Services portal.</span></span> <span data-ttu-id="ff47f-113">如需詳細資訊，請參閱[追蹤訊息](http://msdn.microsoft.com/library/azure/hh949805.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ff47f-113">For more information, see [Tracking Messages](http://msdn.microsoft.com/library/azure/hh949805.aspx).</span></span>
> 
> 

## <a name="view-biztalk-services-operation-logs"></a><span data-ttu-id="ff47f-114">檢視 BizTalk 服務作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="ff47f-114">View BizTalk Services Operation Logs</span></span>
1. <span data-ttu-id="ff47f-115">在 hello Azure 傳統入口網站，選取**管理服務**，然後選取 hello**作業記錄檔** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff47f-115">In hello Azure classic portal, select **Management Services**, and then select hello **Operation Logs** tab.</span></span>
2. <span data-ttu-id="ff47f-116">您可以篩選不同的參數，例如訂閱、 日期範圍、 服務類型 (例如 BizTalk Services)、 服務名稱或 hello 作業 （成功、 失敗） 的狀態為基礎的 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ff47f-116">You can filter hello logs based on different parameters like subscription, date range, service type (e.g. BizTalk Services), service name, or status of hello operation (Succeeded, Failed).</span></span>
3. <span data-ttu-id="ff47f-117">選取 hello 核取記號 tooview hello 篩選清單。</span><span class="sxs-lookup"><span data-stu-id="ff47f-117">Select hello checkmark tooview hello filtered list.</span></span> <span data-ttu-id="ff47f-118">hello 下列影像顯示活動相關的 tootestbiztalkservice:![檢視作業記錄檔][ViewLogs]</span><span class="sxs-lookup"><span data-stu-id="ff47f-118">hello following image shows activities related tootestbiztalkservice: ![View operation logs][ViewLogs]</span></span> 
4. <span data-ttu-id="ff47f-119">進一步了解特定作業，tooview 選取 hello 資料列，然後按一下**詳細資料**hello 底部 hello 工作列中。</span><span class="sxs-lookup"><span data-stu-id="ff47f-119">tooview more about a specific operation, select hello row, and click **Details** in hello task bar at hello bottom.</span></span>

## <span data-ttu-id="ff47f-120"><a name="bizops"></a>使用 Azure 管理服務進行追蹤的作業</span><span class="sxs-lookup"><span data-stu-id="ff47f-120"><a name="bizops"></a>Operations Tracked Using Azure Management Services</span></span>
<span data-ttu-id="ff47f-121">hello 下表列出會追蹤使用 hello Azure 管理服務的 hello 作業：</span><span class="sxs-lookup"><span data-stu-id="ff47f-121">hello following table lists hello operations that are tracked using hello Azure Management Services:</span></span>

| <span data-ttu-id="ff47f-122">作業名稱</span><span class="sxs-lookup"><span data-stu-id="ff47f-122">Operation Name</span></span> | <span data-ttu-id="ff47f-123">工作</span><span class="sxs-lookup"><span data-stu-id="ff47f-123">Task</span></span> |
| --- | --- |
| <span data-ttu-id="ff47f-124">CreateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-124">CreateBizTalkService</span></span> |<span data-ttu-id="ff47f-125">作業 toocreate 新的 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-125">Operation toocreate a new BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-126">DeleteBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-126">DeleteBizTalkService</span></span> |<span data-ttu-id="ff47f-127">作業 toodelete BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-127">Operation toodelete a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-128">RestartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-128">RestartBizTalkService</span></span> |<span data-ttu-id="ff47f-129">作業 toorestart BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-129">Operation toorestart a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-130">StartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-130">StartBizTalkService</span></span> |<span data-ttu-id="ff47f-131">作業 toostart BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-131">Operation toostart a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-132">StopBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-132">StopBizTalkService</span></span> |<span data-ttu-id="ff47f-133">作業 toostop BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-133">Operation toostop a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-134">DisableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-134">DisableBizTalkService</span></span> |<span data-ttu-id="ff47f-135">作業 toodisable BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-135">Operation toodisable a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-136">EnableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-136">EnableBizTalkService</span></span> |<span data-ttu-id="ff47f-137">作業 tooenable BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-137">Operation tooenable a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-138">BackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-138">BackupBizTalkService</span></span> |<span data-ttu-id="ff47f-139">作業 tooback BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-139">Operation tooback up a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-140">RestoreBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-140">RestoreBizTalkService</span></span> |<span data-ttu-id="ff47f-141">作業 toorestore 從指定的備份 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-141">Operation toorestore a BizTalk Service from specified backup</span></span> |
| <span data-ttu-id="ff47f-142">SuspendBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-142">SuspendBizTalkService</span></span> |<span data-ttu-id="ff47f-143">作業 toosuspend BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-143">Operation toosuspend a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-144">ResumeBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-144">ResumeBizTalkService</span></span> |<span data-ttu-id="ff47f-145">作業 tooresume BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-145">Operation tooresume a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-146">ScaleBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-146">ScaleBizTalkService</span></span> |<span data-ttu-id="ff47f-147">作業 tooscale BizTalk 服務向上或向下</span><span class="sxs-lookup"><span data-stu-id="ff47f-147">Operation tooscale a BizTalk Service up or down</span></span> |
| <span data-ttu-id="ff47f-148">ConfigUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-148">ConfigUpdateBizTalkService</span></span> |<span data-ttu-id="ff47f-149">BizTalk 服務作業 tooupdate hello 組態</span><span class="sxs-lookup"><span data-stu-id="ff47f-149">Operation tooupdate hello configuration of a BizTalk Service</span></span> |
| <span data-ttu-id="ff47f-150">ServiceUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-150">ServiceUpdateBizTalkService</span></span> |<span data-ttu-id="ff47f-151">作業 tooupgrade 或降級 tooa 不同 BizTalk 服務的版本</span><span class="sxs-lookup"><span data-stu-id="ff47f-151">Operation tooupgrade or downgrade a BizTalk Service tooa different version</span></span> |
| <span data-ttu-id="ff47f-152">PurgeBackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="ff47f-152">PurgeBackupBizTalkService</span></span> |<span data-ttu-id="ff47f-153">作業 toopurge 備份的 hello 保留期間外 hello BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-153">Operation toopurge backups of hello BizTalk Service outside hello retention period</span></span> |

## <a name="see-also"></a><span data-ttu-id="ff47f-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ff47f-154">See Also</span></span>
* [<span data-ttu-id="ff47f-155">備份 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-155">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="ff47f-156">從備份還原 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="ff47f-156">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="ff47f-157">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="ff47f-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="ff47f-158">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="ff47f-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="ff47f-159">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="ff47f-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="ff47f-160">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="ff47f-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="ff47f-161">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="ff47f-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="ff47f-162">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="ff47f-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="ff47f-163">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="ff47f-163">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

