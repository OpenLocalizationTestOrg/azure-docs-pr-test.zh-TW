---
title: "Wingtip SaaS - Azure SQL Database 多租用戶應用程式簡介 | Microsoft Docs"
description: "藉由使用採用 Azure SQL Database - Wingtip SaaS 應用程式的範例多租用戶應用程式來學習"
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
ms.openlocfilehash: 6d4a5df599137e95ca5458fae74b8daa565b0338
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-wingtip-saas-application"></a><span data-ttu-id="abf32-104">Wingtip SaaS 應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="abf32-104">Introduction to the Wingtip SaaS application</span></span>

<span data-ttu-id="abf32-105">Wingtip SaaS 應用程式是一個多租用戶應用程式範例，可示範 SQL Database 的獨特優點。</span><span class="sxs-lookup"><span data-stu-id="abf32-105">The *Wingtip SaaS* application is a sample multi-tenant app, that demonstrates the unique advantages of SQL Database.</span></span> <span data-ttu-id="abf32-106">此應用程式使用租用戶各有資料庫的 SaaS 應用程式模式來維護多租用戶。</span><span class="sxs-lookup"><span data-stu-id="abf32-106">The app uses a database-per-tenant, SaaS application pattern, to service multiple tenants.</span></span> <span data-ttu-id="abf32-107">此應用程式是設計成用來展示支援 SaaS 案例 (包括數個 SaaS 設計和管理模式) 的 Azure SQL Database 功能。</span><span class="sxs-lookup"><span data-stu-id="abf32-107">The app is designed to showcase features of Azure SQL Database that enable SaaS scenarios, including several SaaS design and management patterns.</span></span> <span data-ttu-id="abf32-108">為了快速啟動並執行，五分鐘內就會部署 Wingtip SaaS 應用程式！</span><span class="sxs-lookup"><span data-stu-id="abf32-108">To quickly get up and running, the Wingtip SaaS app deploys in less than five minutes!</span></span>

