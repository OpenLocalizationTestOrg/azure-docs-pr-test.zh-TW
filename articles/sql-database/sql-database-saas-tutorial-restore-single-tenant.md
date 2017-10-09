---
title: "aaaRestore Azure SQL database 中的多租用戶應用程式 |Microsoft 文件"
description: "了解如何 toorestore 單一租用戶 SQL 資料庫不小心刪除的資料之後"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a><span data-ttu-id="d1a9f-104">還原 Wingtip SaaS 租用戶 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d1a9f-104">Restore a Wingtip SaaS tenants SQL database</span></span>

<span data-ttu-id="d1a9f-105">hello Wingtip SaaS 應用程式是使用每個租用戶的資料庫模型，其中每個租用戶都有各自的資料庫所建立。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-105">hello Wingtip SaaS app is built using a database-per-tenant model, where each tenant has their own database.</span></span> <span data-ttu-id="d1a9f-106">其中一個 hello 這個模型的優點是它是簡單 toorestore 單一租用戶隔離，而不會影響其他租用戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-106">One of hello benefits of this model is that it is easy toorestore a single tenant’s data in isolation without impacting other tenants.</span></span>

<span data-ttu-id="d1a9f-107">在本教學課程中，您將了解兩個資料復原模式：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-107">In this tutorial you learn two data recovery patterns:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="d1a9f-108">將資料庫還原到平行資料庫 (並存)</span><span class="sxs-lookup"><span data-stu-id="d1a9f-108">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="d1a9f-109">就地還原資料庫</span><span class="sxs-lookup"><span data-stu-id="d1a9f-109">Restore a database in place</span></span>


|||
|:--|:--|
| <span data-ttu-id="d1a9f-110">**還原時間，租用戶 tooa 先前點到平行資料庫**</span><span class="sxs-lookup"><span data-stu-id="d1a9f-110">**Restore tenant tooa prior point in time, into a parallel database**</span></span> | <span data-ttu-id="d1a9f-111">檢閱、 稽核、 相容性 hello 租用戶可以使用此模式，等 hello 原始資料庫仍在線上且不變。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-111">This pattern can be used by hello tenant for review, auditing, compliance, etc. hello original database remains online and unchanged.</span></span> |
| <span data-ttu-id="d1a9f-112">**就地還原租用戶**</span><span class="sxs-lookup"><span data-stu-id="d1a9f-112">**Restore tenant in-place**</span></span> | <span data-ttu-id="d1a9f-113">此模式相當常用的 toorecover 租用戶 tooa 先前點在租用戶不小心刪除的資料之後的時間。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-113">This pattern is typically used toorecover a tenant tooa prior point in time, after a tenant accidentally deletes data.</span></span> <span data-ttu-id="d1a9f-114">hello 原始資料庫是離線，以及取代 hello 還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-114">hello original database is taken offline, and replaced with hello restored database.</span></span> |
|||

<span data-ttu-id="d1a9f-115">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-115">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="d1a9f-116">hello Wingtip SaaS 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-116">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="d1a9f-117">toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="d1a9f-117">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="d1a9f-118">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-118">Azure PowerShell is installed.</span></span> <span data-ttu-id="d1a9f-119">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="d1a9f-119">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a><span data-ttu-id="d1a9f-120">簡介 toohello SaaS 租用戶還原模式</span><span class="sxs-lookup"><span data-stu-id="d1a9f-120">Introduction toohello SaaS tenant restore pattern</span></span>

<span data-ttu-id="d1a9f-121">Hello 租用戶還原模式，有兩個簡單的模式還原個別租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-121">For hello tenant restore pattern, there are two simple patterns for restoring an individual tenant's data.</span></span> <span data-ttu-id="d1a9f-122">由於租用戶資料庫彼此互相隔離，因此還原一個租用戶並不會影響到任何其他租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-122">Because tenant databases are isolated from each other, restoring one tenant has no impact on any other tenant's data.</span></span>

