---
title: "針對多個 Azure SQL Database 執行分析查詢 | Microsoft Docs"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="368c1-104">從租用戶資料庫將資料擷取至分析資料庫，以便進行離線分析</span><span class="sxs-lookup"><span data-stu-id="368c1-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="368c1-105">在本教學課程中，您可以使用彈性作業來對每個租用戶資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="368c1-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="368c1-106">該作業會擷取票券銷售資料，並將其載入至分析資料庫 (或資料倉儲) 中進行分析。</span><span class="sxs-lookup"><span data-stu-id="368c1-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="368c1-107">查詢此分析資料庫，即可以從所有租用戶日常作業資料中擷取深入解析。</span><span class="sxs-lookup"><span data-stu-id="368c1-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="368c1-108">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="368c1-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="368c1-109">建立租用戶分析資料庫</span><span class="sxs-lookup"><span data-stu-id="368c1-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="368c1-110">建立排定作業以擷取資料並填入分析資料庫</span><span class="sxs-lookup"><span data-stu-id="368c1-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="368c1-111">若要完成本教學課程，請確定符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="368c1-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="368c1-112">已部署 Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="368c1-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="368c1-113">若要在五分鐘內完成部署，請參閱[部署及探索 Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="368c1-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="368c1-114">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="368c1-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="368c1-115">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="368c1-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="368c1-116">已安裝最新版的 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="368c1-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="368c1-117">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="368c1-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="368c1-118">租用戶操作分析模式</span><span class="sxs-lookup"><span data-stu-id="368c1-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="368c1-119">SaaS 應用程式的其中一個絕佳機會是使用儲存在雲端的豐富租用戶資料。</span><span class="sxs-lookup"><span data-stu-id="368c1-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="368c1-120">使用此資料來深入了解應用程式和租用戶的作業與使用方式。</span><span class="sxs-lookup"><span data-stu-id="368c1-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="368c1-121">此資料可以引導應用程式和平台中的功能開發、使用性改進及其他投資。</span><span class="sxs-lookup"><span data-stu-id="368c1-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="368c1-122">在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。</span><span class="sxs-lookup"><span data-stu-id="368c1-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="368c1-123">存取此資料的其中一種方法是使用彈性作業，其可讓您在輸出資料庫和資料表中擷取作業執行的結果傳回查詢結果。</span><span class="sxs-lookup"><span data-stu-id="368c1-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="368c1-124">取得 Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="368c1-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="368c1-125">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) Github 存放庫可取得 Wingtip Tickets 指令碼和應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="368c1-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="368c1-126">[用於下載 Wingtip SaaS 指令碼的步驟](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="368c1-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="368c1-127">部署租用戶分析結果的資料庫</span><span class="sxs-lookup"><span data-stu-id="368c1-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="368c1-128">在本教學課程中，您必須部署一個資料庫才能擷取指令碼作業執行的結果，其中包含結果傳回的查詢。</span><span class="sxs-lookup"><span data-stu-id="368c1-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="368c1-129">讓我們針對此目的，建立一個稱為 tenantanalytics 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="368c1-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="368c1-130">在 PowerShell ISE 中開啟 …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\Demo-TenantAnalyticsDB.ps1 並設定下列值：</span><span class="sxs-lookup"><span data-stu-id="368c1-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="368c1-131">**$DemoScenario** = **2** *部署操作分析資料庫*</span><span class="sxs-lookup"><span data-stu-id="368c1-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="368c1-132">按 **F5** 以執行可建立租用戶分析資料庫的示範指令碼 (它會呼叫 *Deploy-TenantAnalyticsDB.ps1* 指令碼)。</span><span class="sxs-lookup"><span data-stu-id="368c1-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="368c1-133">建立一些資料以供示範</span><span class="sxs-lookup"><span data-stu-id="368c1-133">Create some data for the demo</span></span>

1. <span data-ttu-id="368c1-134">在 PowerShell ISE 中開啟 …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\Demo-TenantAnalyticsDB.ps1 並設定下列值：</span><span class="sxs-lookup"><span data-stu-id="368c1-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="368c1-135">**$DemoScenario** = **1** *購買各地事件的票證*</span><span class="sxs-lookup"><span data-stu-id="368c1-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="368c1-136">按 **F5** 以執行指令碼並建立票證購買歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="368c1-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="368c1-137">建立排定作業以擷取有關票證購買的租用戶分析</span><span class="sxs-lookup"><span data-stu-id="368c1-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="368c1-138">此指令碼會建立一個作業，以擷取所有租用戶的票證購買資訊。</span><span class="sxs-lookup"><span data-stu-id="368c1-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="368c1-139">一旦彙總成單一資料表，您就可以取得有關各租用戶票證購買模式的豐富詳細計量。</span><span class="sxs-lookup"><span data-stu-id="368c1-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="368c1-140">開啟 SSMS 並連線到 catalog-&lt;user&gt;.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="368c1-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="368c1-141">開啟 ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\TicketPurchasesfromAllTenants.sql</span><span class="sxs-lookup"><span data-stu-id="368c1-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="368c1-142">修改 &lt;User&gt;，使用您在 **sp\_add\_target\_group\_member** 和 **sp\_add\_jobstep** 指令碼上方部署 Wingtip SaaS 應用程式時使用的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="368c1-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="368c1-143">按一下滑鼠右鍵並選取 [連線]，然後連線到 catalog-&lt;User&gt;.database.windows.net 伺服器 (如果您尚未連線)</span><span class="sxs-lookup"><span data-stu-id="368c1-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="368c1-144">確定您已連線到 **jobaccount** 資料庫，然後按 **F5** 以執行指令碼</span><span class="sxs-lookup"><span data-stu-id="368c1-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="368c1-145">**sp\_add\_target\_group** 會建立名為 TenantGroup 的目標群組，我們現在需要新增目標成員。</span><span class="sxs-lookup"><span data-stu-id="368c1-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="368c1-146">**sp\_add\_target\_group\_member** 會新增「伺服器」 目標成員類型，其認為在作業執行時該伺服器內的所有資料庫 (請注意，這是在作業執行時含有租用戶資料庫的 customer1-&lt;User&gt; 伺服器) 都應該包含在作業中。</span><span class="sxs-lookup"><span data-stu-id="368c1-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="368c1-147">**sp\_add\_job** 會建立新的每週排定作業，其名稱為「所有租用戶的票證購買」</span><span class="sxs-lookup"><span data-stu-id="368c1-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="368c1-148">**sp\_add\_jobstep** 會建立含有 T-SQL 命令文字的作業步驟，以擷取所有租用戶的所有票證購買資訊，並將傳回的結果集複製到名為 AllTicketsPurchasesfromAllTenants 的資料表中</span><span class="sxs-lookup"><span data-stu-id="368c1-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="368c1-149">指令碼中的其餘檢視會顯示物件是否存在，以及監視作業執行。</span><span class="sxs-lookup"><span data-stu-id="368c1-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="368c1-150">檢閱 [生命週期] 資料行中的狀態值以監視狀態。</span><span class="sxs-lookup"><span data-stu-id="368c1-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="368c1-151">一旦成功，便已所有租用戶資料庫和含有參考資料表的其他兩個資料庫上順利完成此作業。</span><span class="sxs-lookup"><span data-stu-id="368c1-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="368c1-152">成功執行指令碼應會導致類似的結果︰</span><span class="sxs-lookup"><span data-stu-id="368c1-152">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="368c1-154">建立一個作業以擷取所有租用戶的票證購買摘要計數</span><span class="sxs-lookup"><span data-stu-id="368c1-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="368c1-155">此指令碼會建立一個作業，以擷取所有租用戶的票證購買總和。</span><span class="sxs-lookup"><span data-stu-id="368c1-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="368c1-156">開啟 SSMS 並連線到 catalog-&lt;User&gt;.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="368c1-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="368c1-157">開啟 …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\Results-TicketPurchasesfromAllTenants.sql 檔案</span><span class="sxs-lookup"><span data-stu-id="368c1-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="368c1-158">修改 &lt;User&gt;，使用您在指令碼和 **sp\_add\_jobstep** 預存程序中部署 Wingtip SaaS 應用程式時使用的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="368c1-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="368c1-159">按一下滑鼠右鍵並選取 [連線]，然後連線到 catalog-&lt;User&gt;.database.windows.net 伺服器 (如果您尚未連線)</span><span class="sxs-lookup"><span data-stu-id="368c1-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="368c1-160">確定您已連線到 **tenantanalytics** 資料庫，然後按 **F5** 以執行指令碼</span><span class="sxs-lookup"><span data-stu-id="368c1-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="368c1-161">成功執行指令碼應會導致類似的結果︰</span><span class="sxs-lookup"><span data-stu-id="368c1-161">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="368c1-163">**sp\_add\_job** 會建立新的每週排定作業，其名稱為 “ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="368c1-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="368c1-164">**sp\_add\_jobstep** 會建立含有 T-SQL 命令文字的作業步驟，以擷取所有租用戶的所有票證購買資訊，並將傳回的結果集複製到名為 CountofTicketOrders 的資料表中</span><span class="sxs-lookup"><span data-stu-id="368c1-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="368c1-165">指令碼中的其餘檢視會顯示物件是否存在，以及監視作業執行。</span><span class="sxs-lookup"><span data-stu-id="368c1-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="368c1-166">檢閱 [生命週期] 資料行中的狀態值以監視狀態。</span><span class="sxs-lookup"><span data-stu-id="368c1-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="368c1-167">一旦成功，便已所有租用戶資料庫和含有參考資料表的其他兩個資料庫上順利完成此作業。</span><span class="sxs-lookup"><span data-stu-id="368c1-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="368c1-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="368c1-168">Next steps</span></span>

<span data-ttu-id="368c1-169">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="368c1-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="368c1-170">部署租用戶分析資料庫</span><span class="sxs-lookup"><span data-stu-id="368c1-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="368c1-171">建立排定作業以擷取各租用戶的分析資料</span><span class="sxs-lookup"><span data-stu-id="368c1-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="368c1-172">恭喜！</span><span class="sxs-lookup"><span data-stu-id="368c1-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="368c1-173">其他資源</span><span class="sxs-lookup"><span data-stu-id="368c1-173">Additional resources</span></span>

* <span data-ttu-id="368c1-174">其他[以 Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="368c1-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="368c1-175">彈性作業</span><span class="sxs-lookup"><span data-stu-id="368c1-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