<span data-ttu-id="abf32-109">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) GitHub 存放庫可取得應用程式原始程式碼和管理指令碼。</span><span class="sxs-lookup"><span data-stu-id="abf32-109">Application source code and management scripts are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="abf32-110">若要執行指令碼，請[將 Learning Modules 資料夾](#download-and-unblock-the-wingtip-saas-scripts)下載到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="abf32-110">To run the scripts, [download the Learning Modules folder](#download-and-unblock-the-wingtip-saas-scripts) to your local computer.</span></span>

## <a name="sql-database-wingtip-saas-tutorials"></a><span data-ttu-id="abf32-111">SQL Database Wingtip SaaS 教學課程</span><span class="sxs-lookup"><span data-stu-id="abf32-111">SQL Database Wingtip SaaS tutorials</span></span>

<span data-ttu-id="abf32-112">部署應用程式之後，請瀏覽在初始部署時建立的下列教學課程。</span><span class="sxs-lookup"><span data-stu-id="abf32-112">After deploying the app, explore the following tutorials that build upon the initial deployment.</span></span> <span data-ttu-id="abf32-113">這些教學課程會探索常見 SaaS 模式，其利用 SQL Database、SQL 資料倉儲和其他 Azure 服務的內建功能。</span><span class="sxs-lookup"><span data-stu-id="abf32-113">These tutorials explore common SaaS patterns that take advantage of built-in features of SQL Database, SQL Data Warehouse, and other Azure services.</span></span> <span data-ttu-id="abf32-114">教學課程包含 PowerShell 指令碼，以及可大幅簡化理解的詳細說明，並且在您的應用程式中實作相同的 SaaS 管理模式。</span><span class="sxs-lookup"><span data-stu-id="abf32-114">Tutorials include PowerShell scripts, with detailed explanations that greatly simplify understanding, and implementing the same SaaS management patterns in your applications.</span></span>


| <span data-ttu-id="abf32-115">教學課程</span><span class="sxs-lookup"><span data-stu-id="abf32-115">Tutorial</span></span> | <span data-ttu-id="abf32-116">說明</span><span class="sxs-lookup"><span data-stu-id="abf32-116">Description</span></span> |
|:--|:--|
|[<span data-ttu-id="abf32-117">部署及探索 Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="abf32-117">Deploy and explore the Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)| <span data-ttu-id="abf32-118">**從這裡開始！**</span><span class="sxs-lookup"><span data-stu-id="abf32-118">**START HERE!**</span></span> <span data-ttu-id="abf32-119">將 Wingtip SaaS 應用程式部署至 Azure 訂用帳戶並加以探索。</span><span class="sxs-lookup"><span data-stu-id="abf32-119">Deploy and explore the Wingtip SaaS application to your Azure subscription.</span></span> |
|[<span data-ttu-id="abf32-120">佈建租用戶並在目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="abf32-120">Provision and catalog tenants</span></span>](sql-database-saas-tutorial-provision-and-catalog.md)| <span data-ttu-id="abf32-121">了解應用程式如何使用目錄資料庫連線至租用戶，以及目錄如何將租用戶對應至其資料。</span><span class="sxs-lookup"><span data-stu-id="abf32-121">Learn how the application connects to tenants using a catalog database, and how the catalog maps tenants to their data.</span></span> |
|[<span data-ttu-id="abf32-122">監視及管理效能</span><span class="sxs-lookup"><span data-stu-id="abf32-122">Monitor and manage performance</span></span>](sql-database-saas-tutorial-performance-monitoring.md)| <span data-ttu-id="abf32-123">了解如何使用 SQL Database 的監視功能，以及如何設定超過效能閾值時的警示。</span><span class="sxs-lookup"><span data-stu-id="abf32-123">Learn how to use monitoring features of SQL Database, and how to set alerts when performance thresholds are exceeded.</span></span> |
|[<span data-ttu-id="abf32-124">透過 Log Analytics (OMS) 監視</span><span class="sxs-lookup"><span data-stu-id="abf32-124">Monitor with Log Analytics (OMS)</span></span>](sql-database-saas-tutorial-log-analytics.md) | <span data-ttu-id="abf32-125">了解如何使用 [Log Analytics](../log-analytics/log-analytics-overview.md) 來監視跨多個集區的大量資源。</span><span class="sxs-lookup"><span data-stu-id="abf32-125">Learn about using [Log Analytics](../log-analytics/log-analytics-overview.md) to monitor large amounts of resources, across multiple pools.</span></span> |
|[<span data-ttu-id="abf32-126">還原單一租用戶</span><span class="sxs-lookup"><span data-stu-id="abf32-126">Restore a single tenant</span></span>](sql-database-saas-tutorial-restore-single-tenant.md)| <span data-ttu-id="abf32-127">了解如何將租用戶資料庫還原到先前的時間點。</span><span class="sxs-lookup"><span data-stu-id="abf32-127">Learn how to restore a tenant database to a prior point in time.</span></span> <span data-ttu-id="abf32-128">同時包含還原到平行資料庫 (讓現有的租用戶資料庫留在線上) 的步驟。</span><span class="sxs-lookup"><span data-stu-id="abf32-128">Steps to restore to a parallel database, leaving the existing tenant database online, are also included.</span></span> |
|[<span data-ttu-id="abf32-129">管理租用結構描述</span><span class="sxs-lookup"><span data-stu-id="abf32-129">Manage tenant schema</span></span>](sql-database-saas-tutorial-schema-management.md)| <span data-ttu-id="abf32-130">了解如何更新結構描述，以及更新跨所有 Wingtip SaaS 租用戶的參考資料。</span><span class="sxs-lookup"><span data-stu-id="abf32-130">Learn how to update schema, and update reference data, across all Wingtip SaaS tenants.</span></span> |
|[<span data-ttu-id="abf32-131">執行臨機操作分析</span><span class="sxs-lookup"><span data-stu-id="abf32-131">Run ad-hoc analytics</span></span>](sql-database-saas-tutorial-adhoc-analytics.md) | <span data-ttu-id="abf32-132">建立臨機操作分析資料庫並對所有租用戶執行即時分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="abf32-132">Create an ad-hoc analytics database and run real-time distributed queries across all tenants.</span></span>  |
|[<span data-ttu-id="abf32-133">執行租用戶分析</span><span class="sxs-lookup"><span data-stu-id="abf32-133">Run tenant analytics</span></span>](sql-database-saas-tutorial-tenant-analytics.md) | <span data-ttu-id="abf32-134">將租用戶資料擷取到分析資料庫或資料倉儲中，以便執行離線分析查詢。</span><span class="sxs-lookup"><span data-stu-id="abf32-134">Extract tenant data into an analytics database or data warehouse for running offline analytic queries.</span></span> |



## <a name="application-architecture"></a><span data-ttu-id="abf32-135">應用程式架構</span><span class="sxs-lookup"><span data-stu-id="abf32-135">Application architecture</span></span>

<span data-ttu-id="abf32-136">Wingtip SaaS 應用程式會使用「各租用戶資料庫」模型，並使用 SQL 彈性集區將效率最大化。</span><span class="sxs-lookup"><span data-stu-id="abf32-136">The Wingtip SaaS app uses the database-per-tenant model, and uses SQL elastic pools to maximize efficiency.</span></span> <span data-ttu-id="abf32-137">若要將租用戶佈建和對應至其資料，則會使用目錄資料庫。</span><span class="sxs-lookup"><span data-stu-id="abf32-137">For provisioning and mapping tenants to their data, a catalog database is used.</span></span> <span data-ttu-id="abf32-138">核心 Wingtip SaaS 應用程式會使用具有三個範例租用戶的集區，再加上目錄資料庫。</span><span class="sxs-lookup"><span data-stu-id="abf32-138">The core Wingtip SaaS application, uses a pool with three sample tenants, plus the catalog database.</span></span> <span data-ttu-id="abf32-139">完成許多 Wingtip SaaS 教學課程，可藉由引進分析資料庫、跨資料庫結構描述管理等等，造成初始部署的附加元件。</span><span class="sxs-lookup"><span data-stu-id="abf32-139">Completing many of the Wingtip SaaS tutorials result in add-ons to the intial deployment, by introducing analytic databases, cross-database schema management, etc.</span></span>


![Wingtip SaaS 架構](media/sql-database-wtp-overview/app-architecture.png)


<span data-ttu-id="abf32-141">在進行教學課程並使用應用程式時，務必將焦點放在與資料層相關的 SaaS 模式。</span><span class="sxs-lookup"><span data-stu-id="abf32-141">While going through the tutorials and working with the app, it is important to focus on the SaaS patterns as they relate to the data tier.</span></span> <span data-ttu-id="abf32-142">換句話說，著重於資料層，且不要過度分析應用程式本身。</span><span class="sxs-lookup"><span data-stu-id="abf32-142">In other words, focus on the data tier, and don't over analyze the app itself.</span></span> <span data-ttu-id="abf32-143">了解這些 SaaS 模式的實作方式是在應用程式中實作這些模式的關鍵，同時考慮針對您特定的業務需求進行任何必要的修改。</span><span class="sxs-lookup"><span data-stu-id="abf32-143">Understanding the implementation of these SaaS patterns is key to implementing these patterns in your applications, while considering any necessary modifications for your specific business requirements.</span></span>

## <a name="download-and-unblock-the-wingtip-saas-scripts"></a><span data-ttu-id="abf32-144">下載並解除封鎖 Wingtip SaaS 指令碼</span><span class="sxs-lookup"><span data-stu-id="abf32-144">Download and unblock the Wingtip SaaS scripts</span></span>

<span data-ttu-id="abf32-145">從外部來源下載 zip 檔案並進行解壓縮時，Windows 可能會封鎖可執行的內容 (指令碼、dll)。</span><span class="sxs-lookup"><span data-stu-id="abf32-145">Executable contents (scripts, dlls) may be blocked by Windows when zip files are downloaded from an external source and extracted.</span></span> <span data-ttu-id="abf32-146">從 zip 檔案解壓縮指令碼時，***請遵循下列步驟先解除封鎖 .zip 檔案，再進行解壓縮***。</span><span class="sxs-lookup"><span data-stu-id="abf32-146">When extracting the scripts from a zip file, ***follow the steps below to unblock the .zip file before extracting***.</span></span> <span data-ttu-id="abf32-147">這可確保允許執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="abf32-147">This ensures the scripts are allowed to run.</span></span>

1. <span data-ttu-id="abf32-148">瀏覽至 [Wingtip SaaS github 存放庫](https://github.com/Microsoft/WingtipSaaS)。</span><span class="sxs-lookup"><span data-stu-id="abf32-148">Browse to [the Wingtip SaaS github repo](https://github.com/Microsoft/WingtipSaaS).</span></span>
1. <span data-ttu-id="abf32-149">按一下 [複製或下載]。</span><span class="sxs-lookup"><span data-stu-id="abf32-149">Click **Clone or download**.</span></span>
1. <span data-ttu-id="abf32-150">按一下 [下載 ZIP]，並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="abf32-150">Click **Download ZIP** and save the file.</span></span>
1. <span data-ttu-id="abf32-151">以滑鼠右鍵按一下 **WingtipSaaS-master.zip** 檔案，然後選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="abf32-151">Right-click the **WingtipSaaS-master.zip** file, and select **Properties**.</span></span>
1. <span data-ttu-id="abf32-152">在 [一般] 索引標籤上，選取 [解除封鎖]。</span><span class="sxs-lookup"><span data-stu-id="abf32-152">On the **General** tab, select **Unblock**.</span></span>
1. <span data-ttu-id="abf32-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="abf32-153">Click **OK**.</span></span>
1. <span data-ttu-id="abf32-154">將檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="abf32-154">Extract the files.</span></span>

<span data-ttu-id="abf32-155">指令碼位於 *..\\WingtipSaaS-master\\Learning Modules* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="abf32-155">Scripts are located in the *..\\WingtipSaaS-master\\Learning Modules* folder.</span></span>


## <a name="working-with-the-wingtip-saas-powershell-scripts"></a><span data-ttu-id="abf32-156">使用 Wingtip SaaS PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="abf32-156">Working with the Wingtip SaaS PowerShell Scripts</span></span>

<span data-ttu-id="abf32-157">若要充分利用此範例，您必須深入了解所提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="abf32-157">To get the most out of the sample you need to dive into the provided scripts.</span></span> <span data-ttu-id="abf32-158">使用中斷點和逐步執行指令碼，並檢查不同 SaaS 模式的實作方式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abf32-158">Use breakpoints and step through the scripts, examining the details of how the different SaaS patterns are implemented.</span></span> <span data-ttu-id="abf32-159">若要輕鬆地逐步執行所提供的指令碼和模組，以獲得充分瞭解，我們建議使用 [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。</span><span class="sxs-lookup"><span data-stu-id="abf32-159">To easily step through the provided scripts and modules for the best understanding, we recommend using the [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span>

### <a name="update-the-configuration-file-for-your-deployment"></a><span data-ttu-id="abf32-160">更新部署的組態檔</span><span class="sxs-lookup"><span data-stu-id="abf32-160">Update the configuration file for your deployment</span></span>

<span data-ttu-id="abf32-161">使用您在部署期間設定的資源群組和使用者值，編輯 **UserConfig.psm1** 檔案：</span><span class="sxs-lookup"><span data-stu-id="abf32-161">Edit the **UserConfig.psm1** file with the resource group and user value that you set during deployment:</span></span>

1. <span data-ttu-id="abf32-162">開啟 PowerShell ISE 並載入...\\Learning Modules\\*UserConfig.psm1*</span><span class="sxs-lookup"><span data-stu-id="abf32-162">Open the *PowerShell ISE* and load ...\\Learning Modules\\*UserConfig.psm1*</span></span> 
1. <span data-ttu-id="abf32-163">將 ResourceGroupName 和 Name 更新為您部署的特定值 (只在第 10 行和第 11 行)。</span><span class="sxs-lookup"><span data-stu-id="abf32-163">Update *ResourceGroupName* and *Name* with the specific values for your deployment (on lines 10 and 11 only).</span></span>
1. <span data-ttu-id="abf32-164">儲存變更！</span><span class="sxs-lookup"><span data-stu-id="abf32-164">Save the changes!</span></span>

<span data-ttu-id="abf32-165">在這裏設定這些值，只是要讓您必須更新每個指令碼中的這些部署特有值。</span><span class="sxs-lookup"><span data-stu-id="abf32-165">Setting these values here simply keeps you from having to update these deployment-specific values in every script.</span></span>

### <a name="execute-scripts-by-pressing-f5"></a><span data-ttu-id="abf32-166">按 F5 執行指令碼</span><span class="sxs-lookup"><span data-stu-id="abf32-166">Execute Scripts by pressing F5</span></span>

<span data-ttu-id="abf32-167">數個指令碼會使用 $PSScriptRoot 來瀏覽資料夾，而只有在按 F5 執行指令碼時才會評估 $PSScriptRoot。</span><span class="sxs-lookup"><span data-stu-id="abf32-167">Several scripts use *$PSScriptRoot* to navigate folders, and *$PSScriptRoot* is only evaluated when scripts are executed by pressing **F5**.</span></span>  <span data-ttu-id="abf32-168">醒目提示並執行選取項目 (**F8**) 可能會導致錯誤，因此請在執行指令碼時按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="abf32-168">Highlighting and running a selection (**F8**) can result in errors, so press **F5** when running scripts.</span></span>

### <a name="step-through-the-scripts-to-examine-the-implementation"></a><span data-ttu-id="abf32-169">逐步執行指令碼來檢查實作</span><span class="sxs-lookup"><span data-stu-id="abf32-169">Step through the scripts to examine the implementation</span></span>

<span data-ttu-id="abf32-170">瞭解指令碼的最佳方法是逐步執行它們以了解其作用。</span><span class="sxs-lookup"><span data-stu-id="abf32-170">The best way to understand the scripts is by stepping through them to see what they do.</span></span> <span data-ttu-id="abf32-171">查看包含的 **Demo-** 指令碼，其可呈現輕鬆遵循的高階工作流程。</span><span class="sxs-lookup"><span data-stu-id="abf32-171">Check out the included **Demo-** scripts that present an easy to follow high-level workflow.</span></span> <span data-ttu-id="abf32-172">**Demo-** 指令碼會顯示完成每個工作所需的步驟，所以設定中斷點並且更深入探詢個別的呼叫，以查看不同 SaaS 模式的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abf32-172">The **Demo-** scripts show the steps required to accomplish each task, so set breakpoints and drill deeper into the individual calls to see implementation details for the different SaaS patterns.</span></span>

<span data-ttu-id="abf32-173">探索及逐步執行 PowerShell 指令碼的秘訣：</span><span class="sxs-lookup"><span data-stu-id="abf32-173">Tips for exploring and stepping through PowerShell scripts:</span></span>

* <span data-ttu-id="abf32-174">在 PowerShell ISE 中開啟 **Demo-** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="abf32-174">Open **Demo-** scripts in the PowerShell ISE.</span></span>
* <span data-ttu-id="abf32-175">執行或繼續使用 **F5** (不建議使用 **F8**，因為在執行指令碼的選取項目時不會評估 $PSScriptRoot)。</span><span class="sxs-lookup"><span data-stu-id="abf32-175">Execute or continue with **F5** (using **F8** is not advised because *$PSScriptRoot* is not evaluated when running selections of a script).</span></span>
* <span data-ttu-id="abf32-176">按一下或選取一行，然後按 **F9** 放置中斷點。</span><span class="sxs-lookup"><span data-stu-id="abf32-176">Place breakpoints by clicking or selecting a line and pressing **F9**.</span></span>
* <span data-ttu-id="abf32-177">使用 **F10** 不進入函式或指令碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="abf32-177">Step over a function or script call using **F10**.</span></span>
* <span data-ttu-id="abf32-178">使用 **F11** 逐步執行函式或指令碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="abf32-178">Step into a function or script call using **F11**.</span></span>
* <span data-ttu-id="abf32-179">使用 **Shift + F11** 跳離目前的函式或指令碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="abf32-179">Step out of the current function or script call using **Shift + F11**.</span></span>


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a><span data-ttu-id="abf32-180">使用 SSMS 瀏覽資料庫結構描述並執行 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="abf32-180">Explore database schema and execute SQL queries using SSMS</span></span>

<span data-ttu-id="abf32-181">使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 來連線及瀏覽應用程式伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="abf32-181">Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) to connect and browse the application servers and databases.</span></span>

<span data-ttu-id="abf32-182">部署一開始有兩部可連線的 SQL Database 伺服器 - *tenants1-&lt;User&gt;* 伺服器和 *catalog-&lt;User&gt;* 伺服器。</span><span class="sxs-lookup"><span data-stu-id="abf32-182">The deployment initially has two SQL Database servers to connect to - the *tenants1-&lt;User&gt;* server, and the *catalog-&lt;User&gt;* server.</span></span> <span data-ttu-id="abf32-183">若要確保示範連線成功，這兩部伺服器都有允許所有 IP 通過的[防火牆規則](sql-database-firewall-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="abf32-183">To ensure a successful demo connection, both servers have a [firewall rule](sql-database-firewall-configure.md) allowing all IPs through.</span></span>


1. <span data-ttu-id="abf32-184">開啟 SSMS 並連線到 tenants1-*&lt;User&gt;.database.windows.net* 伺服器。</span><span class="sxs-lookup"><span data-stu-id="abf32-184">Open *SSMS* and connect to the *tenants1-&lt;User&gt;.database.windows.net* server.</span></span>
1. <span data-ttu-id="abf32-185">按一下 [連線] > **[資料庫引擎...]**：</span><span class="sxs-lookup"><span data-stu-id="abf32-185">Click **Connect** > **Database Engine...**:</span></span>

   ![目錄伺服器](media/sql-database-wtp-overview/connect.png)

1. <span data-ttu-id="abf32-187">示範認證︰ 登入= developer、密碼 = P@ssword1</span><span class="sxs-lookup"><span data-stu-id="abf32-187">Demo credentials are: Login = *developer*, Password = *P@ssword1*</span></span>

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. <span data-ttu-id="abf32-189">重複步驟 2-3 並連線到 catalog-&lt;User&gt;.database.windows.net 伺服器。</span><span class="sxs-lookup"><span data-stu-id="abf32-189">Repeat steps 2-3 and connect to the *catalog-&lt;User&gt;.database.windows.net* server.</span></span>

<span data-ttu-id="abf32-190">成功連線之後，您會看到這兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="abf32-190">After successfully connecting you should see both servers.</span></span> <span data-ttu-id="abf32-191">視您已佈建的租用戶而定，您的資料庫清單可能有所不同：</span><span class="sxs-lookup"><span data-stu-id="abf32-191">Your list of databases might be different, depending on the tenants you've provisioned:</span></span>

![物件總管](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a><span data-ttu-id="abf32-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abf32-193">Next steps</span></span>

[<span data-ttu-id="abf32-194">部署 Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="abf32-194">Deploy the Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)