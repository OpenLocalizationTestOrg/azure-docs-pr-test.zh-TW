---
title: "aaaIntro Wingtip SaaS-Azure SQL Database 多租用戶應用程式 |Microsoft 文件"
description: "使用範例多租用戶應用程式使用 Azure SQL Database，hello Wingtip SaaS 應用程式，了解"
keywords: SQL Database Azure
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a><span data-ttu-id="bf732-104">簡介 toohello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf732-104">Introduction toohello Wingtip SaaS application</span></span>

<span data-ttu-id="bf732-105">hello *Wingtip SaaS*應用程式是範例多租用戶應用程式，示範 hello 的 SQL Database 的獨特好處。</span><span class="sxs-lookup"><span data-stu-id="bf732-105">hello *Wingtip SaaS* application is a sample multi-tenant app, that demonstrates hello unique advantages of SQL Database.</span></span> <span data-ttu-id="bf732-106">hello 應用程式會使用資料庫的各個租用戶，SaaS 應用程式模式 tooservice 多個租用戶。</span><span class="sxs-lookup"><span data-stu-id="bf732-106">hello app uses a database-per-tenant, SaaS application pattern, tooservice multiple tenants.</span></span> <span data-ttu-id="bf732-107">hello 應用程式是 Azure SQL Database 的設計的 tooshowcase 功能可讓 SaaS 案例，包括數個 SaaS 設計和管理模式。</span><span class="sxs-lookup"><span data-stu-id="bf732-107">hello app is designed tooshowcase features of Azure SQL Database that enable SaaS scenarios, including several SaaS design and management patterns.</span></span> <span data-ttu-id="bf732-108">tooquickly 啟動和執行，請在五分鐘內部署 hello Wingtip SaaS 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="bf732-108">tooquickly get up and running, hello Wingtip SaaS app deploys in less than five minutes!</span></span>

