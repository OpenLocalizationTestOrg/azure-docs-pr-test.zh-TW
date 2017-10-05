---
title: "在多租用戶應用程式中還原 Azure SQL Database | Microsoft Docs"
description: "了解如何在不小心刪除資料之後還原單一租用戶 SQL Database"
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
ms.openlocfilehash: 547851972f13ec69a8f65d01290874ad7d07f192
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a><span data-ttu-id="a2f20-104">還原 Wingtip SaaS 租用戶 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a2f20-104">Restore a Wingtip SaaS tenants SQL database</span></span>

<span data-ttu-id="a2f20-105">Wingtip SaaS 應用程式是使用每一租用戶一個資料庫的模型來建置的，其中每個租用戶都有自己的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-105">The Wingtip SaaS app is built using a database-per-tenant model, where each tenant has their own database.</span></span> <span data-ttu-id="a2f20-106">此模型的其中一個優點是很容易以隔離方式還原單一租用戶的資料，而不會影響到其他租用戶。</span><span class="sxs-lookup"><span data-stu-id="a2f20-106">One of the benefits of this model is that it is easy to restore a single tenant’s data in isolation without impacting other tenants.</span></span>

<span data-ttu-id="a2f20-107">在本教學課程中，您將了解兩個資料復原模式：</span><span class="sxs-lookup"><span data-stu-id="a2f20-107">In this tutorial you learn two data recovery patterns:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="a2f20-108">將資料庫還原到平行資料庫 (並存)</span><span class="sxs-lookup"><span data-stu-id="a2f20-108">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="a2f20-109">就地還原資料庫</span><span class="sxs-lookup"><span data-stu-id="a2f20-109">Restore a database in place</span></span>


|||
|:--|:--|
| <span data-ttu-id="a2f20-110">**將租用戶還原到先前的時間點且還原到平行資料庫**</span><span class="sxs-lookup"><span data-stu-id="a2f20-110">**Restore tenant to a prior point in time, into a parallel database**</span></span> | <span data-ttu-id="a2f20-111">此模式可供租用戶用於檢閱、稽核及合規性等用途。原始資料庫仍保持連線而不變。</span><span class="sxs-lookup"><span data-stu-id="a2f20-111">This pattern can be used by the tenant for review, auditing, compliance, etc. The original database remains online and unchanged.</span></span> |
| <span data-ttu-id="a2f20-112">**就地還原租用戶**</span><span class="sxs-lookup"><span data-stu-id="a2f20-112">**Restore tenant in-place**</span></span> | <span data-ttu-id="a2f20-113">此模式通常是在租用戶不小心將資料刪除後，用來將租用戶復原到先前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-113">This pattern is typically used to recover a tenant to a prior point in time, after a tenant accidentally deletes data.</span></span> <span data-ttu-id="a2f20-114">原始資料庫將會離線，然後被還原的資料庫取代。</span><span class="sxs-lookup"><span data-stu-id="a2f20-114">The original database is taken offline, and replaced with the restored database.</span></span> |
|||

<span data-ttu-id="a2f20-115">若要完成本教學課程，請確定已完成下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="a2f20-115">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="a2f20-116">已部署 Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2f20-116">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="a2f20-117">若要在五分鐘內完成部署，請參閱[部署及探索 Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="a2f20-117">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="a2f20-118">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a2f20-118">Azure PowerShell is installed.</span></span> <span data-ttu-id="a2f20-119">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="a2f20-119">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

## <a name="introduction-to-the-saas-tenant-restore-pattern"></a><span data-ttu-id="a2f20-120">SaaS 租用戶還原模式簡介</span><span class="sxs-lookup"><span data-stu-id="a2f20-120">Introduction to the SaaS tenant restore pattern</span></span>

<span data-ttu-id="a2f20-121">就租用戶還原模式而言，有兩個可還原個別租用戶資料的簡單模式。</span><span class="sxs-lookup"><span data-stu-id="a2f20-121">For the tenant restore pattern, there are two simple patterns for restoring an individual tenant's data.</span></span> <span data-ttu-id="a2f20-122">由於租用戶資料庫彼此互相隔離，因此還原一個租用戶並不會影響到任何其他租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-122">Because tenant databases are isolated from each other, restoring one tenant has no impact on any other tenant's data.</span></span>

