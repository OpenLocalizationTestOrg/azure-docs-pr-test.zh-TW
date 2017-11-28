---
title: "Azure SQL 資料倉儲中的 aaaManage 資料庫 |Microsoft 文件"
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
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="eb437-104">管理 Azure SQL 資料倉儲中的資料庫</span><span class="sxs-lookup"><span data-stu-id="eb437-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eb437-105">SQL 資料倉儲會自動化管理您的資料庫的各個層面。</span><span class="sxs-lookup"><span data-stu-id="eb437-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="eb437-106">比方說，tooscale 效能，您只需要 tooadjust 和支付 hello 運算資源的權限層級，然後讓 SQL 資料倉儲執行所有的 hello 工作的向外延展和向後還原作業。</span><span class="sxs-lookup"><span data-stu-id="eb437-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="eb437-107">您一定想 toomonitor 您的工作負載 tooidentify 您效能需求，以及疑難排解長時間執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="eb437-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="eb437-108">您也需要 tooperform 一些安全性工作 toomanage 權限的使用者與登入。</span><span class="sxs-lookup"><span data-stu-id="eb437-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="eb437-109">本概觀涵蓋管理 SQL 資料倉儲的這些層面。</span><span class="sxs-lookup"><span data-stu-id="eb437-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="eb437-110">管理工具</span><span class="sxs-lookup"><span data-stu-id="eb437-110">Management tools</span></span>
* <span data-ttu-id="eb437-111">調整計算</span><span class="sxs-lookup"><span data-stu-id="eb437-111">Scale Compute</span></span>
* <span data-ttu-id="eb437-112">暫停與繼續</span><span class="sxs-lookup"><span data-stu-id="eb437-112">Pause and Resume</span></span>
* <span data-ttu-id="eb437-113">效能最佳作法</span><span class="sxs-lookup"><span data-stu-id="eb437-113">Performance Best Practices</span></span>
* <span data-ttu-id="eb437-114">查詢監控</span><span class="sxs-lookup"><span data-stu-id="eb437-114">Query Monitoring</span></span>
* <span data-ttu-id="eb437-115">Security</span><span class="sxs-lookup"><span data-stu-id="eb437-115">Security</span></span>
* <span data-ttu-id="eb437-116">備份與還原</span><span class="sxs-lookup"><span data-stu-id="eb437-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="eb437-117">管理工具</span><span class="sxs-lookup"><span data-stu-id="eb437-117">Management tools</span></span>
<span data-ttu-id="eb437-118">您可以使用各種工具 toomanage 資料庫在 SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="eb437-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="eb437-119">因為您管理資料庫，您將開發工具喜好設定的每種工作類型，您需要 tooperform。</span><span class="sxs-lookup"><span data-stu-id="eb437-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="eb437-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eb437-120">Azure portal</span></span>
<span data-ttu-id="eb437-121">hello [Azure 入口網站][ Azure portal]是網頁型入口網站，建立、 更新和刪除資料庫和監視資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="eb437-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="eb437-122">此工具最適合是如果您剛開始使用 azure，管理少量的資料倉儲資料庫，或 tooquickly 需要執行一些動作。</span><span class="sxs-lookup"><span data-stu-id="eb437-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="eb437-123">tooget 入門 hello Azure 入口網站，請參閱[建立 SQL 資料倉儲 （Azure 入口網站）][Create a SQL Data Warehouse (Azure portal)]。</span><span class="sxs-lookup"><span data-stu-id="eb437-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="eb437-124">Visual Studio 中的 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="eb437-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="eb437-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) 在 Visual Studio 可讓您 tooconnect 來管理及開發您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eb437-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="eb437-126">如果您是熟悉 Visual Studio 或其他整合式開發環境 (IDE) 的應用程式開發人員，請嘗試使用 Visual Studio 中的 SSDT。</span><span class="sxs-lookup"><span data-stu-id="eb437-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="eb437-127">SSDT 包含 SQL Server 物件總管可讓您 toovisualize hello、 連線，並執行對 SQL 資料倉儲資料庫的指令碼。</span><span class="sxs-lookup"><span data-stu-id="eb437-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="eb437-128">tooquickly 連接 tooSQL 資料倉儲，您只需按一下 hello **Visual Studio 中開啟**hello Azure 傳統入口網站中檢視 hello 資料庫詳細資料時，hello 命令列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb437-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="eb437-129">請參閱 < 開始使用 Visual Studio 中的 SSDT tooget[查詢 Azure SQL 資料倉儲與 Visual Studio][Query Azure SQL Data Warehouse with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="eb437-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="eb437-130">命令列工具</span><span class="sxs-lookup"><span data-stu-id="eb437-130">Command-line tools</span></span>
<span data-ttu-id="eb437-131">命令列工具非常適合自動化您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="eb437-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="eb437-132">PowerShell 和 sqlcmd 是兩種方法皆適合 tooautomate 您的程序。</span><span class="sxs-lookup"><span data-stu-id="eb437-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="eb437-133">我們建議這些工具來管理大量的邏輯伺服器和部署在生產環境中的資源變更，可以編寫指令碼或然後自動化所需的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="eb437-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="eb437-134">動態管理檢視</span><span class="sxs-lookup"><span data-stu-id="eb437-134">Dynamic management views</span></span>
<span data-ttu-id="eb437-135">Dmv 會管理 SQL 資料倉儲的 hello bread and 奶油。</span><span class="sxs-lookup"><span data-stu-id="eb437-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="eb437-136">幾乎所有會呈現在 hello 入口網站中的資訊依賴 Dmv。</span><span class="sxs-lookup"><span data-stu-id="eb437-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="eb437-137">toosee 一份 SQL 資料倉儲 Dmv，請參閱[SQL 資料倉儲系統檢視表][SQL Data Warehouse system views]。</span><span class="sxs-lookup"><span data-stu-id="eb437-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="eb437-138">tooget 啟動，請參閱[連接和查詢使用 sqlcmd][Connect and query with sqlcmd]，和[建立資料庫 (PowerShell)][Create a database (PowerShell)]。</span><span class="sxs-lookup"><span data-stu-id="eb437-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="eb437-139">調整計算</span><span class="sxs-lookup"><span data-stu-id="eb437-139">Scale compute</span></span>
<span data-ttu-id="eb437-140">在 SQL 資料倉儲中，您可以快速地將效能相應放大或調整回來，方法是增加或減少 CPU、記憶體和 I/O 頻寬的計算資源。</span><span class="sxs-lookup"><span data-stu-id="eb437-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="eb437-141">tooscale 效能，您只需要 toodo 正在調整 hello 資料倉儲單位 (Dwu) SQL 資料倉儲會配置 tooyour 資料庫數目。</span><span class="sxs-lookup"><span data-stu-id="eb437-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="eb437-142">SQL 資料倉儲快速變更的 hello 並處理所有的基礎變更 toohardware hello 或軟體。</span><span class="sxs-lookup"><span data-stu-id="eb437-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="eb437-143">toolearn 深入了解調整 dwu 調整，請參閱[調整效能]。</span><span class="sxs-lookup"><span data-stu-id="eb437-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="eb437-144">暫停與繼續</span><span class="sxs-lookup"><span data-stu-id="eb437-144">Pause and resume</span></span>
<span data-ttu-id="eb437-145">toosave 成本，您可以暫停和繼續計算資源隨。</span><span class="sxs-lookup"><span data-stu-id="eb437-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="eb437-146">例如，如果您將不會使用 hello 資料庫期間 hello 夜晚及週末，可以暫停在這些時間，並繼續 hello 一天。</span><span class="sxs-lookup"><span data-stu-id="eb437-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="eb437-147">您不需要支付費用的 Dwu hello 資料庫暫停時。</span><span class="sxs-lookup"><span data-stu-id="eb437-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="eb437-148">如需詳細資訊，請參閱[暫停計算][Pause compute]和[繼續計算][Resume compute]。</span><span class="sxs-lookup"><span data-stu-id="eb437-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="eb437-149">效能最佳作法</span><span class="sxs-lookup"><span data-stu-id="eb437-149">Performance Best Practices</span></span>
<span data-ttu-id="eb437-150">當開始使用新的技術，探索 hello 的秘訣和技巧可從 hello 開始最佳的權限可讓您很多時間。</span><span class="sxs-lookup"><span data-stu-id="eb437-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="eb437-151">您可以在許多主題中找到我們的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="eb437-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="eb437-152">請參閱 toosee hello 最重要的考量開發您的工作負載時的許多摘要[SQL 資料倉儲的最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="eb437-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="eb437-153">查詢監控</span><span class="sxs-lookup"><span data-stu-id="eb437-153">Query Monitoring</span></span>
<span data-ttu-id="eb437-154">有時候查詢太長，但您不確定哪一個 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="eb437-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="eb437-155">SQL 資料倉儲具有動態管理檢視 (Dmv)，您可以使用 toofigure 出的查詢太長。</span><span class="sxs-lookup"><span data-stu-id="eb437-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="eb437-156">toofind 長時間執行的查詢，請參閱[監視您的工作負載使用 Dmv][Monitor your workload using DMVs]。</span><span class="sxs-lookup"><span data-stu-id="eb437-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="eb437-157">安全性</span><span class="sxs-lookup"><span data-stu-id="eb437-157">Security</span></span>
<span data-ttu-id="eb437-158">toomaintain 安全系統，您必須在 hello 警示並防範未經授權任何的存取型別。</span><span class="sxs-lookup"><span data-stu-id="eb437-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="eb437-159">安全性系統必須 toomake 確定防火牆規則已就緒，所以只有獲得授權的 IP 位址可以連線。</span><span class="sxs-lookup"><span data-stu-id="eb437-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="eb437-160">它需要使用者認證的適當驗證。</span><span class="sxs-lookup"><span data-stu-id="eb437-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="eb437-161">使用者已連接 toohello 資料庫之後，hello 使用者應該只有權限 tooperform 最少的動作。</span><span class="sxs-lookup"><span data-stu-id="eb437-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="eb437-162">toosecure 資料，您可以使用加密。</span><span class="sxs-lookup"><span data-stu-id="eb437-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="eb437-163">它也是重要 toohave 稽核與追蹤讓您可以追溯事件，如果沒有任何可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="eb437-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="eb437-164">關於管理安全性，透過 toohello head toolearn[安全性概觀][Security overview]。</span><span class="sxs-lookup"><span data-stu-id="eb437-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="eb437-165">備份與還原</span><span class="sxs-lookup"><span data-stu-id="eb437-165">Backup and restore</span></span>
<span data-ttu-id="eb437-166">對生產環境資料庫來說，擁有可靠的資料備份是不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="eb437-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="eb437-167">「SQL 資料倉儲」會自動定期備份您的作用中資料庫來維護您的資料安全。</span><span class="sxs-lookup"><span data-stu-id="eb437-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="eb437-168">這些備份可讓您 toorecover 情況下，您已在此資料已損毀或意外遭到卸除資料庫或資料。</span><span class="sxs-lookup"><span data-stu-id="eb437-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="eb437-169">針對 hello 資料備份排程，請保留原則和如何 toorestore 資料庫，請參閱[從快照還原][Restore from snapshot]。</span><span class="sxs-lookup"><span data-stu-id="eb437-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb437-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb437-170">Next steps</span></span>
<span data-ttu-id="eb437-171">使用良好的資料庫設計原則可以讓您更容易 toomanage SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="eb437-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="eb437-172">toolearn 詳細，透過 toohello head[開發概觀][Development overview]。</span><span class="sxs-lookup"><span data-stu-id="eb437-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

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
[調整效能]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
