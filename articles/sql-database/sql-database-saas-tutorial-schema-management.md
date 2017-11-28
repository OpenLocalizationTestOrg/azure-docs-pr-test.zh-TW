---
title: "aaaManage Azure SQL Database 的結構描述中的多租用戶應用程式 |Microsoft 文件"
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
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a><span data-ttu-id="450cd-104">多個租用戶 hello Wingtip SaaS 應用程式中管理結構描述</span><span class="sxs-lookup"><span data-stu-id="450cd-104">Manage schema for multiple tenants in hello Wingtip SaaS application</span></span>

<span data-ttu-id="450cd-105">hello[第一個 Wingtip SaaS 教學課程](sql-database-saas-tutorial.md)顯示 hello 應用程式如何佈建租用戶資料庫和註冊 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="450cd-105">hello [first Wingtip SaaS tutorial](sql-database-saas-tutorial.md) shows how hello app can provision a tenant database and register it in hello catalog.</span></span> <span data-ttu-id="450cd-106">就像任何應用程式，hello Wingtip SaaS 應用程式將持續改進，經過一段時間，與有時候會需要變更 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="450cd-106">Like any application, hello Wingtip SaaS app will evolve over time, and at times will require changes toohello database.</span></span> <span data-ttu-id="450cd-107">變更可能包括新增或變更結構描述、 新增或變更的參考資料，以及例行的資料庫維護工作 tooensure 最佳應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="450cd-107">Changes may include new or changed schema, new or changed reference data, and routine database maintenance tasks tooensure optimal app performance.</span></span> <span data-ttu-id="450cd-108">與 SaaS 應用程式，這些變更需要 toobe 跨租用戶資料庫可能會大量以及部署中協調的方式。</span><span class="sxs-lookup"><span data-stu-id="450cd-108">With a SaaS application, these changes need toobe deployed in a coordinated manner across a potentially massive fleet of tenant databases.</span></span> <span data-ttu-id="450cd-109">這些變更 toobe 未來租用戶資料庫、 需要 toobe 併入 hello 佈建程序。</span><span class="sxs-lookup"><span data-stu-id="450cd-109">For these changes toobe in future tenant databases, they need toobe incorporated into hello provisioning process.</span></span>

<span data-ttu-id="450cd-110">本教學課程會探討兩種案例-將參考資料更新部署的所有租用戶，並 retuning hello 上的索引，資料表包含 hello 參考資料。</span><span class="sxs-lookup"><span data-stu-id="450cd-110">This tutorial explores two scenarios - deploying reference data updates for all tenants, and retuning an index on hello table containing hello reference data.</span></span> <span data-ttu-id="450cd-111">hello[彈性作業](sql-database-elastic-jobs-overview.md)功能是使用的 tooexecute 這些作業的所有租用戶和 hello*黃金*新的資料庫做為範本使用的租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="450cd-111">hello [Elastic jobs](sql-database-elastic-jobs-overview.md) feature is used tooexecute these operations across all tenants, and hello *golden* tenant database that is used as a template for new databases.</span></span>

<span data-ttu-id="450cd-112">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="450cd-112">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="450cd-113">建立作業帳戶</span><span class="sxs-lookup"><span data-stu-id="450cd-113">Create a job account</span></span>
> * <span data-ttu-id="450cd-114">跨多個租用戶進行查詢</span><span class="sxs-lookup"><span data-stu-id="450cd-114">Query across multiple tenants</span></span>
> * <span data-ttu-id="450cd-115">更新所有租用戶資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="450cd-115">Update data in all tenant databases</span></span>
> * <span data-ttu-id="450cd-116">針對所有租用戶資料庫中的資料表建立索引</span><span class="sxs-lookup"><span data-stu-id="450cd-116">Create an index on a table in all tenant databases</span></span>


<span data-ttu-id="450cd-117">toocomplete 符合本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="450cd-117">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="450cd-118">hello Wingtip SaaS 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="450cd-118">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="450cd-119">toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="450cd-119">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="450cd-120">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="450cd-120">Azure PowerShell is installed.</span></span> <span data-ttu-id="450cd-121">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="450cd-121">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="450cd-122">已安裝最新版本的 SQL Server Management Studio (SSMS) hello。</span><span class="sxs-lookup"><span data-stu-id="450cd-122">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="450cd-123">下載並安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="450cd-123">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