<span data-ttu-id="a2f20-123">在第一個模式中，資料會還原到新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-123">In the first pattern, data is restored into a new database.</span></span> <span data-ttu-id="a2f20-124">租用戶會接著獲得存取權來存取此資料庫及它們的生產環境資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-124">The tenant is then given access to this database alongside their production data.</span></span> <span data-ttu-id="a2f20-125">此模式可讓租用戶系統管理員檢閱已還原的資料，並可能使用此資料來選擇性地覆寫目前的資料值。</span><span class="sxs-lookup"><span data-stu-id="a2f20-125">This pattern allows a tenant admin to review the restored data and potentially use it to selectively overwrite current data values.</span></span> <span data-ttu-id="a2f20-126">資料復原選項應有的複雜程度是由 SaaS 應用程式設計人員決定。</span><span class="sxs-lookup"><span data-stu-id="a2f20-126">It's up to the SaaS app designer to determine just how sophisticated the data recovery options should be.</span></span> <span data-ttu-id="a2f20-127">在某些情況下，只要能夠檢閱資料在所指定時間點時的狀態，可能就已足以滿足需求。</span><span class="sxs-lookup"><span data-stu-id="a2f20-127">Simply being able to review data in the state it was in at a given point in time may be all that is required in some scenarios.</span></span> <span data-ttu-id="a2f20-128">如果資料庫使用[異地複寫](sql-database-geo-replication-overview.md)，建議您從已還原的複本將所需的資料複製到原始資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-128">If the database uses [geo-replication](sql-database-geo-replication-overview.md), we recommend copying the required data from the restored copy into the original database.</span></span> <span data-ttu-id="a2f20-129">如果您以已還原的資料庫取代原始資料庫，則必須重新設定並重新同步處理異地複寫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-129">If you replace the original database with the restored database, you need to reconfigure and resynchronize geo-replication.</span></span>

<span data-ttu-id="a2f20-130">在第二個模式中 (其中假設租用戶的資料遺失或損毀)，租用戶的生產環境資料會還原到先前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-130">In the second pattern, which assumes that the tenant has suffered a loss or corruption of data, the tenant’s production database is restored to a prior point in time.</span></span> <span data-ttu-id="a2f20-131">在就地還原模式中，租用戶會在資料庫還原時短暫離線，然後再重新上線。</span><span class="sxs-lookup"><span data-stu-id="a2f20-131">In the restore in place pattern, the tenant is taken offline for a brief time while the database is restored and brought back online.</span></span> <span data-ttu-id="a2f20-132">此模式會將原始資料庫刪除，但如果您需要回到先前時間點中的某個事件，則仍可從此資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="a2f20-132">The original database is deleted, but can still be restored from if you need to go back to an even earlier point in time.</span></span> <span data-ttu-id="a2f20-133">此模式的一個變通形式可將此資料庫重新命名，而不是刪除它，不過就資料安全性而言，將資料庫重新命名並不會提供任何額外的優點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-133">A variation of this pattern could rename the database instead of deleting it, although renaming the database offers no additional advantage in terms of data security.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="a2f20-134">取得 Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="a2f20-134">Get the Wingtip application scripts</span></span>

