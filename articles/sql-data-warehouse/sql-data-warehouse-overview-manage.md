---
title: "管理 Azure SQL 資料倉儲中的資料庫 | Microsoft Docs"
description: "管理 SQL 資料倉儲資料庫的概觀。 包含管理工具、DWU 與相應放大效能、疑難排解查詢效能、建立良好的安全性原則，以及從資料損毀或區域性停電還原資料庫。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: b14d0aad5a1f50c225391dbab27ec6240423a65a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="abf87-104">管理 Azure SQL 資料倉儲中的資料庫</span><span class="sxs-lookup"><span data-stu-id="abf87-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="abf87-105">SQL 資料倉儲會自動化管理您的資料庫的各個層面。</span><span class="sxs-lookup"><span data-stu-id="abf87-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="abf87-106">例如，若要調整效能，您只需要調整並支付適當等級的計算資源，然後讓 SQL 資料倉儲執行相應放大和調整回來的所有工作。</span><span class="sxs-lookup"><span data-stu-id="abf87-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span></span>

<span data-ttu-id="abf87-107">您一定想要監視工作負載來識別您的效能需求，以及對長時間執行的查詢進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="abf87-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="abf87-108">您也必須執行幾項安全性工作，管理使用者與登入的權限。</span><span class="sxs-lookup"><span data-stu-id="abf87-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span></span>

<span data-ttu-id="abf87-109">本概觀涵蓋管理 SQL 資料倉儲的這些層面。</span><span class="sxs-lookup"><span data-stu-id="abf87-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="abf87-110">管理工具</span><span class="sxs-lookup"><span data-stu-id="abf87-110">Management tools</span></span>
* <span data-ttu-id="abf87-111">調整計算</span><span class="sxs-lookup"><span data-stu-id="abf87-111">Scale Compute</span></span>
* <span data-ttu-id="abf87-112">暫停與繼續</span><span class="sxs-lookup"><span data-stu-id="abf87-112">Pause and Resume</span></span>
* <span data-ttu-id="abf87-113">效能最佳作法</span><span class="sxs-lookup"><span data-stu-id="abf87-113">Performance Best Practices</span></span>
* <span data-ttu-id="abf87-114">查詢監控</span><span class="sxs-lookup"><span data-stu-id="abf87-114">Query Monitoring</span></span>
* <span data-ttu-id="abf87-115">Security</span><span class="sxs-lookup"><span data-stu-id="abf87-115">Security</span></span>
* <span data-ttu-id="abf87-116">備份與還原</span><span class="sxs-lookup"><span data-stu-id="abf87-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="abf87-117">管理工具</span><span class="sxs-lookup"><span data-stu-id="abf87-117">Management tools</span></span>
<span data-ttu-id="abf87-118">您可以使用各種工具來管理 SQL 資料倉儲中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="abf87-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="abf87-119">管理資料庫時，您將針對您需要執行的各種類型工作開發工具喜好設定。</span><span class="sxs-lookup"><span data-stu-id="abf87-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="abf87-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="abf87-120">Azure portal</span></span>
<span data-ttu-id="abf87-121">[Azure 入口網站][Azure portal]是一個網頁型入口網站，您可以在當中建立、更新和刪除資料庫以及監視資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="abf87-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="abf87-122">如果您剛開始使用 Azure、管理少量的資料倉儲資料庫，或是需要快速執行工作，那這正是十分適合您的工具。</span><span class="sxs-lookup"><span data-stu-id="abf87-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span></span>

<span data-ttu-id="abf87-123">若要開始使用 Azure 入口網站，請參閱[建立 SQL 資料倉儲 (Azure 入口網站)][Create a SQL Data Warehouse (Azure portal)]。</span><span class="sxs-lookup"><span data-stu-id="abf87-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="abf87-124">Visual Studio 中的 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="abf87-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="abf87-125">Visual Studio 中的 [SQL Server Data Tools][SQL Server Data Tools] (SSDT) 可讓您連接、管理及開發資料庫。</span><span class="sxs-lookup"><span data-stu-id="abf87-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span></span> <span data-ttu-id="abf87-126">如果您是熟悉 Visual Studio 或其他整合式開發環境 (IDE) 的應用程式開發人員，請嘗試使用 Visual Studio 中的 SSDT。</span><span class="sxs-lookup"><span data-stu-id="abf87-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="abf87-127">SSDT 包含的 SQL Server 物件總管，可讓您針對 SQL 資料倉儲資料庫視覺化、連接和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="abf87-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="abf87-128">若要快速連線至 SQL 資料倉儲，只需在 Azure 傳統入口網站檢視資料庫的詳細資料時，按一下命令列中的 [在 Visual Studio 中開啟]  按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="abf87-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span></span>  