<span data-ttu-id="bf732-109">應用程式來源的程式碼和管理指令碼位於 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="bf732-109">Application source code and management scripts are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="bf732-110">toorun hello 指令碼，[下載 hello 學習模組資料夾](#download-and-unblock-the-wingtip-saas-scripts)tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="bf732-110">toorun hello scripts, [download hello Learning Modules folder](#download-and-unblock-the-wingtip-saas-scripts) tooyour local computer.</span></span>

## <a name="sql-database-wingtip-saas-tutorials"></a><span data-ttu-id="bf732-111">SQL Database Wingtip SaaS 教學課程</span><span class="sxs-lookup"><span data-stu-id="bf732-111">SQL Database Wingtip SaaS tutorials</span></span>

<span data-ttu-id="bf732-112">部署之後 hello 應用程式，請瀏覽 hello 遵循 hello 初始部署為基礎的教學課程。</span><span class="sxs-lookup"><span data-stu-id="bf732-112">After deploying hello app, explore hello following tutorials that build upon hello initial deployment.</span></span> <span data-ttu-id="bf732-113">這些教學課程會探索常見 SaaS 模式，其利用 SQL Database、SQL 資料倉儲和其他 Azure 服務的內建功能。</span><span class="sxs-lookup"><span data-stu-id="bf732-113">These tutorials explore common SaaS patterns that take advantage of built-in features of SQL Database, SQL Data Warehouse, and other Azure services.</span></span> <span data-ttu-id="bf732-114">教學課程包含詳細的說明，大幅簡化了解，以 PowerShell 指令碼，並實作 hello 在應用程式中的相同 SaaS 管理模式。</span><span class="sxs-lookup"><span data-stu-id="bf732-114">Tutorials include PowerShell scripts, with detailed explanations that greatly simplify understanding, and implementing hello same SaaS management patterns in your applications.</span></span>


| <span data-ttu-id="bf732-115">教學課程</span><span class="sxs-lookup"><span data-stu-id="bf732-115">Tutorial</span></span> | <span data-ttu-id="bf732-116">說明</span><span class="sxs-lookup"><span data-stu-id="bf732-116">Description</span></span> |
|:--|:--|
|[<span data-ttu-id="bf732-117">部署及瀏覽 hello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf732-117">Deploy and explore hello Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)| <span data-ttu-id="bf732-118">**從這裡開始！**</span><span class="sxs-lookup"><span data-stu-id="bf732-118">**START HERE!**</span></span> <span data-ttu-id="bf732-119">部署及瀏覽 hello Wingtip SaaS 應用程式 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf732-119">Deploy and explore hello Wingtip SaaS application tooyour Azure subscription.</span></span> |
|[<span data-ttu-id="bf732-120">佈建租用戶並在目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="bf732-120">Provision and catalog tenants</span></span>](sql-database-saas-tutorial-provision-and-catalog.md)| <span data-ttu-id="bf732-121">Hello 應用程式如何連接 tootenants 使用類別目錄資料庫，了解，以及如何 hello 目錄對應的租用戶 tootheir 資料。</span><span class="sxs-lookup"><span data-stu-id="bf732-121">Learn how hello application connects tootenants using a catalog database, and how hello catalog maps tenants tootheir data.</span></span> |
|[<span data-ttu-id="bf732-122">監視及管理效能</span><span class="sxs-lookup"><span data-stu-id="bf732-122">Monitor and manage performance</span></span>](sql-database-saas-tutorial-performance-monitoring.md)| <span data-ttu-id="bf732-123">了解如何 toouse 監視功能的 SQL Database 和如何 tooset 警示時超出效能臨界值。</span><span class="sxs-lookup"><span data-stu-id="bf732-123">Learn how toouse monitoring features of SQL Database, and how tooset alerts when performance thresholds are exceeded.</span></span> |
|[<span data-ttu-id="bf732-124">透過 Log Analytics (OMS) 監視</span><span class="sxs-lookup"><span data-stu-id="bf732-124">Monitor with Log Analytics (OMS)</span></span>](sql-database-saas-tutorial-log-analytics.md) | <span data-ttu-id="bf732-125">了解如何使用[記錄分析](../log-analytics/log-analytics-overview.md)toomonitor 大量的資源，跨多個集區。</span><span class="sxs-lookup"><span data-stu-id="bf732-125">Learn about using [Log Analytics](../log-analytics/log-analytics-overview.md) toomonitor large amounts of resources, across multiple pools.</span></span> |
|[<span data-ttu-id="bf732-126">還原單一租用戶</span><span class="sxs-lookup"><span data-stu-id="bf732-126">Restore a single tenant</span></span>](sql-database-saas-tutorial-restore-single-tenant.md)| <span data-ttu-id="bf732-127">了解如何 toorestore 租用戶資料庫 tooa 先前時間點。</span><span class="sxs-lookup"><span data-stu-id="bf732-127">Learn how toorestore a tenant database tooa prior point in time.</span></span> <span data-ttu-id="bf732-128">步驟 toorestore tooa 平行資料庫，讓 hello 現有租用戶資料庫上線，也會包含。</span><span class="sxs-lookup"><span data-stu-id="bf732-128">Steps toorestore tooa parallel database, leaving hello existing tenant database online, are also included.</span></span> |
|[<span data-ttu-id="bf732-129">管理租用結構描述</span><span class="sxs-lookup"><span data-stu-id="bf732-129">Manage tenant schema</span></span>](sql-database-saas-tutorial-schema-management.md)| <span data-ttu-id="bf732-130">了解如何 tooupdate 結構描述，並更新參考資料，跨所有 Wingtip SaaS 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bf732-130">Learn how tooupdate schema, and update reference data, across all Wingtip SaaS tenants.</span></span> |
|[<span data-ttu-id="bf732-131">執行臨機操作分析</span><span class="sxs-lookup"><span data-stu-id="bf732-131">Run ad-hoc analytics</span></span>](sql-database-saas-tutorial-adhoc-analytics.md) | <span data-ttu-id="bf732-132">建立臨機操作分析資料庫並對所有租用戶執行即時分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="bf732-132">Create an ad-hoc analytics database and run real-time distributed queries across all tenants.</span></span>  |
|[<span data-ttu-id="bf732-133">執行租用戶分析</span><span class="sxs-lookup"><span data-stu-id="bf732-133">Run tenant analytics</span></span>](sql-database-saas-tutorial-tenant-analytics.md) | <span data-ttu-id="bf732-134">將租用戶資料擷取到分析資料庫或資料倉儲中，以便執行離線分析查詢。</span><span class="sxs-lookup"><span data-stu-id="bf732-134">Extract tenant data into an analytics database or data warehouse for running offline analytic queries.</span></span> |



## <a name="application-architecture"></a><span data-ttu-id="bf732-135">應用程式架構</span><span class="sxs-lookup"><span data-stu-id="bf732-135">Application architecture</span></span>

<span data-ttu-id="bf732-136">hello Wingtip SaaS 應用程式使用 hello 資料庫每個租用戶模型，並使用 SQL 彈性集區 toomaximize 效率。</span><span class="sxs-lookup"><span data-stu-id="bf732-136">hello Wingtip SaaS app uses hello database-per-tenant model, and uses SQL elastic pools toomaximize efficiency.</span></span> <span data-ttu-id="bf732-137">佈建及租用戶 tootheir 資料對應，目錄會使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="bf732-137">For provisioning and mapping tenants tootheir data, a catalog database is used.</span></span> <span data-ttu-id="bf732-138">hello 核心 Wingtip SaaS 應用程式，使用具有三個範例租用戶，再加上 hello 類別目錄資料庫集區。</span><span class="sxs-lookup"><span data-stu-id="bf732-138">hello core Wingtip SaaS application, uses a pool with three sample tenants, plus hello catalog database.</span></span> <span data-ttu-id="bf732-139">完成許多 hello Wingtip SaaS 教學課程會導致附加元件 toohello 初始部署後，藉由引進分析資料庫，跨資料庫結構描述管理等等。</span><span class="sxs-lookup"><span data-stu-id="bf732-139">Completing many of hello Wingtip SaaS tutorials result in add-ons toohello intial deployment, by introducing analytic databases, cross-database schema management, etc.</span></span>


![Wingtip SaaS 架構](media/sql-database-wtp-overview/app-architecture.png)


<span data-ttu-id="bf732-141">時經過 hello 教學課程和使用 hello 應用程式，它會是重要 toofocus hello SaaS 模式會彼此 toohello 資料層。</span><span class="sxs-lookup"><span data-stu-id="bf732-141">While going through hello tutorials and working with hello app, it is important toofocus on hello SaaS patterns as they relate toohello data tier.</span></span> <span data-ttu-id="bf732-142">換句話說，著重於 hello 資料層，而不要超過分析 hello 應用程式本身。</span><span class="sxs-lookup"><span data-stu-id="bf732-142">In other words, focus on hello data tier, and don't over analyze hello app itself.</span></span> <span data-ttu-id="bf732-143">了解這些 SaaS 模式 hello 實作是金鑰 tooimplementing 這些模式，在應用程式中的，同時考慮到特定的業務需求的任何必要的修改。</span><span class="sxs-lookup"><span data-stu-id="bf732-143">Understanding hello implementation of these SaaS patterns is key tooimplementing these patterns in your applications, while considering any necessary modifications for your specific business requirements.</span></span>

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a><span data-ttu-id="bf732-144">下載並解除封鎖 hello Wingtip SaaS 指令碼</span><span class="sxs-lookup"><span data-stu-id="bf732-144">Download and unblock hello Wingtip SaaS scripts</span></span>

<span data-ttu-id="bf732-145">從外部來源下載 zip 檔案並進行解壓縮時，Windows 可能會封鎖可執行的內容 (指令碼、dll)。</span><span class="sxs-lookup"><span data-stu-id="bf732-145">Executable contents (scripts, dlls) may be blocked by Windows when zip files are downloaded from an external source and extracted.</span></span> <span data-ttu-id="bf732-146">從 zip 檔案解壓縮 hello 指令碼時***步驟 hello 下方 toounblock hello.zip 檔案，然後才能擷取***。</span><span class="sxs-lookup"><span data-stu-id="bf732-146">When extracting hello scripts from a zip file, ***follow hello steps below toounblock hello .zip file before extracting***.</span></span> <span data-ttu-id="bf732-147">這可確保會允許 toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bf732-147">This ensures hello scripts are allowed toorun.</span></span>

1. <span data-ttu-id="bf732-148">瀏覽過[hello Wingtip SaaS github 儲存機制](https://github.com/Microsoft/WingtipSaaS)。</span><span class="sxs-lookup"><span data-stu-id="bf732-148">Browse too[hello Wingtip SaaS github repo](https://github.com/Microsoft/WingtipSaaS).</span></span>
1. <span data-ttu-id="bf732-149">按一下 [複製或下載]。</span><span class="sxs-lookup"><span data-stu-id="bf732-149">Click **Clone or download**.</span></span>
1. <span data-ttu-id="bf732-150">按一下**Download ZIP**儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="bf732-150">Click **Download ZIP** and save hello file.</span></span>
1. <span data-ttu-id="bf732-151">以滑鼠右鍵按一下 hello **WingtipSaaS master.zip**檔案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="bf732-151">Right-click hello **WingtipSaaS-master.zip** file, and select **Properties**.</span></span>
1. <span data-ttu-id="bf732-152">在 hello**一般**索引標籤上，選取**解除封鎖**。</span><span class="sxs-lookup"><span data-stu-id="bf732-152">On hello **General** tab, select **Unblock**.</span></span>
1. <span data-ttu-id="bf732-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bf732-153">Click **OK**.</span></span>
1. <span data-ttu-id="bf732-154">Hello 檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="bf732-154">Extract hello files.</span></span>

<span data-ttu-id="bf732-155">指令碼位於 hello *...\\WingtipSaaS master\\學習模組*資料夾。</span><span class="sxs-lookup"><span data-stu-id="bf732-155">Scripts are located in hello *..\\WingtipSaaS-master\\Learning Modules* folder.</span></span>


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a><span data-ttu-id="bf732-156">使用 hello Wingtip SaaS PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="bf732-156">Working with hello Wingtip SaaS PowerShell Scripts</span></span>

<span data-ttu-id="bf732-157">tooget hello 最 hello 範例超出您需要 toodive hello 提供指令碼。</span><span class="sxs-lookup"><span data-stu-id="bf732-157">tooget hello most out of hello sample you need toodive into hello provided scripts.</span></span> <span data-ttu-id="bf732-158">使用中斷點和逐步執行 hello 指令碼，檢查 hello hello SaaS 模式不同的實作方式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf732-158">Use breakpoints and step through hello scripts, examining hello details of how hello different SaaS patterns are implemented.</span></span> <span data-ttu-id="bf732-159">tooeasily 逐步執行 hello 提供指令碼和模組 hello 最好了解，我們建議您使用 hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。</span><span class="sxs-lookup"><span data-stu-id="bf732-159">tooeasily step through hello provided scripts and modules for hello best understanding, we recommend using hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span>

### <a name="update-hello-configuration-file-for-your-deployment"></a><span data-ttu-id="bf732-160">更新您的部署的 hello 設定檔</span><span class="sxs-lookup"><span data-stu-id="bf732-160">Update hello configuration file for your deployment</span></span>

<span data-ttu-id="bf732-161">編輯 hello **UserConfig.psm1** hello 資源群組和使用者值與您在部署期間設定的檔案：</span><span class="sxs-lookup"><span data-stu-id="bf732-161">Edit hello **UserConfig.psm1** file with hello resource group and user value that you set during deployment:</span></span>

1. <span data-ttu-id="bf732-162">開啟 hello *PowerShell ISE*並載入...\\學習模組\\*UserConfig.psm1*</span><span class="sxs-lookup"><span data-stu-id="bf732-162">Open hello *PowerShell ISE* and load ...\\Learning Modules\\*UserConfig.psm1*</span></span> 
1. <span data-ttu-id="bf732-163">更新*ResourceGroupName*和*名稱*（位於行 10 和 11 只） 部署的 hello 特定值。</span><span class="sxs-lookup"><span data-stu-id="bf732-163">Update *ResourceGroupName* and *Name* with hello specific values for your deployment (on lines 10 and 11 only).</span></span>
1. <span data-ttu-id="bf732-164">儲存 hello 變更 ！</span><span class="sxs-lookup"><span data-stu-id="bf732-164">Save hello changes!</span></span>

<span data-ttu-id="bf732-165">這裡設定這些值只可防止您在每個指令碼中具有 tooupdate 這些部署專屬的值。</span><span class="sxs-lookup"><span data-stu-id="bf732-165">Setting these values here simply keeps you from having tooupdate these deployment-specific values in every script.</span></span>

### <a name="execute-scripts-by-pressing-f5"></a><span data-ttu-id="bf732-166">按 F5 執行指令碼</span><span class="sxs-lookup"><span data-stu-id="bf732-166">Execute Scripts by pressing F5</span></span>

<span data-ttu-id="bf732-167">使用數個指令碼*$PSScriptRoot* toonavigate 資料夾和*$PSScriptRoot*藉由按下執行指令碼時，才會評估**F5**。</span><span class="sxs-lookup"><span data-stu-id="bf732-167">Several scripts use *$PSScriptRoot* toonavigate folders, and *$PSScriptRoot* is only evaluated when scripts are executed by pressing **F5**.</span></span>  <span data-ttu-id="bf732-168">醒目提示並執行選取項目 (**F8**) 可能會導致錯誤，因此請在執行指令碼時按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="bf732-168">Highlighting and running a selection (**F8**) can result in errors, so press **F5** when running scripts.</span></span>

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a><span data-ttu-id="bf732-169">逐步執行 hello 指令碼 tooexamine hello 實作</span><span class="sxs-lookup"><span data-stu-id="bf732-169">Step through hello scripts tooexamine hello implementation</span></span>

<span data-ttu-id="bf732-170">hello 最佳方式 toounderstand hello 指令碼會透過逐步執行它們 toosee 它們執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bf732-170">hello best way toounderstand hello scripts is by stepping through them toosee what they do.</span></span> <span data-ttu-id="bf732-171">簽出 hello 包含**示範-**呈現輕鬆 toofollow 高階工作流程的指令碼。</span><span class="sxs-lookup"><span data-stu-id="bf732-171">Check out hello included **Demo-** scripts that present an easy toofollow high-level workflow.</span></span> <span data-ttu-id="bf732-172">hello**示範-**指令碼顯示 hello 步驟需要的 tooaccomplish 每項工作，因此設定中斷點，而且會鑽研更深入 hello 個別呼叫 toosee 實作細節 hello SaaS 模式不同。</span><span class="sxs-lookup"><span data-stu-id="bf732-172">hello **Demo-** scripts show hello steps required tooaccomplish each task, so set breakpoints and drill deeper into hello individual calls toosee implementation details for hello different SaaS patterns.</span></span>

<span data-ttu-id="bf732-173">探索及逐步執行 PowerShell 指令碼的秘訣：</span><span class="sxs-lookup"><span data-stu-id="bf732-173">Tips for exploring and stepping through PowerShell scripts:</span></span>

* <span data-ttu-id="bf732-174">開啟**示範-** hello PowerShell ISE 中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="bf732-174">Open **Demo-** scripts in hello PowerShell ISE.</span></span>
* <span data-ttu-id="bf732-175">執行或繼續使用 **F5** (不建議使用 **F8**，因為在執行指令碼的選取項目時不會評估 $PSScriptRoot)。</span><span class="sxs-lookup"><span data-stu-id="bf732-175">Execute or continue with **F5** (using **F8** is not advised because *$PSScriptRoot* is not evaluated when running selections of a script).</span></span>
* <span data-ttu-id="bf732-176">按一下或選取一行，然後按 **F9** 放置中斷點。</span><span class="sxs-lookup"><span data-stu-id="bf732-176">Place breakpoints by clicking or selecting a line and pressing **F9**.</span></span>
* <span data-ttu-id="bf732-177">使用 **F10** 不進入函式或指令碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="bf732-177">Step over a function or script call using **F10**.</span></span>
* <span data-ttu-id="bf732-178">使用 **F11** 逐步執行函式或指令碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="bf732-178">Step into a function or script call using **F11**.</span></span>
* <span data-ttu-id="bf732-179">跳離 hello 目前函式或指令碼呼叫使用**Shift + F11**。</span><span class="sxs-lookup"><span data-stu-id="bf732-179">Step out of hello current function or script call using **Shift + F11**.</span></span>


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a><span data-ttu-id="bf732-180">使用 SSMS 瀏覽資料庫結構描述並執行 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="bf732-180">Explore database schema and execute SQL queries using SSMS</span></span>

<span data-ttu-id="bf732-181">使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect 並瀏覽 hello 應用程式伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="bf732-181">Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect and browse hello application servers and databases.</span></span>

<span data-ttu-id="bf732-182">hello 部署一開始會有兩個 SQL Database 伺服器 tooconnect 太-hello *tenants1-&lt;使用者&gt;*伺服器和 hello*目錄-&lt;使用者&gt;*伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf732-182">hello deployment initially has two SQL Database servers tooconnect too- hello *tenants1-&lt;User&gt;* server, and hello *catalog-&lt;User&gt;* server.</span></span> <span data-ttu-id="bf732-183">tooensure 成功示範連接，這兩部伺服器具有[防火牆規則](sql-database-firewall-configure.md)允許透過所有 Ip。</span><span class="sxs-lookup"><span data-stu-id="bf732-183">tooensure a successful demo connection, both servers have a [firewall rule](sql-database-firewall-configure.md) allowing all IPs through.</span></span>


1. <span data-ttu-id="bf732-184">開啟*SSMS*並連接 toohello *tenants1-&lt;使用者&gt;。.database.windows.net*伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf732-184">Open *SSMS* and connect toohello *tenants1-&lt;User&gt;.database.windows.net* server.</span></span>
1. <span data-ttu-id="bf732-185">按一下 [連線] > **[資料庫引擎...]**：</span><span class="sxs-lookup"><span data-stu-id="bf732-185">Click **Connect** > **Database Engine...**:</span></span>

   ![目錄伺服器](media/sql-database-wtp-overview/connect.png)

1. <span data-ttu-id="bf732-187">示範認證︰ 登入= developer、密碼 = P@ssword1</span><span class="sxs-lookup"><span data-stu-id="bf732-187">Demo credentials are: Login = *developer*, Password = *P@ssword1*</span></span>

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. <span data-ttu-id="bf732-189">重複步驟 2-3，並連接 toohello*目錄-&lt;使用者&gt;。.database.windows.net*伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf732-189">Repeat steps 2-3 and connect toohello *catalog-&lt;User&gt;.database.windows.net* server.</span></span>

<span data-ttu-id="bf732-190">成功連線之後，您會看到這兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf732-190">After successfully connecting you should see both servers.</span></span> <span data-ttu-id="bf732-191">您的資料庫清單可能會有所不同，您已佈建的 hello 租用戶：</span><span class="sxs-lookup"><span data-stu-id="bf732-191">Your list of databases might be different, depending on hello tenants you've provisioned:</span></span>

![物件總管](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a><span data-ttu-id="bf732-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf732-193">Next steps</span></span>

[<span data-ttu-id="bf732-194">部署 hello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf732-194">Deploy hello Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)
