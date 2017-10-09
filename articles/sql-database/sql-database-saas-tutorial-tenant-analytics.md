---
title: "針對多個 Azure SQL database aaaRun 分析查詢 |Microsoft 文件"
description: "從租用戶資料庫將資料擷取至分析資料庫，以便進行離線分析"
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="446ad-104">從租用戶資料庫將資料擷取至分析資料庫，以便進行離線分析</span><span class="sxs-lookup"><span data-stu-id="446ad-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="446ad-105">在本教學課程中，您使用彈性的工作 toorun 查詢的每個租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="446ad-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="446ad-106">hello 作業會擷取票證銷售資料，並將其載入至分析資料庫 （或資料倉儲） 中進行分析。</span><span class="sxs-lookup"><span data-stu-id="446ad-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="446ad-107">hello 分析資料庫是然後查詢 tooextract 所有租用戶此日常操作資料的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="446ad-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="446ad-108">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="446ad-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="446ad-109">建立 hello 租用戶分析資料庫</span><span class="sxs-lookup"><span data-stu-id="446ad-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="446ad-110">建立排程的工作 tooretrieve 資料並填入 hello 分析資料庫</span><span class="sxs-lookup"><span data-stu-id="446ad-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="446ad-111">toocomplete 符合本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="446ad-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="446ad-112">hello Wingtip SaaS 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="446ad-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="446ad-113">toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="446ad-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="446ad-114">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="446ad-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="446ad-115">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="446ad-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="446ad-116">已安裝最新版本的 SQL Server Management Studio (SSMS) hello。</span><span class="sxs-lookup"><span data-stu-id="446ad-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="446ad-117">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="446ad-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="446ad-118">租用戶操作分析模式</span><span class="sxs-lookup"><span data-stu-id="446ad-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="446ad-119">Toouse hello 豐富的租用戶資料儲存在 hello 雲端的其中一個 hello 與 SaaS 應用程式的絕佳機會。</span><span class="sxs-lookup"><span data-stu-id="446ad-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="446ad-120">使用此資料 toogain 深入了解 hello 作業和您的應用程式和您的租用戶的使用方式。</span><span class="sxs-lookup"><span data-stu-id="446ad-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="446ad-121">此資料可以引導開發功能、 使用性增強功能和其他的投資，在 hello 應用程式和平台。</span><span class="sxs-lookup"><span data-stu-id="446ad-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="446ad-122">在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。</span><span class="sxs-lookup"><span data-stu-id="446ad-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="446ad-123">一種方法 tooaccessing 這份資料是 toouse 彈性作業，可讓工作執行 toobe 輸出資料庫和資料表中擷取結果傳回查詢結果。</span><span class="sxs-lookup"><span data-stu-id="446ad-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="446ad-124">取得 hello Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="446ad-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="446ad-125">hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="446ad-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="446ad-126">[步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="446ad-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="446ad-127">部署租用戶分析結果的資料庫</span><span class="sxs-lookup"><span data-stu-id="446ad-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="446ad-128">本教學課程需要的 toohave 資料庫部署的 toocapture hello 產生的指令碼，包含傳回結果的查詢執行的作業。</span><span class="sxs-lookup"><span data-stu-id="446ad-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="446ad-129">讓我們針對此目的，建立一個稱為 tenantanalytics 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="446ad-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="446ad-130">開啟...\\學習模組\\作業分析\\租用戶分析\\*示範 TenantAnalyticsDB.ps1*在 hello *PowerShell ISE*和設定hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="446ad-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="446ad-131">**$DemoScenario** = **2** *部署操作分析資料庫*</span><span class="sxs-lookup"><span data-stu-id="446ad-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="446ad-132">按**F5** toorun hello 的示範指令碼 (該呼叫 hello*部署 TenantAnalyticsDB.ps1*指令碼) 以建立 hello 租用戶分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="446ad-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="446ad-133">建立 hello 示範的某些資料</span><span class="sxs-lookup"><span data-stu-id="446ad-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="446ad-134">開啟...\\學習模組\\作業分析\\租用戶分析\\*示範 TenantAnalyticsDB.ps1*在 hello *PowerShell ISE*和設定hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="446ad-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="446ad-135">**$DemoScenario** = **1** *購買各地事件的票證*</span><span class="sxs-lookup"><span data-stu-id="446ad-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="446ad-136">按**F5** toorun hello 指令碼，並建立購買記錄的票證。</span><span class="sxs-lookup"><span data-stu-id="446ad-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="446ad-137">建立票證購買項目有關的排程的工作 tooretrieve 租用戶分析</span><span class="sxs-lookup"><span data-stu-id="446ad-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="446ad-138">此指令碼會從所有租用戶建立作業 tooretrieve 票證購買資訊。</span><span class="sxs-lookup"><span data-stu-id="446ad-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="446ad-139">一旦彙總成單一資料表，您可以取得有關購買模式在 hello 租用戶之間的票證豐富具洞察力的度量。</span><span class="sxs-lookup"><span data-stu-id="446ad-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="446ad-140">開啟 SSMS 並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="446ad-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="446ad-141">開啟 ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\TicketPurchasesfromAllTenants.sql</span><span class="sxs-lookup"><span data-stu-id="446ad-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="446ad-142">修改&lt;使用者&gt;，使用 hello 使用者名稱，而您在 hello hello 指令碼頂端，hello Wingtip SaaS 應用程式部署時使用**sp\_新增\_目標\_群組\_成員**和**sp\_新增\_作業步驟**</span><span class="sxs-lookup"><span data-stu-id="446ad-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="446ad-143">以滑鼠右鍵按一下，然後選取**連接**，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接</span><span class="sxs-lookup"><span data-stu-id="446ad-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="446ad-144">確保您已連線的 toohello **jobaccount**資料庫，然後按**F5**執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="446ad-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="446ad-145">**預存程序\_新增\_目標\_群組**建立 hello 目標群組名稱*TenantGroup*，現在我們需要 tooadd 目標成員。</span><span class="sxs-lookup"><span data-stu-id="446ad-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="446ad-146">**預存程序\_新增\_目標\_群組\_成員**新增*伺服器*目標成員類型，認為 （這是 hello customer1-請注意該伺服器內的所有資料庫&lt;使用者&gt;包含 hello 租用戶資料庫伺服器) 在工作時間執行應該包含在 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="446ad-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="446ad-147">**sp\_add\_job** 會建立新的每週排定作業，其名稱為「所有租用戶的票證購買」</span><span class="sxs-lookup"><span data-stu-id="446ad-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="446ad-148">**預存程序\_新增\_jobstep**從所有租用戶和複製 hello 傳回的結果集至名為的資料表建立 hello 作業步驟包含 T-SQL 命令文字 tooretrieve 所有 hello 票證購買資訊*AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="446ad-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="446ad-149">hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。</span><span class="sxs-lookup"><span data-stu-id="446ad-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="446ad-150">檢閱從 hello hello 狀態值**生命週期**資料行 toomonitor hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="446ad-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="446ad-151">一次成功，hello 工作已順利完成所有租用戶資料庫上且 hello 包含 hello 的兩個其他資料庫參考資料表。</span><span class="sxs-lookup"><span data-stu-id="446ad-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="446ad-152">已成功執行 hello 指令碼，應該會產生類似的結果：</span><span class="sxs-lookup"><span data-stu-id="446ad-152">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="446ad-154">建立從所有租用戶購買票證摘要計數工作 tooretrieve</span><span class="sxs-lookup"><span data-stu-id="446ad-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="446ad-155">此指令碼會從所有租用戶建立作業的所有票證購買 tooretrieve 總和。</span><span class="sxs-lookup"><span data-stu-id="446ad-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="446ad-156">開啟 SSMS 並連接 toohello*目錄-&lt;使用者&gt;。.database.windows.net*伺服器</span><span class="sxs-lookup"><span data-stu-id="446ad-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="446ad-157">開啟 hello 檔案...\\學習模組\\佈建和類別目錄\\作業分析\\租用戶分析\\*結果 TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="446ad-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="446ad-158">修改&lt;使用者&gt;，使用 hello 使用者名稱，而當您在 hello 指令碼在 hello hello Wingtip SaaS 應用程式部署時，使用**sp\_新增\_jobstep**預存程序</span><span class="sxs-lookup"><span data-stu-id="446ad-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="446ad-159">以滑鼠右鍵按一下，然後選取**連接**，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接</span><span class="sxs-lookup"><span data-stu-id="446ad-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="446ad-160">確保您已連線的 toohello **tenantanalytics**資料庫，然後按**F5**執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="446ad-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="446ad-161">已成功執行 hello 指令碼，應該會產生類似的結果：</span><span class="sxs-lookup"><span data-stu-id="446ad-161">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="446ad-163">**sp\_add\_job** 會建立新的每週排定作業，其名稱為 “ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="446ad-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="446ad-164">**預存程序\_新增\_jobstep**從所有租用戶和複製 hello 傳回的結果集至名為 CountofTicketOrders 的資料表建立 hello 作業步驟包含 T-SQL 命令文字 tooretrieve 所有 hello 票證購買資訊</span><span class="sxs-lookup"><span data-stu-id="446ad-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="446ad-165">hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。</span><span class="sxs-lookup"><span data-stu-id="446ad-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="446ad-166">檢閱從 hello hello 狀態值**生命週期**資料行 toomonitor hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="446ad-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="446ad-167">一次成功，hello 工作已順利完成所有租用戶資料庫上且 hello 包含 hello 的兩個其他資料庫參考資料表。</span><span class="sxs-lookup"><span data-stu-id="446ad-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="446ad-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="446ad-168">Next steps</span></span>

<span data-ttu-id="446ad-169">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="446ad-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="446ad-170">部署租用戶分析資料庫</span><span class="sxs-lookup"><span data-stu-id="446ad-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="446ad-171">在租用戶之間建立排程的工作 tooretrieve 分析資料</span><span class="sxs-lookup"><span data-stu-id="446ad-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="446ad-172">恭喜！</span><span class="sxs-lookup"><span data-stu-id="446ad-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="446ad-173">其他資源</span><span class="sxs-lookup"><span data-stu-id="446ad-173">Additional resources</span></span>

* <span data-ttu-id="446ad-174">其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="446ad-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="446ad-175">彈性作業</span><span class="sxs-lookup"><span data-stu-id="446ad-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