<span data-ttu-id="a2f20-135">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) Github 存放庫可取得 Wingtip Tickets 指令碼和應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="a2f20-135">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="a2f20-136">[用於下載 Wingtip SaaS 指令碼的步驟](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="a2f20-136">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="simulate-a-tenant-accidentally-deleting-data"></a><span data-ttu-id="a2f20-137">模擬租用戶不小心刪除資料的情況</span><span class="sxs-lookup"><span data-stu-id="a2f20-137">Simulate a tenant accidentally deleting data</span></span>

<span data-ttu-id="a2f20-138">為了示範這些復原情況，我們需要「不小心」刪除其中一個租用戶資料庫中的一些資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-138">To demonstrate these recovery scenarios, we need to *accidentally* delete some data in one of the tenant databases.</span></span> <span data-ttu-id="a2f20-139">您可以刪除任何記錄，而下一個步驟則是設定示範，讓它不會因為違反參考完整性而遭到封鎖！</span><span class="sxs-lookup"><span data-stu-id="a2f20-139">While you can delete any record, the next step sets up the demo to not get blocked by referential integrity violations!</span></span> <span data-ttu-id="a2f20-140">它也會新增一些您可以稍後在＜Wingtip SaaS 分析教學課程＞中使用的票證購買資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-140">It also adds some ticket purchase data you can use later in the *Wingtip SaaS Analytics tutorials*.</span></span>

<span data-ttu-id="a2f20-141">請執行票證產生器指令碼並建立額外的資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-141">Run the ticket generator script and create additional data.</span></span> <span data-ttu-id="a2f20-142">票證產生器會刻意不為每個租用戶的最後一個事件購買票證。</span><span class="sxs-lookup"><span data-stu-id="a2f20-142">The ticket generator intentionally does not purchase tickets for each tenants last event.</span></span>

1. <span data-ttu-id="a2f20-143">在 *PowerShell ISE* 中開啟 ...\\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1*</span><span class="sxs-lookup"><span data-stu-id="a2f20-143">Open ...\\Learning Modules\\Utilities\\*Demo-TicketGenerator.ps1* in the *PowerShell ISE*</span></span>
1. <span data-ttu-id="a2f20-144">按 **F5** 以執行指令碼並產生客戶與票證銷售資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-144">Press **F5** to run the script and generate customers and ticket sales data.</span></span>


### <a name="open-the-events-app-to-review-the-current-events"></a><span data-ttu-id="a2f20-145">開啟事件應用程式以檢閱目前的事件</span><span class="sxs-lookup"><span data-stu-id="a2f20-145">Open the Events app to review the current events</span></span>

1. <span data-ttu-id="a2f20-146">開啟 *[事件中樞]* \(http://events.wtp.&lt;user&gt;.trafficmanager.net)，然後按一下 **[Contoso Concert Hall]**：</span><span class="sxs-lookup"><span data-stu-id="a2f20-146">Open the *Events Hub* (http://events.wtp.&lt;user&gt;.trafficmanager.net) and click **Contoso Concert Hall**:</span></span>

   ![事件中樞](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. <span data-ttu-id="a2f20-148">捲動事件清單，然後記下清單中的最後一個事件：</span><span class="sxs-lookup"><span data-stu-id="a2f20-148">Scroll the list of events and make a note of the last event in the list:</span></span>

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-the-demo-scenario-to-accidentally-delete-the-last-event"></a><span data-ttu-id="a2f20-150">執行示範案例來不小心刪除最後一個事件</span><span class="sxs-lookup"><span data-stu-id="a2f20-150">Run the demo scenario to accidentally delete the last event</span></span>

1. <span data-ttu-id="a2f20-151">在 *PowerShell ISE* 中開啟 ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1*，然後設定下列值：</span><span class="sxs-lookup"><span data-stu-id="a2f20-151">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\*Demo-RestoreTenant.ps1* in the *PowerShell ISE*, and set the following value:</span></span>
   * <span data-ttu-id="a2f20-152">**$DemoScenario** = **1**，設定為 **1** - 刪除沒有任何票證銷售額的事件。</span><span class="sxs-lookup"><span data-stu-id="a2f20-152">**$DemoScenario** = **1**, Set to **1** - Delete events with no ticket sales.</span></span>
1. <span data-ttu-id="a2f20-153">按 **F5** 以執行指令碼並刪除最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="a2f20-153">Press **F5** to run the script and delete the last event.</span></span> <span data-ttu-id="a2f20-154">您應該會看見類似下方的確認訊息：</span><span class="sxs-lookup"><span data-stu-id="a2f20-154">You should see a confirmation message similar to the following:</span></span>

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. <span data-ttu-id="a2f20-155">Contoso 事件頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="a2f20-155">The Contoso events page opens.</span></span> <span data-ttu-id="a2f20-156">請向下捲動並確認該事件已消失。</span><span class="sxs-lookup"><span data-stu-id="a2f20-156">Scroll down and verify the event is gone.</span></span> <span data-ttu-id="a2f20-157">如果該事件仍在清單中，請按一下 [重新整理] 並確認它已消失。</span><span class="sxs-lookup"><span data-stu-id="a2f20-157">If the event is still in the list, click refresh and verify it is gone.</span></span>

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-the-production-database"></a><span data-ttu-id="a2f20-159">將租用戶資料庫以與生產環境資料戶平行的方式還原</span><span class="sxs-lookup"><span data-stu-id="a2f20-159">Restore a tenant database in parallel with the production database</span></span>

<span data-ttu-id="a2f20-160">此練習會將 Contoso Concert Hall 資料庫還原到刪除事件前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-160">This exercise restores the Contoso Concert Hall database to a point in time before the event was deleted.</span></span> <span data-ttu-id="a2f20-161">在於先前的步驟中刪除事件之後，您想要復原並查看已刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-161">After the event is deleted in the previous steps, you want to recover and see the deleted data.</span></span> <span data-ttu-id="a2f20-162">您不需要還原含有所刪除記錄的生產環境資料庫，但基於其他業務原因，您必須復原舊資料庫以存取舊資料。</span><span class="sxs-lookup"><span data-stu-id="a2f20-162">You don't need to restore your production database with the deleted record, but you need to recover the old database to access the old data for other business reasons.</span></span>

 <span data-ttu-id="a2f20-163">*Restore-TenantInParallel.ps1* 指令碼會建立一個平行租用戶資料庫，以及一個平行目錄項目，兩者皆名為 *ContosoConcertHall\_old*。</span><span class="sxs-lookup"><span data-stu-id="a2f20-163">The *Restore-TenantInParallel.ps1* script creates a parallel tenant database, and a parallel catalog entry both named *ContosoConcertHall\_old*.</span></span> <span data-ttu-id="a2f20-164">此復原模式最適用於從較不嚴重的資料遺失進行復原，或用於合規性和稽核復原案例。</span><span class="sxs-lookup"><span data-stu-id="a2f20-164">This pattern of restore is best suited for recovering from a minor data loss or for compliance and auditing recovery scenarios.</span></span> <span data-ttu-id="a2f20-165">當您使用的是[異地複寫](sql-database-geo-replication-overview.md)時，這也是建議採用的方法。</span><span class="sxs-lookup"><span data-stu-id="a2f20-165">It is also the recommended approach when you are using [geo-replication](sql-database-geo-replication-overview.md).</span></span>

1. <span data-ttu-id="a2f20-166">完成[模擬使用者不小心刪除資料的情況](#simulate-a-tenant-accidentally-deleting-data)一節。</span><span class="sxs-lookup"><span data-stu-id="a2f20-166">Complete the [simulate a user accidentally deleting data](#simulate-a-tenant-accidentally-deleting-data) section.</span></span>
1. <span data-ttu-id="a2f20-167">在 *PowerShell ISE* 中開啟 ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_。</span><span class="sxs-lookup"><span data-stu-id="a2f20-167">Open ...\\Learning Modules\\Business Continuity and Disaster Recovery\\RestoreTenant\\_Demo-RestoreTenant.ps1_ in the *PowerShell ISE*.</span></span>
1. <span data-ttu-id="a2f20-168">設定 **$DemoScenario** = **2**，將此項目設定為 **2** 以「平行還原租用戶」。</span><span class="sxs-lookup"><span data-stu-id="a2f20-168">Set **$DemoScenario** = **2**, Set this to **2** to *Restore tenant in parallel*.</span></span>
1. <span data-ttu-id="a2f20-169">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="a2f20-169">Press **F5** to run the script.</span></span>

<span data-ttu-id="a2f20-170">此指令碼會將租用戶資料庫還原 (到平行資料庫) 到您在上一節中刪除事件之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-170">The script restores the tenant database (to a parallel database) to a point in time before you deleted the event in the previous section.</span></span> <span data-ttu-id="a2f20-171">它會建立第二個資料庫、移除此資料庫中任何現有的目錄中繼資料，然後將資料庫新增到目錄中 *ContosoConcertHall\_old* 項目底下。</span><span class="sxs-lookup"><span data-stu-id="a2f20-171">It creates a second database, removes any existing catalog metadata that exists in this database, and adds the database to the catalog under the *ContosoConcertHall\_old* entry.</span></span>

<span data-ttu-id="a2f20-172">此示範指令碼會在您的瀏覽器中開啟事件頁面。</span><span class="sxs-lookup"><span data-stu-id="a2f20-172">The demo script opens the events page in your browser.</span></span> <span data-ttu-id="a2f20-173">請注意 URL：```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old```，這顯示資料來自所還原的資料庫，其中在名稱加上了 *_old*。</span><span class="sxs-lookup"><span data-stu-id="a2f20-173">Note from the URL: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` that this is showing data from the restored database where *_old* is added to the name.</span></span>

<span data-ttu-id="a2f20-174">請捲動瀏覽器中列出的事件，以確認在上一節中刪除的事件已經還原。</span><span class="sxs-lookup"><span data-stu-id="a2f20-174">Scroll the events listed in the browser to confirm that the event deleted in the previous section has been restored.</span></span>

<span data-ttu-id="a2f20-175">請注意，將已還原的租用戶公開為額外的租用戶 (具有自己的「事件」應用程式來瀏覽票證)，不太可能是您將所還原資料的存取權提供給租用戶的方式，但可用來輕鬆說明還原模式。</span><span class="sxs-lookup"><span data-stu-id="a2f20-175">Note that exposing the restored tenant as an additional tenant, with its own Events app to browse tickets, is unlikely to be how you would provide a tenant access to restored data, but serves to easily illustrate the restore pattern.</span></span>

<span data-ttu-id="a2f20-176">事實上，您可能只會依據一段定義的期間保留這個已還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-176">In reality, you would probably only retain this restored database for a defined period.</span></span> <span data-ttu-id="a2f20-177">在您完成作業之後，即可呼叫 *Remove-RestoredTenant.ps1* 指令碼來刪除已還原的租用戶項目。</span><span class="sxs-lookup"><span data-stu-id="a2f20-177">You can delete the restored tenant entry once you are finished by calling the *Remove-RestoredTenant.ps1* script.</span></span>

1. <span data-ttu-id="a2f20-178">將 **$DemoScenario** 設定為 **4** 以選取「移除已還原的租用戶」案例。</span><span class="sxs-lookup"><span data-stu-id="a2f20-178">Set **$DemoScenario** to **4** to select the *remove restored tenant* scenario.</span></span>
1. <span data-ttu-id="a2f20-179">**使用** **F5** 來**執行**</span><span class="sxs-lookup"><span data-stu-id="a2f20-179">**Execute** **using** **F5**</span></span>
1. <span data-ttu-id="a2f20-180">*ContosoConcertHall\_old* 項目現在已從目錄中刪除。</span><span class="sxs-lookup"><span data-stu-id="a2f20-180">The *ContosoConcertHall\_old* entry is now deleted from the catalog.</span></span> <span data-ttu-id="a2f20-181">請在您的瀏覽器中逕行關閉此租用戶的事件頁面。</span><span class="sxs-lookup"><span data-stu-id="a2f20-181">Go ahead and close the events page for this tenant in your browser.</span></span>


## <a name="restore-a-tenant-in-place-replacing-the-existing-tenant-database"></a><span data-ttu-id="a2f20-182">就地還原租用戶，取代現有的租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="a2f20-182">Restore a tenant in place, replacing the existing tenant database</span></span>

<span data-ttu-id="a2f20-183">此練習會將 Contoso Concert Hall 租用戶還原到刪除事件前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-183">This exercise restores the Contoso Concert Hall tenant to a point in time before the event was deleted.</span></span> <span data-ttu-id="a2f20-184">*Restore-TenantInPlace* 指令碼會將目前的租用戶資料庫還原到指向先前時間點的新資料庫，並刪除原始資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-184">The *Restore-TenantInPlace* script restores the current tenant database to a new database pointing to a previous point in time, and deletes the original database.</span></span> <span data-ttu-id="a2f20-185">此復原模式最適用於從嚴重的資料損毀進行復原，因為可能有租用戶將必須調適的重大資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a2f20-185">This pattern of restore is best suited for recovering from serious data corruption as there may be significant data loss that the tenant would have to accommodate.</span></span>

1. <span data-ttu-id="a2f20-186">在 PowerShell ISE 中開啟 **Demo-RestoreTenant.ps1** 檔案</span><span class="sxs-lookup"><span data-stu-id="a2f20-186">Open **Demo-RestoreTenant.ps1** file in PowerShell ISE</span></span>
1. <span data-ttu-id="a2f20-187">將 **$DemoScenario** 設定為 **5** 以選取「就地還原租用戶」案例。</span><span class="sxs-lookup"><span data-stu-id="a2f20-187">Set **$DemoScenario** to **5** to select the *restore tenant in place scenario*.</span></span>
1. <span data-ttu-id="a2f20-188">使用 **F5** 來執行。</span><span class="sxs-lookup"><span data-stu-id="a2f20-188">Execute using **F5**.</span></span>

<span data-ttu-id="a2f20-189">此指令碼會將租用戶資料庫還原到刪除事件前 5 分鐘的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-189">The script restores the tenant database to a point five minutes before the event was deleted.</span></span> <span data-ttu-id="a2f20-190">其做法是先讓 Contoso Concert Hall 租用戶離線，使得對資料無法進行任何進一步的更新。</span><span class="sxs-lookup"><span data-stu-id="a2f20-190">It does this by first taking the Contoso Concert Hall tenant offline so there are no further updates to the data.</span></span> <span data-ttu-id="a2f20-191">然後，會從還原點還原來建立一個平行資料庫，並以時間戳記命名，以確保資料庫名稱不會與現有的租用戶資料庫名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="a2f20-191">Then, a parallel database is created by restoring from the restore point and named with a timestamp to ensure the database name does not conflict with the existing tenant database name.</span></span> <span data-ttu-id="a2f20-192">接著，會刪除舊的租用戶資料庫，並將已還原的資料庫重新命名成原始資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a2f20-192">Next, the old tenant database is deleted, and the restored database is renamed to the original database name.</span></span> <span data-ttu-id="a2f20-193">最後，會讓 Contoso Concert Hall 上線以允許應用程式存取已還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2f20-193">Finally, Contoso Concert Hall is brought online to allow the app access to the restored database.</span></span>

<span data-ttu-id="a2f20-194">您已成功地將資料庫還原到刪除事件前的時間點。</span><span class="sxs-lookup"><span data-stu-id="a2f20-194">You successfully restored the database to a point in time before the event was deleted.</span></span> <span data-ttu-id="a2f20-195">此時會開啟 [事件] 頁面，因此請確認最後一個事件已經還原。</span><span class="sxs-lookup"><span data-stu-id="a2f20-195">The Events page opens, so confirm the last event has been restored.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2f20-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2f20-196">Next steps</span></span>

<span data-ttu-id="a2f20-197">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="a2f20-197">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="a2f20-198">將資料庫還原到平行資料庫 (並存)</span><span class="sxs-lookup"><span data-stu-id="a2f20-198">Restore a database into a parallel database (side-by-side)</span></span>
> * <span data-ttu-id="a2f20-199">就地還原資料庫</span><span class="sxs-lookup"><span data-stu-id="a2f20-199">Restore a database in place</span></span>

[<span data-ttu-id="a2f20-200">管理租用戶資料庫結構描述</span><span class="sxs-lookup"><span data-stu-id="a2f20-200">Manage tenant database schema</span></span>](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a><span data-ttu-id="a2f20-201">其他資源</span><span class="sxs-lookup"><span data-stu-id="a2f20-201">Additional resources</span></span>

* <span data-ttu-id="a2f20-202">其他[以 Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="a2f20-202">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="a2f20-203">使用 Azure SQL Database 的商務持續性概觀</span><span class="sxs-lookup"><span data-stu-id="a2f20-203">Overview of business continuity with Azure SQL Database</span></span>](sql-database-business-continuity.md)
* [<span data-ttu-id="a2f20-204">了解 SQL Database 備份</span><span class="sxs-lookup"><span data-stu-id="a2f20-204">Learn about SQL Database backups</span></span>](sql-database-automated-backups.md)
