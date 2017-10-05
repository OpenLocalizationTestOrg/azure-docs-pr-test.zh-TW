---
title: "在多租用戶應用程式中管理 Azure SQL Database 結構描述 | Microsoft Docs"
description: "在使用 Azure SQL Database 的多租用戶應用程式中，管理多租用戶的結構描述"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: 78d76efb88bf11fa18a416b59e6f881539141232
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-schema-for-multiple-tenants-in-the-wingtip-saas-application"></a><span data-ttu-id="f6e61-104">針對 Wingtip SaaS 應用程式中的多個租用戶管理結構描述</span><span class="sxs-lookup"><span data-stu-id="f6e61-104">Manage schema for multiple tenants in the Wingtip SaaS application</span></span>

<span data-ttu-id="f6e61-105">[第一個 Wingtip SaaS 教學課程](sql-database-saas-tutorial.md)說明應用程式如何佈建租用戶資料庫並在目錄中註冊它。</span><span class="sxs-lookup"><span data-stu-id="f6e61-105">The [first Wingtip SaaS tutorial](sql-database-saas-tutorial.md) shows how the app can provision a tenant database and register it in the catalog.</span></span> <span data-ttu-id="f6e61-106">就像任何應用程式一樣，Wingtip SaaS 應用程式會隨著時間演進，而且有時候會需要變更資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6e61-106">Like any application, the Wingtip SaaS app will evolve over time, and at times will require changes to the database.</span></span> <span data-ttu-id="f6e61-107">變更可能包含新增或變更的結構描述、新增或變更的參考資料，以及例行性資料庫維護工作以確保最佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="f6e61-107">Changes may include new or changed schema, new or changed reference data, and routine database maintenance tasks to ensure optimal app performance.</span></span> <span data-ttu-id="f6e61-108">有了 SaaS 應用程式，這些變更需要以經過協調的方式部署到可能非常大規模的租用戶資料庫群。</span><span class="sxs-lookup"><span data-stu-id="f6e61-108">With a SaaS application, these changes need to be deployed in a coordinated manner across a potentially massive fleet of tenant databases.</span></span> <span data-ttu-id="f6e61-109">變更也需要整合到佈建程序中，以供未來在租用戶資料庫中使用。</span><span class="sxs-lookup"><span data-stu-id="f6e61-109">For these changes to be in future tenant databases, they need to be incorporated into the provisioning process.</span></span>

<span data-ttu-id="f6e61-110">本教學課程會探討兩種案例：為所有租用戶部署參考資料更新，以及針對包含參考資料的資料表重新調整索引。</span><span class="sxs-lookup"><span data-stu-id="f6e61-110">This tutorial explores two scenarios - deploying reference data updates for all tenants, and retuning an index on the table containing the reference data.</span></span> <span data-ttu-id="f6e61-111">[彈性作業](sql-database-elastic-jobs-overview.md)功能是用來跨所有租用戶執行這些作業，而「範本」租用戶資料庫則是用來作為新資料庫的範本。</span><span class="sxs-lookup"><span data-stu-id="f6e61-111">The [Elastic jobs](sql-database-elastic-jobs-overview.md) feature is used to execute these operations across all tenants, and the *golden* tenant database that is used as a template for new databases.</span></span>

<span data-ttu-id="f6e61-112">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="f6e61-112">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="f6e61-113">建立作業帳戶</span><span class="sxs-lookup"><span data-stu-id="f6e61-113">Create a job account</span></span>
> * <span data-ttu-id="f6e61-114">跨多個租用戶進行查詢</span><span class="sxs-lookup"><span data-stu-id="f6e61-114">Query across multiple tenants</span></span>
> * <span data-ttu-id="f6e61-115">更新所有租用戶資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="f6e61-115">Update data in all tenant databases</span></span>
> * <span data-ttu-id="f6e61-116">針對所有租用戶資料庫中的資料表建立索引</span><span class="sxs-lookup"><span data-stu-id="f6e61-116">Create an index on a table in all tenant databases</span></span>