<span data-ttu-id="d1a9f-123">在 hello 第一個模式中，會將資料還原到新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-123">In hello first pattern, data is restored into a new database.</span></span> <span data-ttu-id="d1a9f-124">hello 租用戶將會授與存取 toothis 資料庫連同其實際執行資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-124">hello tenant is then given access toothis database alongside their production data.</span></span> <span data-ttu-id="d1a9f-125">此模式可讓租用戶系統管理員 tooreview hello 還原資料，且有可能利用 tooselectively 覆寫目前的資料值。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-125">This pattern allows a tenant admin tooreview hello restored data and potentially use it tooselectively overwrite current data values.</span></span> <span data-ttu-id="d1a9f-126">它是最多 toohello SaaS 應用程式設計師 toodetermine 多麼複雜 hello 選項應該是資料復原。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-126">It's up toohello SaaS app designer toodetermine just how sophisticated hello data recovery options should be.</span></span> <span data-ttu-id="d1a9f-127">只要正在 hello 的狀態，在特定時點的時間可以 tooreview 資料可能只需要在某些情況下。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-127">Simply being able tooreview data in hello state it was in at a given point in time may be all that is required in some scenarios.</span></span> <span data-ttu-id="d1a9f-128">如果 hello 資料庫使用[地理複寫](sql-database-geo-replication-overview.md)，我們建議您所需的 hello 資料複製到 hello 原始資料庫的 hello 還原複本。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-128">If hello database uses [geo-replication](sql-database-geo-replication-overview.md), we recommend copying hello required data from hello restored copy into hello original database.</span></span> <span data-ttu-id="d1a9f-129">如果您取代 hello 原始資料庫與 hello 還原資料庫時，您會需要 tooreconfigure，並重新同步處理地理複寫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-129">If you replace hello original database with hello restored database, you need tooreconfigure and resynchronize geo-replication.</span></span>

<span data-ttu-id="d1a9f-130">Hello 租用戶的實際執行資料庫還原在 hello 第二個模式中，假設該 hello 租用戶發生遺失或損毀的資料，tooa 先前時間點。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-130">In hello second pattern, which assumes that hello tenant has suffered a loss or corruption of data, hello tenant’s production database is restored tooa prior point in time.</span></span> <span data-ttu-id="d1a9f-131">在 hello 還原中的位置模式中，hello 租用戶會離線短暫時還原並上線 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-131">In hello restore in place pattern, hello tenant is taken offline for a brief time while hello database is restored and brought back online.</span></span> <span data-ttu-id="d1a9f-132">hello 原始資料庫已刪除，但仍可還原從如果您需要 toogo 後 tooan 更早的時間點。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-132">hello original database is deleted, but can still be restored from if you need toogo back tooan even earlier point in time.</span></span> <span data-ttu-id="d1a9f-133">此模式的一種變化無法重新命名 hello 資料庫，而不刪除，雖然重新命名的 hello 資料庫提供不了任何其他的優勢，根據資料安全性。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-133">A variation of this pattern could rename hello database instead of deleting it, although renaming hello database offers no additional advantage in terms of data security.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="d1a9f-134">取得 hello Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="d1a9f-134">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="d1a9f-135">hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-135">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="d1a9f-136">[步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-136">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="simulate-a-tenant-accidentally-deleting-data"></a><span data-ttu-id="d1a9f-137">模擬租用戶不小心刪除資料的情況</span><span class="sxs-lookup"><span data-stu-id="d1a9f-137">Simulate a tenant accidentally deleting data</span></span>

<span data-ttu-id="d1a9f-138">toodemonstrate 這些復原案例中，我們需要太*意外*刪除其中一個 hello 租用戶資料庫中的部分資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-138">toodemonstrate these recovery scenarios, we need too*accidentally* delete some data in one of hello tenant databases.</span></span> <span data-ttu-id="d1a9f-139">您可以刪除任何記錄，而參考完整性違規取得封鎖 hello 下一個步驟設定 hello 示範 toonot ！</span><span class="sxs-lookup"><span data-stu-id="d1a9f-139">While you can delete any record, hello next step sets up hello demo toonot get blocked by referential integrity violations!</span></span> <span data-ttu-id="d1a9f-140">它也會加入您可以使用某些票證採購資料稍後 hello *Wingtip SaaS 分析教學課程*。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-140">It also adds some ticket purchase data you can use later in hello *Wingtip SaaS Analytics tutorials*.</span></span>

<span data-ttu-id="d1a9f-141">執行 hello 票證產生器的指令碼並建立其他資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-141">Run hello ticket generator script and create additional data.</span></span> <span data-ttu-id="d1a9f-142">刻意 hello 票證產生器不會購買的每個租用戶最後一個事件的票證。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-142">hello ticket generator intentionally does not purchase tickets for each tenants last event.</span></span>

1. <span data-ttu-id="d1a9f-143">開啟...\\學習模組\\公用程式\\*示範 TicketGenerator.ps1*在 hello *PowerShell ISE*</span><span class="sxs-lookup"><span data-stu-id="d1a9f-143">Open ...\\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1* in hello *PowerShell ISE*</span></span>
1. <span data-ttu-id="d1a9f-144">按**F5** toorun hello 指令碼和產生客戶和票證銷售資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-144">Press **F5** toorun hello script and generate customers and ticket sales data.</span></span>