<span data-ttu-id="450cd-124">*本教學課程會使用有限的預覽 （彈性資料庫工作） 所 hello SQL Database 服務功能。如果您想 toodo 本教學課程，提供您的訂用帳戶 idtooSaaSFeedback@microsoft.com主旨 = 彈性作業預覽。您會收到確認訊息，已啟用您的訂用帳戶之後,[下載及安裝最新發行前版本工作 cmdlet hello](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*</span><span class="sxs-lookup"><span data-stu-id="450cd-124">*This tutorial uses features of hello SQL Database service that are in a limited preview (Elastic Database jobs). If you wish toodo this tutorial, provide your subscription id tooSaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install hello latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>


## <a name="introduction-toosaas-schema-management-patterns"></a><span data-ttu-id="450cd-125">簡介 tooSaaS 結構描述管理模式</span><span class="sxs-lookup"><span data-stu-id="450cd-125">Introduction tooSaaS Schema Management patterns</span></span>

<span data-ttu-id="450cd-126">hello 每個資料庫的單一租用戶 SaaS 模式在許多方面與所產生，hello 資料隔離的優點，但在 hello 同時介紹 hello 維護和管理多個資料庫的額外的複雜性。</span><span class="sxs-lookup"><span data-stu-id="450cd-126">hello single tenant per database SaaS pattern benefits in many ways from hello data isolation that results, but at hello same time introduces hello additional complexity of maintaining and managing many databases.</span></span> <span data-ttu-id="450cd-127">[彈性作業](sql-database-elastic-jobs-overview.md)有助於管理工作的 hello SQL 資料層。</span><span class="sxs-lookup"><span data-stu-id="450cd-127">[Elastic Jobs](sql-database-elastic-jobs-overview.md) facilitates administration and management of hello SQL data tier.</span></span> <span data-ttu-id="450cd-128">作業 toosecurely 可讓您和可靠地執行工作 （T-SQL 指令碼） 獨立於使用者互動或輸入，對資料庫的群組。</span><span class="sxs-lookup"><span data-stu-id="450cd-128">Jobs enable you toosecurely and reliably, run tasks (T-SQL scripts) independent of user interaction or input, against a group of databases.</span></span> <span data-ttu-id="450cd-129">這個方法也有應用程式中的所有租用戶使用的 toodeploy 結構描述和一般參考資料變更。</span><span class="sxs-lookup"><span data-stu-id="450cd-129">This method can be used toodeploy schema and common reference data changes across all tenants in an application.</span></span> <span data-ttu-id="450cd-130">彈性的工作也可以使用的 toomaintain*黃金*hello 資料庫副本使用 toocreate 新租用戶，確保它必定 hello 最新的結構描述和參考資料。</span><span class="sxs-lookup"><span data-stu-id="450cd-130">Elastic Jobs can also be used toomaintain a *golden* copy of hello database used toocreate new tenants, ensuring it always has hello latest schema and reference data.</span></span>

![畫面](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a><span data-ttu-id="450cd-132">彈性作業有限預覽版</span><span class="sxs-lookup"><span data-stu-id="450cd-132">Elastic Jobs limited preview</span></span>

<span data-ttu-id="450cd-133">新版本的「彈性作業」現在是 Azure SQL Database 的整合功能 (不需要額外的服務或元件)。</span><span class="sxs-lookup"><span data-stu-id="450cd-133">There is a new version of Elastic Jobs that is now an integrated feature of Azure SQL Database (that requires no additional services or components).</span></span> <span data-ttu-id="450cd-134">這個新的「彈性作業」版本目前處於有限預覽版狀態。</span><span class="sxs-lookup"><span data-stu-id="450cd-134">This new version of Elastic Jobs is currently in limited preview.</span></span> <span data-ttu-id="450cd-135">這個有限預覽版本目前支援 PowerShell toocreate 工作帳戶和 T-SQL toocreate 及管理工作。</span><span class="sxs-lookup"><span data-stu-id="450cd-135">This limited preview currently supports PowerShell toocreate job accounts, and T-SQL toocreate and manage jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="450cd-136">*本教學課程會使用有限的預覽 （彈性資料庫工作） 所 hello SQL Database 服務功能。如果您想 toodo 本教學課程，提供您的訂用帳戶 idtooSaaSFeedback@microsoft.com主旨 = 彈性作業預覽。您會收到確認訊息，已啟用您的訂用帳戶之後,[下載及安裝最新發行前版本工作 cmdlet hello](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*</span><span class="sxs-lookup"><span data-stu-id="450cd-136">*This tutorial uses features of hello SQL Database service that are in a limited preview (Elastic Database jobs). If you wish toodo this tutorial, provide your subscription id tooSaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install hello latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="450cd-137">取得 hello Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="450cd-137">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="450cd-138">hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="450cd-138">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="450cd-139">[步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="450cd-139">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-a-job-account-database-and-new-job-account"></a><span data-ttu-id="450cd-140">建立作業帳戶資料庫和新的作業帳戶</span><span class="sxs-lookup"><span data-stu-id="450cd-140">Create a job account database and new job account</span></span>

<span data-ttu-id="450cd-141">本教學課程要求您使用 PowerShell toocreate hello 工作帳戶資料庫與工作帳戶。</span><span class="sxs-lookup"><span data-stu-id="450cd-141">This tutorial requires you use PowerShell toocreate hello job account database and job account.</span></span> <span data-ttu-id="450cd-142">如同 MSDB 和 SQL 代理程式，彈性的工作會使用 Azure SQL 資料庫 toostore 工作定義、 工作狀態和歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="450cd-142">Like MSDB and SQL Agent, Elastic Jobs uses an Azure SQL database toostore job definitions, job status, and history.</span></span> <span data-ttu-id="450cd-143">一旦建立 hello 工作帳戶之後，您可以建立並立即監視作業。</span><span class="sxs-lookup"><span data-stu-id="450cd-143">Once hello job account is created, you can create and monitor jobs immediately.</span></span>

1. <span data-ttu-id="450cd-144">開啟...\\學習模組\\結構描述管理\\*示範 SchemaManagement.ps1*在 hello **PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="450cd-144">Open …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1* in hello **PowerShell ISE**.</span></span>
1. <span data-ttu-id="450cd-145">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="450cd-145">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="450cd-146">hello*示範 SchemaManagement.ps1*指令碼呼叫 hello*部署 SchemaManagement.ps1*指令碼 toocreate *S2*資料庫名為**jobaccount** hello 類別目錄伺服器上。</span><span class="sxs-lookup"><span data-stu-id="450cd-146">hello *Demo-SchemaManagement.ps1* script calls hello *Deploy-SchemaManagement.ps1* script toocreate an *S2* database named **jobaccount** on hello catalog server.</span></span> <span data-ttu-id="450cd-147">然後，它會建立 hello 工作帳戶，做為參數 toohello 工作帳戶建立呼叫傳遞 hello jobaccount 資料庫。</span><span class="sxs-lookup"><span data-stu-id="450cd-147">It then creates hello job account, passing hello jobaccount database as a parameter toohello job account creation call.</span></span>

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a><span data-ttu-id="450cd-148">建立工作 toodeploy 新增參考資料 tooall 租用戶</span><span class="sxs-lookup"><span data-stu-id="450cd-148">Create a job toodeploy new reference data tooall tenants</span></span>

<span data-ttu-id="450cd-149">每個租用戶資料庫包含一組定義的事件裝載在法院 hello 種類的法院型別。</span><span class="sxs-lookup"><span data-stu-id="450cd-149">Each tenant database includes a set of venue types that define hello kind of events that are hosted at a venue.</span></span> <span data-ttu-id="450cd-150">在此練習中，您會部署更新 tooall hello 租用戶資料庫 tooadd 兩個其他地點類型：*機車賽*和*游泳社團*。</span><span class="sxs-lookup"><span data-stu-id="450cd-150">In this exercise, you deploy an update tooall hello tenant databases tooadd two additional venue types: *Motorcycle Racing* and *Swimming Club*.</span></span> <span data-ttu-id="450cd-151">這些地點的型別對應 toohello 看到 hello 租用戶事件應用程式中的背景影像。</span><span class="sxs-lookup"><span data-stu-id="450cd-151">These venue types correspond toohello background image you see in hello tenant events app.</span></span>

<span data-ttu-id="450cd-152">按一下 [hello 法院類型] 下拉式清單功能表上，驗證只限於 10 個地點類型選項可用，並特別該 '機車賽' 和 '游泳社團' 不包含 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="450cd-152">Click hello Venue Type drop down menu and validate that only 10 venue type options are available, and specifically that ‘Motorcycle Racing’ and ‘Swimming Club’ are not included in hello list.</span></span>

<span data-ttu-id="450cd-153">現在讓我們來建立工作 tooupdate hello *VenueTypes* hello 租用戶的所有資料庫中資料表，並新增 hello 法院類型。</span><span class="sxs-lookup"><span data-stu-id="450cd-153">Now let’s create a job tooupdate hello *VenueTypes* table in all hello tenant databases and add hello new venue types.</span></span>

<span data-ttu-id="450cd-154">toocreate 新的工作，我們會使用一組工作的系統預存程序建立 hello 工作帳戶時，在 hello jobaccount 資料庫中建立。</span><span class="sxs-lookup"><span data-stu-id="450cd-154">toocreate a new job, we use a set of jobs system stored procedures created in hello jobaccount database when hello job account was created.</span></span>

1. <span data-ttu-id="450cd-155">開啟 SSMS 並連接 toohello 類別目錄伺服器： 類別目錄-\<使用者\>。.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="450cd-155">Open SSMS and connect toohello catalog server: catalog-\<user\>.database.windows.net server</span></span>
1. <span data-ttu-id="450cd-156">也連接 toohello 租用戶伺服器： tenants1-\<使用者\>。.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="450cd-156">Also connect toohello tenant server: tenants1-\<user\>.database.windows.net</span></span>
1. <span data-ttu-id="450cd-157">瀏覽 toohello *contosoconcerthall* hello 上的資料庫*tenants1*伺服器和查詢 hello *VenueTypes*資料表 tooconfirm，*機車賽*和*游泳社團***不**hello [結果] 清單中。</span><span class="sxs-lookup"><span data-stu-id="450cd-157">Browse toohello *contosoconcerthall* database on hello *tenants1* server and query hello *VenueTypes* table tooconfirm that *Motorcycle Racing* and *Swimming Club* **are not** in hello results list.</span></span>
1. <span data-ttu-id="450cd-158">開啟 hello 檔案...\\學習模組\\結構描述管理\\DeployReferenceData.sql</span><span class="sxs-lookup"><span data-stu-id="450cd-158">Open hello file …\\Learning Modules\\Schema Management\\DeployReferenceData.sql</span></span>
1. <span data-ttu-id="450cd-159">修改 hello 陳述式： 設定@wtpUser=&lt;使用者&gt;和取代部署 hello Wingtip 應用程式時使用的 hello 使用者值</span><span class="sxs-lookup"><span data-stu-id="450cd-159">Modify hello statement: SET @wtpUser = &lt;user&gt; and substitute hello User value used when you deployed hello Wingtip app</span></span>
1. <span data-ttu-id="450cd-160">確認您是連接的 toohello jobaccount 資料庫，然後按**F5**執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="450cd-160">Ensure you are connected toohello jobaccount database and press **F5** to run hello script</span></span>

* <span data-ttu-id="450cd-161">**預存程序\_新增\_目標\_群組**建立 hello 目標群組名稱 DemoServerGroup，現在我們需要 tooadd 目標成員。</span><span class="sxs-lookup"><span data-stu-id="450cd-161">**sp\_add\_target\_group** creates hello target group name DemoServerGroup, now we need tooadd target members.</span></span>
* <span data-ttu-id="450cd-162">**預存程序\_新增\_目標\_群組\_成員**新增*伺服器*目標成員類型，認為該伺服器 （請注意這是 hello tenants1內的所有資料庫&lt;使用者&gt;包含 hello 租用戶資料庫伺服器) 在工作時間執行應該包含在 hello 工作第二個新增 hello*資料庫*目標成員類型，特別是 hello '黃金' 資料庫 (basetenantdb) 位於類別目錄-&lt;使用者&gt;伺服器，以及最後的另一個*資料庫*目標群組成員型別 tooinclude hello adhocanalytics 資料庫之後的教學課程中所使用。</span><span class="sxs-lookup"><span data-stu-id="450cd-162">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello tenants1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job, hello second is adding a *database* target member type, specifically hello ‘golden’ database (basetenantdb) that resides on catalog-&lt;User&gt; server, and lastly another *database* target group member type tooinclude hello adhocanalytics database that is used in a later tutorial.</span></span>
* <span data-ttu-id="450cd-163">**sp\_add\_job** 會建立稱為「參考資料部署」的作業</span><span class="sxs-lookup"><span data-stu-id="450cd-163">**sp\_add\_job** creates a job called “Reference Data Deployment”</span></span>
* <span data-ttu-id="450cd-164">**預存程序\_新增\_jobstep**會建立包含 T-SQL 命令文字 tooupdate hello 參考資料表中，VenueTypes hello 作業步驟</span><span class="sxs-lookup"><span data-stu-id="450cd-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooupdate hello reference table, VenueTypes</span></span>
* <span data-ttu-id="450cd-165">hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。</span><span class="sxs-lookup"><span data-stu-id="450cd-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="450cd-166">在 hello 中使用這些查詢 tooreview hello 狀態值**生命週期**時 hello 工作已順利完成所有租用戶資料庫與 hello 兩個其他資料庫包含 hello 參考資料表上的資料行 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="450cd-166">Use these queries tooreview hello status value in hello **lifecycle** column toodetermine when hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

1. <span data-ttu-id="450cd-167">在 SSMS 中，瀏覽 toohello *contosoconcerthall* hello 上的資料庫*tenants1*伺服器和查詢 hello *VenueTypes*資料表 tooconfirm，*機車賽*和*游泳社團***是**現在 hello [結果] 清單中。</span><span class="sxs-lookup"><span data-stu-id="450cd-167">In SSMS, browse toohello *contosoconcerthall* database on hello *tenants1* server and query hello *VenueTypes* table tooconfirm that *Motorcycle Racing* and *Swimming Club* **are** now in hello results list.</span></span>


## <a name="create-a-job-toomanage-hello-reference-table-index"></a><span data-ttu-id="450cd-168">建立工作 toomanage hello 參考資料表索引</span><span class="sxs-lookup"><span data-stu-id="450cd-168">Create a job toomanage hello reference table index</span></span>

<span data-ttu-id="450cd-169">類似 toohello 上一個練習中，這個練習作業 toorebuild hello 上建立索引 hello 參考資料表主索引鍵，在一般資料庫管理作業的系統管理員可能會執行大型資料載入之後，插入資料表。</span><span class="sxs-lookup"><span data-stu-id="450cd-169">Similar toohello previous exercise, this exercise creates a job toorebuild hello index on hello reference table primary key, a typical database management operation an administrator might perform after a large data load into a table.</span></span>

<span data-ttu-id="450cd-170">建立使用 hello 作業相同的作業 'system' 預存程序。</span><span class="sxs-lookup"><span data-stu-id="450cd-170">Create a job using hello same jobs 'system' stored procedures.</span></span>

1. <span data-ttu-id="450cd-171">開啟 SSMS 並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器</span><span class="sxs-lookup"><span data-stu-id="450cd-171">Open SSMS and connect toohello catalog-&lt;User&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="450cd-172">開啟 hello 檔案...\\學習模組\\結構描述管理\\OnlineReindex.sql</span><span class="sxs-lookup"><span data-stu-id="450cd-172">Open hello file …\\Learning Modules\\Schema Management\\OnlineReindex.sql</span></span>
1. <span data-ttu-id="450cd-173">以滑鼠右鍵按一下、 選取連接，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接</span><span class="sxs-lookup"><span data-stu-id="450cd-173">Right click, select Connection, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="450cd-174">請確定您已連線的 toohello jobaccount 資料庫，然後按 F5 toorun hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="450cd-174">Ensure you are connected toohello jobaccount database and press F5 toorun hello script</span></span>

* <span data-ttu-id="450cd-175">sp\_add\_job 會建立稱為「線上 PK 索引重建\_\_VenueTyp\_\_265E44FD7FD4C885」的新作業</span><span class="sxs-lookup"><span data-stu-id="450cd-175">sp\_add\_job creates a new job called “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”</span></span>
* <span data-ttu-id="450cd-176">預存程序\_新增\_作業步驟會建立包含 T-SQL 命令文字 tooupdate hello 索引的 hello 作業步驟</span><span class="sxs-lookup"><span data-stu-id="450cd-176">sp\_add\_jobstep creates hello job step containing T-SQL command text tooupdate hello index</span></span>




## <a name="next-steps"></a><span data-ttu-id="450cd-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="450cd-177">Next steps</span></span>

<span data-ttu-id="450cd-178">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="450cd-178">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="450cd-179">建立工作帳戶 tooquery 跨多個租用戶</span><span class="sxs-lookup"><span data-stu-id="450cd-179">Create a job account tooquery across multiple tenants</span></span>
> * <span data-ttu-id="450cd-180">更新所有租用戶資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="450cd-180">Update data in all tenant databases</span></span>
> * <span data-ttu-id="450cd-181">針對所有租用戶資料庫中的資料表建立索引</span><span class="sxs-lookup"><span data-stu-id="450cd-181">Create an index on a table in all tenant databases</span></span>

[<span data-ttu-id="450cd-182">臨機操作分析教學課程</span><span class="sxs-lookup"><span data-stu-id="450cd-182">Ad-hoc analytics tutorial</span></span>](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a><span data-ttu-id="450cd-183">其他資源</span><span class="sxs-lookup"><span data-stu-id="450cd-183">Additional resources</span></span>

* [<span data-ttu-id="450cd-184">Hello Wingtip SaaS 應用程式部署為基礎的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="450cd-184">Additional tutorials that build upon hello Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="450cd-185">管理相應放大的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="450cd-185">Managing scaled-out cloud databases</span></span>](sql-database-elastic-jobs-overview.md)
* [<span data-ttu-id="450cd-186">建立和管理相應放大的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="450cd-186">Create and manage scaled-out cloud databases</span></span>](sql-database-elastic-jobs-create-and-manage.md)