<span data-ttu-id="abf87-129">若要開始使用 Visual Studio 中的 SSDT，請參閱[使用 Visual Studio 來查詢 Azure SQL 資料倉儲][Query Azure SQL Data Warehouse with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="abf87-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="abf87-130">命令列工具</span><span class="sxs-lookup"><span data-stu-id="abf87-130">Command-line tools</span></span>
<span data-ttu-id="abf87-131">命令列工具非常適合自動化您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="abf87-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="abf87-132">PowerShell 和 sqlcmd 是自動化程序的兩個好方法。</span><span class="sxs-lookup"><span data-stu-id="abf87-132">PowerShell and sqlcmd are two great ways to automate your processes.</span></span>  <span data-ttu-id="abf87-133">因為您可為必要的工作編寫指令碼並自動執行這類工作，所以我們建議使用這些工具來管理大量的邏輯伺服器，以及在生產環境中部署資源變更。</span><span class="sxs-lookup"><span data-stu-id="abf87-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="abf87-134">動態管理檢視</span><span class="sxs-lookup"><span data-stu-id="abf87-134">Dynamic management views</span></span>
<span data-ttu-id="abf87-135">DMV 是管理 SQL 資料倉儲的要素。</span><span class="sxs-lookup"><span data-stu-id="abf87-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="abf87-136">入口網站上幾乎所有的資訊都依賴 DMV。</span><span class="sxs-lookup"><span data-stu-id="abf87-136">Almost all information that surfaces in the portal relies on DMVs.</span></span> <span data-ttu-id="abf87-137">若要查看「SQL 資料倉儲」DMV 的清單，請參閱 [SQL 資料倉儲系統檢視][SQL Data Warehouse system views]。</span><span class="sxs-lookup"><span data-stu-id="abf87-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="abf87-138">若要開始，請參閱[使用 sqlcmd 來連接和查詢][Connect and query with sqlcmd]和[建立資料庫 (PowerShell)][Create a database (PowerShell)]。</span><span class="sxs-lookup"><span data-stu-id="abf87-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="abf87-139">調整計算</span><span class="sxs-lookup"><span data-stu-id="abf87-139">Scale compute</span></span>
<span data-ttu-id="abf87-140">在 SQL 資料倉儲中，您可以快速地將效能相應放大或調整回來，方法是增加或減少 CPU、記憶體和 I/O 頻寬的計算資源。</span><span class="sxs-lookup"><span data-stu-id="abf87-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="abf87-141">若要調整效能，您只需要調整 SQL 資料倉儲配置到您的資料庫的資料倉儲單位 (DWU) 的數目。</span><span class="sxs-lookup"><span data-stu-id="abf87-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span></span> <span data-ttu-id="abf87-142">SQL 資料倉儲會快速進行變更，並處理硬體或軟體的所有基礎變更。</span><span class="sxs-lookup"><span data-stu-id="abf87-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span></span>

<span data-ttu-id="abf87-143">若要深入了解如何調整 DWU，請參閱[調整效能]。</span><span class="sxs-lookup"><span data-stu-id="abf87-143">To learn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="abf87-144">暫停與繼續</span><span class="sxs-lookup"><span data-stu-id="abf87-144">Pause and resume</span></span>
<span data-ttu-id="abf87-145">為了節省成本，您可以隨選暫停和繼續計算資源。</span><span class="sxs-lookup"><span data-stu-id="abf87-145">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="abf87-146">例如，如果您在夜間和週末不會使用資料庫，可以在這段時間暫停，並且在白天時繼續。</span><span class="sxs-lookup"><span data-stu-id="abf87-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="abf87-147">資料庫暫停時，不會向您收取 DWU 的費用。</span><span class="sxs-lookup"><span data-stu-id="abf87-147">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="abf87-148">如需詳細資訊，請參閱[暫停計算][Pause compute]和[繼續計算][Resume compute]。</span><span class="sxs-lookup"><span data-stu-id="abf87-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="abf87-149">效能最佳作法</span><span class="sxs-lookup"><span data-stu-id="abf87-149">Performance Best Practices</span></span>
<span data-ttu-id="abf87-150">開始使用新技術時，探索一開始就最能節省您的時間的最佳秘訣和竅門。</span><span class="sxs-lookup"><span data-stu-id="abf87-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span></span>  <span data-ttu-id="abf87-151">您可以在許多主題中找到我們的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="abf87-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="abf87-152">若要查看開發工作負載時最重要考量的諸多摘要，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="abf87-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="abf87-153">查詢監控</span><span class="sxs-lookup"><span data-stu-id="abf87-153">Query Monitoring</span></span>
<span data-ttu-id="abf87-154">有時候查詢執行時間太久，但您不確定哪一個是罪魁禍首。</span><span class="sxs-lookup"><span data-stu-id="abf87-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span></span> <span data-ttu-id="abf87-155">SQL 資料倉儲具有動態管理檢視 (DMV)，可讓您找出哪一個查詢的時間太長。</span><span class="sxs-lookup"><span data-stu-id="abf87-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span></span>

<span data-ttu-id="abf87-156">若要找出長時間執行的查詢，請參閱[使用 DMV 監視工作負載][Monitor your workload using DMVs]。</span><span class="sxs-lookup"><span data-stu-id="abf87-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="abf87-157">安全性</span><span class="sxs-lookup"><span data-stu-id="abf87-157">Security</span></span>
<span data-ttu-id="abf87-158">若要維護安全系統，您必須提高警覺，並且防範任何類型的未經授權存取。</span><span class="sxs-lookup"><span data-stu-id="abf87-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="abf87-159">安全性系統必須確定防火牆規則作用中，只有獲得授權的 IP 位址可以連接。</span><span class="sxs-lookup"><span data-stu-id="abf87-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="abf87-160">它需要使用者認證的適當驗證。</span><span class="sxs-lookup"><span data-stu-id="abf87-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="abf87-161">使用者已連接到資料庫之後，使用者應該只有執行最少動作的權限。</span><span class="sxs-lookup"><span data-stu-id="abf87-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span></span> <span data-ttu-id="abf87-162">若要保護資料，您可以使用加密。</span><span class="sxs-lookup"><span data-stu-id="abf87-162">To secure data, you can use encryption.</span></span> <span data-ttu-id="abf87-163">稽核和追蹤也同樣重要，這樣您就可以在有任何可疑的活動時追溯事件。</span><span class="sxs-lookup"><span data-stu-id="abf87-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="abf87-164">若要了解如何管理安全性，請前往[安全性概觀][Security overview]。</span><span class="sxs-lookup"><span data-stu-id="abf87-164">To learn about managing security, head over to the [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="abf87-165">備份與還原</span><span class="sxs-lookup"><span data-stu-id="abf87-165">Backup and restore</span></span>
<span data-ttu-id="abf87-166">對生產環境資料庫來說，擁有可靠的資料備份是不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="abf87-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="abf87-167">「SQL 資料倉儲」會自動定期備份您的作用中資料庫來維護您的資料安全。</span><span class="sxs-lookup"><span data-stu-id="abf87-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="abf87-168">這些備份可讓您從已損毀資料或不小心卸除資料或資料庫的情況下復原。</span><span class="sxs-lookup"><span data-stu-id="abf87-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="abf87-169">若要了解資料備份排程、保留原則及如何還原資料庫，請參閱[從快照還原][Restore from snapshot]。</span><span class="sxs-lookup"><span data-stu-id="abf87-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="abf87-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abf87-170">Next steps</span></span>
<span data-ttu-id="abf87-171">使用良好的資料庫設計原則，會讓在 SQL 資料倉儲中管理您的資料庫更容易。</span><span class="sxs-lookup"><span data-stu-id="abf87-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="abf87-172">若要深入了解，請前往[開發概觀][Development overview]。</span><span class="sxs-lookup"><span data-stu-id="abf87-172">To learn more, head over to the [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
<span data-ttu-id="abf87-173">[調整效能]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span><span class="sxs-lookup"><span data-stu-id="abf87-173">[Scale performance]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span></span>
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