### <a name="open-hello-events-app-tooreview-hello-current-events"></a><span data-ttu-id="d1a9f-145">開啟 hello 事件應用程式 tooreview hello 目前事件</span><span class="sxs-lookup"><span data-stu-id="d1a9f-145">Open hello Events app tooreview hello current events</span></span>

1. <span data-ttu-id="d1a9f-146">開啟 hello*事件中樞*(http://events.wtp。&lt;使用者&gt;。 trafficmanager.net) 按一下**Contoso 搭配 Hall**:</span><span class="sxs-lookup"><span data-stu-id="d1a9f-146">Open hello *Events Hub* (http://events.wtp.&lt;user&gt;.trafficmanager.net) and click **Contoso Concert Hall**:</span></span>

   ![事件中樞](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. <span data-ttu-id="d1a9f-148">捲動 hello 事件清單，並記下 hello 最後一個事件 hello 清單中：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-148">Scroll hello list of events and make a note of hello last event in hello list:</span></span>

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a><span data-ttu-id="d1a9f-150">執行 hello 示範案例 tooaccidentally delete hello 最後一個事件</span><span class="sxs-lookup"><span data-stu-id="d1a9f-150">Run hello demo scenario tooaccidentally delete hello last event</span></span>

1. <span data-ttu-id="d1a9f-151">開啟...\\學習模組\\業務續航力和災害復原\\RestoreTenant\\*示範 RestoreTenant.ps1*在 hello *PowerShell ISE*，並設定 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-151">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1* in hello *PowerShell ISE*, and set hello following value:</span></span>
   * <span data-ttu-id="d1a9f-152">**$DemoScenario** = **1**，太將**1** -刪除沒有任何票證銷售的事件。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-152">**$DemoScenario** = **1**, Set too**1** - Delete events with no ticket sales.</span></span>
1. <span data-ttu-id="d1a9f-153">按**F5** toorun hello 指令碼，並刪除 hello 最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-153">Press **F5** toorun hello script and delete hello last event.</span></span> <span data-ttu-id="d1a9f-154">您應該會看到確認訊息類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-154">You should see a confirmation message similar toohello following:</span></span>

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. <span data-ttu-id="d1a9f-155">hello Contoso 事件頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-155">hello Contoso events page opens.</span></span> <span data-ttu-id="d1a9f-156">向下捲動並確認 hello 事件就會消失。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-156">Scroll down and verify hello event is gone.</span></span> <span data-ttu-id="d1a9f-157">如果 hello 事件仍在 hello 清單中，按一下 重新整理，並確認它消失。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-157">If hello event is still in hello list, click refresh and verify it is gone.</span></span>

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a><span data-ttu-id="d1a9f-159">還原租用戶資料庫與 hello 生產資料庫並行</span><span class="sxs-lookup"><span data-stu-id="d1a9f-159">Restore a tenant database in parallel with hello production database</span></span>

<span data-ttu-id="d1a9f-160">這個練習還原 hello Contoso 搭配 Hall database tooa 點之前已刪除 hello 事件的時間。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-160">This exercise restores hello Contoso Concert Hall database tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="d1a9f-161">在 hello 先前步驟中刪除 hello 事件之後，您會想 toorecover，並查看 hello 刪除資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-161">After hello event is deleted in hello previous steps, you want toorecover and see hello deleted data.</span></span> <span data-ttu-id="d1a9f-162">您不需要 toorestore 與 hello 刪除記錄，在生產資料庫，但您需要針對其他商業用途的 toorecover hello 舊資料庫 tooaccess hello 舊資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-162">You don't need toorestore your production database with hello deleted record, but you need toorecover hello old database tooaccess hello old data for other business reasons.</span></span>

 <span data-ttu-id="d1a9f-163">hello*還原 TenantInParallel.ps1*指令碼會建立平行的租用戶資料庫，以及平行類別目錄項目這兩個名為*ContosoConcertHall\_舊*。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-163">hello *Restore-TenantInParallel.ps1* script creates a parallel tenant database, and a parallel catalog entry both named *ContosoConcertHall\_old*.</span></span> <span data-ttu-id="d1a9f-164">此復原模式最適用於從較不嚴重的資料遺失進行復原，或用於合規性和稽核復原案例。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-164">This pattern of restore is best suited for recovering from a minor data loss or for compliance and auditing recovery scenarios.</span></span> <span data-ttu-id="d1a9f-165">它也是建議的方法，當您使用的 hello[地理複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-165">It is also hello recommended approach when you are using [geo-replication](sql-database-geo-replication-overview.md).</span></span>

1. <span data-ttu-id="d1a9f-166">完整的 hello[模擬使用者不小心刪除資料](#simulate-a-tenant-accidentally-deleting-data)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-166">Complete hello [simulate a user accidentally deleting data](#simulate-a-tenant-accidentally-deleting-data) section.</span></span>
1. <span data-ttu-id="d1a9f-167">開啟...\\學習模組\\業務續航力和災害復原\\RestoreTenant\\_示範 RestoreTenant.ps1_在 hello *PowerShell ISE*.</span><span class="sxs-lookup"><span data-stu-id="d1a9f-167">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_ in hello *PowerShell ISE*.</span></span>
1. <span data-ttu-id="d1a9f-168">設定**$DemoScenario** = **2**，設定得**2**太*還原租用戶，以平行方式*。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-168">Set **$DemoScenario** = **2**, Set this too**2** too*Restore tenant in parallel*.</span></span>
1. <span data-ttu-id="d1a9f-169">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-169">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="d1a9f-170">hello 指令碼還原 hello 租用戶資料庫 （tooa 平行資料庫） tooa 點刪除 hello 前一節中的 hello 事件之前的時間。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-170">hello script restores hello tenant database (tooa parallel database) tooa point in time before you deleted hello event in hello previous section.</span></span> <span data-ttu-id="d1a9f-171">它會建立第二個資料庫，移除任何現有的目錄中繼資料存在於此資料庫，並將 hello 資料庫 toohello 目錄下 hello *ContosoConcertHall\_舊*項目。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-171">It creates a second database, removes any existing catalog metadata that exists in this database, and adds hello database toohello catalog under hello *ContosoConcertHall\_old* entry.</span></span>

<span data-ttu-id="d1a9f-172">hello 的示範指令碼會在您的瀏覽器中開啟 hello 事件頁面。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-172">hello demo script opens hello events page in your browser.</span></span> <span data-ttu-id="d1a9f-173">請注意，從 hello URL:```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old```這會顯示 hello 還原資料庫中的資料其中*_old*加入 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-173">Note from hello URL: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` that this is showing data from hello restored database where *_old* is added toohello name.</span></span>

<span data-ttu-id="d1a9f-174">已還原捲動 hello 事件列在 hello 瀏覽器 tooconfirm hello 刪除 hello 前一節中的事件。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-174">Scroll hello events listed in hello browser tooconfirm that hello event deleted in hello previous section has been restored.</span></span>

<span data-ttu-id="d1a9f-175">請注意該公開 hello 還原租用戶，因為與它自己的事件的應用程式 toobrowse 票證的其他租用戶不太可能 toobe 會提供租用戶存取 toorestored 資料，但可做 tooeasily 說明 hello 還原模式的方式。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-175">Note that exposing hello restored tenant as an additional tenant, with its own Events app toobrowse tickets, is unlikely toobe how you would provide a tenant access toorestored data, but serves tooeasily illustrate hello restore pattern.</span></span>

<span data-ttu-id="d1a9f-176">事實上，您可能只會依據一段定義的期間保留這個已還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-176">In reality, you would probably only retain this restored database for a defined period.</span></span> <span data-ttu-id="d1a9f-177">您可以刪除 hello 還原租用戶項目，當您已完成後，由呼叫 hello*移除 RestoredTenant.ps1*指令碼。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-177">You can delete hello restored tenant entry once you are finished by calling hello *Remove-RestoredTenant.ps1* script.</span></span>

1. <span data-ttu-id="d1a9f-178">設定**$DemoScenario**太**4** tooselect hello*還原移除租用戶*案例。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-178">Set **$DemoScenario** too**4** tooselect hello *remove restored tenant* scenario.</span></span>
1. <span data-ttu-id="d1a9f-179">**使用** **F5** 來**執行**</span><span class="sxs-lookup"><span data-stu-id="d1a9f-179">**Execute** **using** **F5**</span></span>
1. <span data-ttu-id="d1a9f-180">hello *ContosoConcertHall\_舊*從 hello 類別目錄現在刪除項目。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-180">hello *ContosoConcertHall\_old* entry is now deleted from hello catalog.</span></span> <span data-ttu-id="d1a9f-181">請繼續並關閉您的瀏覽器中的此租用戶的 hello 事件頁面。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-181">Go ahead and close hello events page for this tenant in your browser.</span></span>


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a><span data-ttu-id="d1a9f-182">還原租用戶的位置，以取代 hello 現有租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="d1a9f-182">Restore a tenant in place, replacing hello existing tenant database</span></span>

<span data-ttu-id="d1a9f-183">這個練習還原 hello Contoso 搭配 Hall 租用戶 tooa 點之前已刪除 hello 事件的時間。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-183">This exercise restores hello Contoso Concert Hall tenant tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="d1a9f-184">hello*還原 TenantInPlace*指令碼還原 hello 目前租用戶資料庫 tooa 新資料庫指向 tooa 前一個點的時間，並刪除 hello 原始資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-184">hello *Restore-TenantInPlace* script restores hello current tenant database tooa new database pointing tooa previous point in time, and deletes hello original database.</span></span> <span data-ttu-id="d1a9f-185">從嚴重的資料損毀復原，因為可能會有重大資料遺失的 hello 租用戶會有 tooaccommodate，最適合這種模式的還原。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-185">This pattern of restore is best suited for recovering from serious data corruption as there may be significant data loss that hello tenant would have tooaccommodate.</span></span>

1. <span data-ttu-id="d1a9f-186">在 PowerShell ISE 中開啟 **Demo-RestoreTenant.ps1** 檔案</span><span class="sxs-lookup"><span data-stu-id="d1a9f-186">Open **Demo-RestoreTenant.ps1** file in PowerShell ISE</span></span>
1. <span data-ttu-id="d1a9f-187">設定**$DemoScenario**太**5** tooselect hello*還原位置的案例中的租用戶*。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-187">Set **$DemoScenario** too**5** tooselect hello *restore tenant in place scenario*.</span></span>
1. <span data-ttu-id="d1a9f-188">使用 **F5** 來執行。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-188">Execute using **F5**.</span></span>

<span data-ttu-id="d1a9f-189">hello 指令碼會還原 hello 租用戶資料庫 tooa 點五分鐘的時間才能 hello 事件已刪除。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-189">hello script restores hello tenant database tooa point five minutes before hello event was deleted.</span></span> <span data-ttu-id="d1a9f-190">其做法是先採取 hello Contoso 搭配 Hall 離線因此沒有其他進一步的租用戶更新 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-190">It does this by first taking hello Contoso Concert Hall tenant offline so there are no further updates toohello data.</span></span> <span data-ttu-id="d1a9f-191">然後，建立從 hello 還原點還原，名為平行資料庫時間戳記 tooensure hello 資料庫名稱未與 hello 現有租用戶資料庫名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-191">Then, a parallel database is created by restoring from hello restore point and named with a timestamp tooensure hello database name does not conflict with hello existing tenant database name.</span></span> <span data-ttu-id="d1a9f-192">接下來，hello 舊的租用戶資料庫被刪除，且 hello 還原的資料庫重新命名的 toohello 原始資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-192">Next, hello old tenant database is deleted, and hello restored database is renamed toohello original database name.</span></span> <span data-ttu-id="d1a9f-193">最後，Contoso 搭配 Hall 資料庫處於線上 tooallow hello 應用程式存取 toohello 還原資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-193">Finally, Contoso Concert Hall is brought online tooallow hello app access toohello restored database.</span></span>

<span data-ttu-id="d1a9f-194">您已成功刪除 hello 事件之前的時間還原 hello database tooa 點。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-194">You successfully restored hello database tooa point in time before hello event was deleted.</span></span> <span data-ttu-id="d1a9f-195">hello 事件頁面隨即開啟，因此確認還原 hello 最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="d1a9f-195">hello Events page opens, so confirm hello last event has been restored.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d1a9f-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1a9f-196">Next steps</span></span>

<span data-ttu-id="d1a9f-197">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="d1a9f-197">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="d1a9f-198">將資料庫還原到平行資料庫 (並存)</span><span class="sxs-lookup"><span data-stu-id="d1a9f-198">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="d1a9f-199">就地還原資料庫</span><span class="sxs-lookup"><span data-stu-id="d1a9f-199">Restore a database in place</span></span>

[<span data-ttu-id="d1a9f-200">管理租用戶資料庫結構描述</span><span class="sxs-lookup"><span data-stu-id="d1a9f-200">Manage tenant database schema</span></span>](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a><span data-ttu-id="d1a9f-201">其他資源</span><span class="sxs-lookup"><span data-stu-id="d1a9f-201">Additional resources</span></span>

* <span data-ttu-id="d1a9f-202">其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="d1a9f-202">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="d1a9f-203">使用 Azure SQL Database 的商務持續性概觀</span><span class="sxs-lookup"><span data-stu-id="d1a9f-203">Overview of business continuity with Azure SQL Database</span></span>](sql-database-business-continuity.md)
* [<span data-ttu-id="d1a9f-204">了解 SQL Database 備份</span><span class="sxs-lookup"><span data-stu-id="d1a9f-204">Learn about SQL Database backups</span></span>](sql-database-automated-backups.md)