<span data-ttu-id="f6e61-117">若要完成本教學課程，請確定符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="f6e61-117">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="f6e61-118">已部署 Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6e61-118">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="f6e61-119">若要在五分鐘內完成部署，請參閱[部署及探索 Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="f6e61-119">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="f6e61-120">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f6e61-120">Azure PowerShell is installed.</span></span> <span data-ttu-id="f6e61-121">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="f6e61-121">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="f6e61-122">已安裝最新版的 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="f6e61-122">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="f6e61-123">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="f6e61-123">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

<span data-ttu-id="f6e61-124">*本教學課程使用的 SQL Database 服務功能處於有限預覽版狀態 (彈性資料庫作業)。如果想要進行本教學課程，請將您的訂用帳戶識別碼提供給 SaaSFeedback@microsoft.com，並使用主旨 Elastic Jobs Preview (彈性作業預覽)。在您收到訂用帳戶已啟用的確認之後，請[下載並安裝最新的發行前版本作業 Cmdlet (英文)](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*</span><span class="sxs-lookup"><span data-stu-id="f6e61-124">*This tutorial uses features of the SQL Database service that are in a limited preview (Elastic Database jobs). If you wish to do this tutorial, provide your subscription id to SaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install the latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>


## <a name="introduction-to-saas-schema-management-patterns"></a><span data-ttu-id="f6e61-125">SaaS 結構描述管理模式的簡介</span><span class="sxs-lookup"><span data-stu-id="f6e61-125">Introduction to SaaS Schema Management patterns</span></span>

<span data-ttu-id="f6e61-126">每個資料庫單一租用戶的 SaaS 模式可以達成資料隔離而獲得許多方面的好處，但同時也會造成維護及管理許多資料庫的額外複雜性。</span><span class="sxs-lookup"><span data-stu-id="f6e61-126">The single tenant per database SaaS pattern benefits in many ways from the data isolation that results, but at the same time introduces the additional complexity of maintaining and managing many databases.</span></span> <span data-ttu-id="f6e61-127">[彈性作業](sql-database-elastic-jobs-overview.md)有助於 SQL 資料層的管理。</span><span class="sxs-lookup"><span data-stu-id="f6e61-127">[Elastic Jobs](sql-database-elastic-jobs-overview.md) facilitates administration and management of the SQL data tier.</span></span> <span data-ttu-id="f6e61-128">作業可讓您針對一組資料庫安全可靠地執行工作 (T-SQL 指令碼)，而不需要使用者互動或輸入。</span><span class="sxs-lookup"><span data-stu-id="f6e61-128">Jobs enable you to securely and reliably, run tasks (T-SQL scripts) independent of user interaction or input, against a group of databases.</span></span> <span data-ttu-id="f6e61-129">這個方法可用來在應用程式中跨所有租用戶部署結構描述和一般參考資料變更。</span><span class="sxs-lookup"><span data-stu-id="f6e61-129">This method can be used to deploy schema and common reference data changes across all tenants in an application.</span></span> <span data-ttu-id="f6e61-130">彈性作業也可以用來維護建立新租用戶所使用的「範本」資料庫複本，確保它隨時具有最新的結構描述和參考資料。</span><span class="sxs-lookup"><span data-stu-id="f6e61-130">Elastic Jobs can also be used to maintain a *golden* copy of the database used to create new tenants, ensuring it always has the latest schema and reference data.</span></span>

![畫面](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a><span data-ttu-id="f6e61-132">彈性作業有限預覽版</span><span class="sxs-lookup"><span data-stu-id="f6e61-132">Elastic Jobs limited preview</span></span>

<span data-ttu-id="f6e61-133">新版本的「彈性作業」現在是 Azure SQL Database 的整合功能 (不需要額外的服務或元件)。</span><span class="sxs-lookup"><span data-stu-id="f6e61-133">There is a new version of Elastic Jobs that is now an integrated feature of Azure SQL Database (that requires no additional services or components).</span></span> <span data-ttu-id="f6e61-134">這個新的「彈性作業」版本目前處於有限預覽版狀態。</span><span class="sxs-lookup"><span data-stu-id="f6e61-134">This new version of Elastic Jobs is currently in limited preview.</span></span> <span data-ttu-id="f6e61-135">這個有限預覽版目前支援使用 PowerShell 建立作業帳戶，以及使用 T-SQL 建立及管理作業。</span><span class="sxs-lookup"><span data-stu-id="f6e61-135">This limited preview currently supports PowerShell to create job accounts, and T-SQL to create and manage jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e61-136">*本教學課程使用的 SQL Database 服務功能處於有限預覽版狀態 (彈性資料庫作業)。如果想要進行本教學課程，請將您的訂用帳戶識別碼提供給 SaaSFeedback@microsoft.com，並使用主旨 Elastic Jobs Preview (彈性作業預覽)。在您收到訂用帳戶已啟用的確認之後，請[下載並安裝最新的發行前版本作業 Cmdlet (英文)](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*</span><span class="sxs-lookup"><span data-stu-id="f6e61-136">*This tutorial uses features of the SQL Database service that are in a limited preview (Elastic Database jobs). If you wish to do this tutorial, provide your subscription id to SaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install the latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="f6e61-137">取得 Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="f6e61-137">Get the Wingtip application scripts</span></span>

<span data-ttu-id="f6e61-138">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) Github 存放庫可取得 Wingtip Tickets 指令碼和應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6e61-138">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="f6e61-139">[用於下載 Wingtip SaaS 指令碼的步驟](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="f6e61-139">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-a-job-account-database-and-new-job-account"></a><span data-ttu-id="f6e61-140">建立作業帳戶資料庫和新的作業帳戶</span><span class="sxs-lookup"><span data-stu-id="f6e61-140">Create a job account database and new job account</span></span>

<span data-ttu-id="f6e61-141">本教學課程要求您必須使用 PowerShell 建立作業帳戶資料庫和作業帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6e61-141">This tutorial requires you use PowerShell to create the job account database and job account.</span></span> <span data-ttu-id="f6e61-142">如同 MSDB 和 SQL Agent，「彈性作業」會使用 Azure SQL 資料庫來儲存作業定義、作業狀態和歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f6e61-142">Like MSDB and SQL Agent, Elastic Jobs uses an Azure SQL database to store job definitions, job status, and history.</span></span> <span data-ttu-id="f6e61-143">一旦建立作業帳戶，您就可以立即建立及監視作業。</span><span class="sxs-lookup"><span data-stu-id="f6e61-143">Once the job account is created, you can create and monitor jobs immediately.</span></span>

1. <span data-ttu-id="f6e61-144">在 [PowerShell ISE] 中開啟 …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1*。</span><span class="sxs-lookup"><span data-stu-id="f6e61-144">Open …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1* in the **PowerShell ISE**.</span></span>
1. <span data-ttu-id="f6e61-145">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6e61-145">Press **F5** to run the script.</span></span>

<span data-ttu-id="f6e61-146">*Demo-SchemaManagement.ps1* 指令碼會呼叫 *Deploy-SchemaManagement.ps1* 指令碼，以在類別目錄伺服器上建立名為 **jobaccount** 的 *S2* 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6e61-146">The *Demo-SchemaManagement.ps1* script calls the *Deploy-SchemaManagement.ps1* script to create an *S2* database named **jobaccount** on the catalog server.</span></span> <span data-ttu-id="f6e61-147">然後，它會建立作業帳戶，將 jobaccount 資料庫當成參數傳遞至作業帳戶建立呼叫。</span><span class="sxs-lookup"><span data-stu-id="f6e61-147">It then creates the job account, passing the jobaccount database as a parameter to the job account creation call.</span></span>

## <a name="create-a-job-to-deploy-new-reference-data-to-all-tenants"></a><span data-ttu-id="f6e61-148">建立作業以將新的參考資料部署到所有租用戶</span><span class="sxs-lookup"><span data-stu-id="f6e61-148">Create a job to deploy new reference data to all tenants</span></span>

<span data-ttu-id="f6e61-149">每個租用戶資料庫都包含一組場地類型，其中定義要在場地舉辦的活動種類。</span><span class="sxs-lookup"><span data-stu-id="f6e61-149">Each tenant database includes a set of venue types that define the kind of events that are hosted at a venue.</span></span> <span data-ttu-id="f6e61-150">在這個練習中，您要將更新部署到所有租用戶資料庫，以新增兩個額外的場地類型：*Motorcycle Racing* (機車賽) 和 *Swimming Club* (游泳俱樂部)。</span><span class="sxs-lookup"><span data-stu-id="f6e61-150">In this exercise, you deploy an update to all the tenant databases to add two additional venue types: *Motorcycle Racing* and *Swimming Club*.</span></span> <span data-ttu-id="f6e61-151">這些場地類型會對應至您在租用戶活動應用程式中看到的背景影像。</span><span class="sxs-lookup"><span data-stu-id="f6e61-151">These venue types correspond to the background image you see in the tenant events app.</span></span>

<span data-ttu-id="f6e61-152">按一下 [Venue Type (場地類型)] 下拉式功能表，然後確認只有 10 個場地類型選項可用，特別是清單中不包含 [Motorcycle Racing (機車賽)] 和 [Swimming Club (游泳俱樂部)]。</span><span class="sxs-lookup"><span data-stu-id="f6e61-152">Click the Venue Type drop down menu and validate that only 10 venue type options are available, and specifically that ‘Motorcycle Racing’ and ‘Swimming Club’ are not included in the list.</span></span>

<span data-ttu-id="f6e61-153">現在讓我們建立作業以更新所有租用戶資料庫中的 *VenueTypes* 資料表，並新增新的場地類型。</span><span class="sxs-lookup"><span data-stu-id="f6e61-153">Now let’s create a job to update the *VenueTypes* table in all the tenant databases and add the new venue types.</span></span>

<span data-ttu-id="f6e61-154">為了建立新的作業，我們會使用作業帳戶建立時，在 jobaccount 資料庫中建立的一組作業系統預存程序。</span><span class="sxs-lookup"><span data-stu-id="f6e61-154">To create a new job, we use a set of jobs system stored procedures created in the jobaccount database when the job account was created.</span></span>

1. <span data-ttu-id="f6e61-155">開啟 SSMS 並連線到類別目錄伺服器：catalog-\<user\>.database.windows.net server</span><span class="sxs-lookup"><span data-stu-id="f6e61-155">Open SSMS and connect to the catalog server: catalog-\<user\>.database.windows.net server</span></span>
1. <span data-ttu-id="f6e61-156">另外也連線到租用戶伺服器：tenants1-\<user\>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f6e61-156">Also connect to the tenant server: tenants1-\<user\>.database.windows.net</span></span>
1. <span data-ttu-id="f6e61-157">瀏覽至 *tenants1* 伺服器上的 *contosoconcerthall* 資料庫，並查詢 *VenueTypes* 資料表以確認 *Motorcycle Racing* (機車賽) 和 *Swimming Club* (游泳俱樂部) **不存在於**結果清單中。</span><span class="sxs-lookup"><span data-stu-id="f6e61-157">Browse to the *contosoconcerthall* database on the *tenants1* server and query the *VenueTypes* table to confirm that *Motorcycle Racing* and *Swimming Club* **are not** in the results list.</span></span>
1. <span data-ttu-id="f6e61-158">開啟檔案 …\\Learning Modules\\Schema Management\\DeployReferenceData.sql</span><span class="sxs-lookup"><span data-stu-id="f6e61-158">Open the file …\\Learning Modules\\Schema Management\\DeployReferenceData.sql</span></span>
1. <span data-ttu-id="f6e61-159">修改陳述式：SET @wtpUser = &lt;user&gt;，並使用您在部署 Wingtip 應用程式時使用的 User 值來取代</span><span class="sxs-lookup"><span data-stu-id="f6e61-159">Modify the statement: SET @wtpUser = &lt;user&gt; and substitute the User value used when you deployed the Wingtip app</span></span>
1. <span data-ttu-id="f6e61-160">確定您已連線到 jobaccount 資料庫，然後按 **F5** 以執行指令碼</span><span class="sxs-lookup"><span data-stu-id="f6e61-160">Ensure you are connected to the jobaccount database and press **F5** to run the script</span></span>

* <span data-ttu-id="f6e61-161">**sp\_add\_target\_group** 會建立目標群組名稱 DemoServerGroup，我們現在需要新增目標成員。</span><span class="sxs-lookup"><span data-stu-id="f6e61-161">**sp\_add\_target\_group** creates the target group name DemoServerGroup, now we need to add target members.</span></span>
* <span data-ttu-id="f6e61-162">**sp\_add\_target\_group\_member** 會新增「伺服器」目標成員類型，這會將該伺服器 (請注意，這是包含租用戶資料庫的 tenants1-&lt;User&gt; 伺服器) 中的所有資料庫視為作業執行時應包含在作業中的項目，其次是新增「資料庫」目標成員類型，具體而言是「範本」資料庫 (basetenantdb)，它位於 catalog-&lt;User&gt; 伺服器上，最後，另一個「資料庫」目標群組成員類型會包括稍後教學課程要使用的 adhocanalytics 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6e61-162">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the tenants1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job, the second is adding a *database* target member type, specifically the ‘golden’ database (basetenantdb) that resides on catalog-&lt;User&gt; server, and lastly another *database* target group member type to include the adhocanalytics database that is used in a later tutorial.</span></span>
* <span data-ttu-id="f6e61-163">**sp\_add\_job** 會建立稱為「參考資料部署」的作業</span><span class="sxs-lookup"><span data-stu-id="f6e61-163">**sp\_add\_job** creates a job called “Reference Data Deployment”</span></span>
* <span data-ttu-id="f6e61-164">**sp\_add\_jobstep** 會建立作業步驟，包含更新參考資料表 VenueTypes 的 T-SQL 命令文字</span><span class="sxs-lookup"><span data-stu-id="f6e61-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to update the reference table, VenueTypes</span></span>
* <span data-ttu-id="f6e61-165">指令碼中的其餘檢視會顯示物件是否存在，以及監視作業執行。</span><span class="sxs-lookup"><span data-stu-id="f6e61-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="f6e61-166">使用這些查詢來檢閱 **lifecycle** 資料行中的值，以判斷作業在所有租用戶資料庫上，以及包含參考資料表的兩個額外資料庫上成功完成的時間。</span><span class="sxs-lookup"><span data-stu-id="f6e61-166">Use these queries to review the status value in the **lifecycle** column to determine when the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

1. <span data-ttu-id="f6e61-167">在 SSMS 中，瀏覽至 *tenants1* 伺服器上的 *contosoconcerthall* 資料庫，並查詢 *VenueTypes* 資料表以確認 *Motorcycle Racing* (機車賽) 和 *Swimming Club* (游泳俱樂部) 現在**存在於**結果清單中。</span><span class="sxs-lookup"><span data-stu-id="f6e61-167">In SSMS, browse to the *contosoconcerthall* database on the *tenants1* server and query the *VenueTypes* table to confirm that *Motorcycle Racing* and *Swimming Club* **are** now in the results list.</span></span>


## <a name="create-a-job-to-manage-the-reference-table-index"></a><span data-ttu-id="f6e61-168">建立作業以管理參考資料表索引</span><span class="sxs-lookup"><span data-stu-id="f6e61-168">Create a job to manage the reference table index</span></span>

<span data-ttu-id="f6e61-169">類似於前一個練習，這個練習會建立作業以針對參考資料表的主索引鍵重建索引，這是將大量資料載入資料表後，系統管理員可能會執行的常見資料庫管理作業。</span><span class="sxs-lookup"><span data-stu-id="f6e61-169">Similar to the previous exercise, this exercise creates a job to rebuild the index on the reference table primary key, a typical database management operation an administrator might perform after a large data load into a table.</span></span>

<span data-ttu-id="f6e61-170">使用相同的作業「系統」預存程序建立作業。</span><span class="sxs-lookup"><span data-stu-id="f6e61-170">Create a job using the same jobs 'system' stored procedures.</span></span>

1. <span data-ttu-id="f6e61-171">開啟 SSMS 並連線到 catalog-&lt;User&gt;.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="f6e61-171">Open SSMS and connect to the catalog-&lt;User&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="f6e61-172">開啟檔案 …\\Learning Modules\\Schema Management\\OnlineReindex.sql</span><span class="sxs-lookup"><span data-stu-id="f6e61-172">Open the file …\\Learning Modules\\Schema Management\\OnlineReindex.sql</span></span>
1. <span data-ttu-id="f6e61-173">按一下滑鼠右鍵並選取 [連線]，然後連線到 catalog-&lt;User&gt;.database.windows.net 伺服器 (如果您尚未連線)</span><span class="sxs-lookup"><span data-stu-id="f6e61-173">Right click, select Connection, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="f6e61-174">確定您已連線到 jobaccount 資料庫，然後按 F5 以執行指令碼</span><span class="sxs-lookup"><span data-stu-id="f6e61-174">Ensure you are connected to the jobaccount database and press F5 to run the script</span></span>

* <span data-ttu-id="f6e61-175">sp\_add\_job 會建立稱為「線上 PK 索引重建\_\_VenueTyp\_\_265E44FD7FD4C885」的新作業</span><span class="sxs-lookup"><span data-stu-id="f6e61-175">sp\_add\_job creates a new job called “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”</span></span>
* <span data-ttu-id="f6e61-176">sp\_add\_jobstep 會建立作業步驟，其中包含要更新索引的 T-SQL 命令文字</span><span class="sxs-lookup"><span data-stu-id="f6e61-176">sp\_add\_jobstep creates the job step containing T-SQL command text to update the index</span></span>




## <a name="next-steps"></a><span data-ttu-id="f6e61-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6e61-177">Next steps</span></span>

<span data-ttu-id="f6e61-178">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="f6e61-178">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="f6e61-179">建立作業帳戶以跨多個租用戶查詢</span><span class="sxs-lookup"><span data-stu-id="f6e61-179">Create a job account to query across multiple tenants</span></span>
> * <span data-ttu-id="f6e61-180">更新所有租用戶資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="f6e61-180">Update data in all tenant databases</span></span>
> * <span data-ttu-id="f6e61-181">針對所有租用戶資料庫中的資料表建立索引</span><span class="sxs-lookup"><span data-stu-id="f6e61-181">Create an index on a table in all tenant databases</span></span>

[<span data-ttu-id="f6e61-182">臨機操作分析教學課程</span><span class="sxs-lookup"><span data-stu-id="f6e61-182">Ad-hoc analytics tutorial</span></span>](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a><span data-ttu-id="f6e61-183">其他資源</span><span class="sxs-lookup"><span data-stu-id="f6e61-183">Additional resources</span></span>

* <span data-ttu-id="f6e61-184">其他[以 Wingtip SaaS 應用程式部署為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="f6e61-184">[Additional tutorials that build upon the Wingtip SaaS application deployment](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="f6e61-185">管理相應放大的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="f6e61-185">Managing scaled-out cloud databases</span></span>](sql-database-elastic-jobs-overview.md)
* [<span data-ttu-id="f6e61-186">建立和管理相應放大的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="f6e61-186">Create and manage scaled-out cloud databases</span></span>](sql-database-elastic-jobs-create-and-manage.md)
