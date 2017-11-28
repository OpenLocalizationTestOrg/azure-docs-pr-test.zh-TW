---
title: "aaaGet 入門彈性資料庫工具 |Microsoft 文件"
description: "基本的 hello 彈性資料庫工具功能的 Azure SQL Database，包括簡單執行範例應用程式的詳細說明。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a><span data-ttu-id="b555d-103">開始使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="b555d-103">Get started with elastic database tools</span></span>
<span data-ttu-id="b555d-104">本文件介紹您 toohello 開發人員的體驗藉由協助您 toorun hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b555d-104">This document introduces you toohello developer experience by helping you toorun hello sample app.</span></span> <span data-ttu-id="b555d-105">hello 範例會建立簡單的分區化應用程式，並且瀏覽的彈性資料庫工具的主要功能。</span><span class="sxs-lookup"><span data-stu-id="b555d-105">hello sample creates a simple sharded application and explores key capabilities of elastic database tools.</span></span> <span data-ttu-id="b555d-106">hello 範例示範的 hello 函式[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。</span><span class="sxs-lookup"><span data-stu-id="b555d-106">hello sample demonstrates functions of hello [elastic database client library](sql-database-elastic-database-client-library.md).</span></span>

<span data-ttu-id="b555d-107">tooinstall hello 程式庫，請移太[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="b555d-107">tooinstall hello library, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="b555d-108">hello 程式庫會隨 hello 之後 > 一節中所述的 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b555d-108">hello library is installed with hello sample app that's described in hello following section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b555d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="b555d-109">Prerequisites</span></span>
* <span data-ttu-id="b555d-110">含 C# 的 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b555d-110">Visual Studio 2012 or later with C#.</span></span> <span data-ttu-id="b555d-111">請在 [Visual Studio 下載](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)上下載免費版本。</span><span class="sxs-lookup"><span data-stu-id="b555d-111">Download a free version at [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="b555d-112">NuGet 2.7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b555d-112">NuGet 2.7 or later.</span></span> <span data-ttu-id="b555d-113">tooget hello 最新版本，請參閱[安裝 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)。</span><span class="sxs-lookup"><span data-stu-id="b555d-113">tooget hello latest version, see [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>

## <a name="download-and-run-hello-sample-app"></a><span data-ttu-id="b555d-114">下載並執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b555d-114">Download and run hello sample app</span></span>
<span data-ttu-id="b555d-115">hello**彈性的 DB Tools for Azure SQL-快速入門**範例應用程式說明 hello 最重要的 hello 使用彈性資料庫工具的分區化應用程式的開發經驗的觀點。</span><span class="sxs-lookup"><span data-stu-id="b555d-115">hello **Elastic DB Tools for Azure SQL - Getting Started** sample application illustrates hello most important aspects of hello development experience for sharded applications that use elastic database tools.</span></span> <span data-ttu-id="b555d-116">此範例應用程式著重在[分區對應管理](sql-database-elastic-scale-shard-map-management.md)、[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)和[多分區查詢](sql-database-elastic-scale-multishard-querying.md)的主要使用案例。</span><span class="sxs-lookup"><span data-stu-id="b555d-116">It focuses on key use cases for [shard map management](sql-database-elastic-scale-shard-map-management.md), [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), and [multi-shard querying](sql-database-elastic-scale-multishard-querying.md).</span></span> <span data-ttu-id="b555d-117">toodownload 和執行的 hello 範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b555d-117">toodownload and run hello sample, follow these steps:</span></span> 

1. <span data-ttu-id="b555d-118">下載 hello[彈性的 DB Tools for Azure SQL-快速入門範例](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6)從 MSDN。</span><span class="sxs-lookup"><span data-stu-id="b555d-118">Download hello [Elastic DB Tools for Azure SQL - Getting Started sample](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) from MSDN.</span></span> <span data-ttu-id="b555d-119">解壓縮您選擇的 hello 範例 tooa 位置。</span><span class="sxs-lookup"><span data-stu-id="b555d-119">Unzip hello sample tooa location that you choose.</span></span>

2. <span data-ttu-id="b555d-120">toocreate 專案中，開啟 hello **ElasticScaleStarterKit.sln**解決方案的 hello **C#**目錄。</span><span class="sxs-lookup"><span data-stu-id="b555d-120">toocreate a project, open hello **ElasticScaleStarterKit.sln** solution from hello **C#** directory.</span></span>

3. <span data-ttu-id="b555d-121">在 hello hello 範例專案的方案，開啟 hello **app.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="b555d-121">In hello solution for hello sample project, open hello **app.config** file.</span></span> <span data-ttu-id="b555d-122">您的 Azure SQL Database 伺服器名稱和登入資訊 （使用者名稱和密碼），然後遵循 hello 檔案 tooadd hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="b555d-122">Then follow hello instructions in hello file tooadd your Azure SQL Database server name and your sign-in information (user name and password).</span></span>

4. <span data-ttu-id="b555d-123">建置並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b555d-123">Build and run hello application.</span></span> <span data-ttu-id="b555d-124">出現提示時，讓 Visual Studio toorestore hello 的 hello 方案的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="b555d-124">When prompted, enable Visual Studio toorestore hello NuGet packages of hello solution.</span></span> <span data-ttu-id="b555d-125">這會從 NuGet 下載 hello hello 彈性資料庫用戶端程式庫的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b555d-125">This downloads hello latest version of hello elastic database client library from NuGet.</span></span>

5. <span data-ttu-id="b555d-126">試驗 hello 不同選項 toolearn 進一步了解 hello 的用戶端程式庫功能。</span><span class="sxs-lookup"><span data-stu-id="b555d-126">Experiment with hello different options toolearn more about hello client library capabilities.</span></span> <span data-ttu-id="b555d-127">請注意 hello 步驟 hello hello 主控台輸出中的應用程式會接受，但覺得 hello 幕後可用 tooexplore hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b555d-127">Note hello steps hello application takes in hello console output and feel free tooexplore hello code behind hello scenes.</span></span>
   
    ![Progress][4]

<span data-ttu-id="b555d-129">恭喜 - 您已使用彈性資料庫工具，在 SQL Database 上成功建置並執行您的第一個分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="b555d-129">Congratulations--you have successfully built and run your first sharded application by using elastic database tools on SQL Database.</span></span> <span data-ttu-id="b555d-130">使用 Visual Studio 或 SQL Server Management Studio tooconnect tooyour SQL 資料庫，看看 hello 範例建立的 hello 分區快速。</span><span class="sxs-lookup"><span data-stu-id="b555d-130">Use Visual Studio or SQL Server Management Studio tooconnect tooyour SQL database and take a quick look at hello shards that hello sample created.</span></span> <span data-ttu-id="b555d-131">您會注意到新的範例分區化資料庫和分區對應管理員資料庫已建立該 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b555d-131">You will notice new sample shard databases and a shard map manager database that hello sample has created.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b555d-132">我們建議您一律使用 hello 最新版本的 Management Studio，以便您保持同步更新 tooAzure 與 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b555d-132">We recommend that you always use hello latest version of Management Studio so that you stay synchronized with updates tooAzure and SQL Database.</span></span> <span data-ttu-id="b555d-133">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b555d-133">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a><span data-ttu-id="b555d-134">關鍵的 hello 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="b555d-134">Key pieces of hello code sample</span></span>
* <span data-ttu-id="b555d-135">**管理分區和分區對應**: hello 程式碼說明如何與分區、 範圍和 hello 檔案中的對應 toowork **ShardManagementUtils.cs**。</span><span class="sxs-lookup"><span data-stu-id="b555d-135">**Managing shards and shard maps**: hello code illustrates how toowork with shards, ranges, and mappings in hello file **ShardManagementUtils.cs**.</span></span> <span data-ttu-id="b555d-136">如需詳細資訊，請參閱[hello 分區對應管理員與資料庫的延展](http://go.microsoft.com/?linkid=9862595)。</span><span class="sxs-lookup"><span data-stu-id="b555d-136">For more information, see [Scale out databases with hello shard map manager](http://go.microsoft.com/?linkid=9862595).</span></span>  

* <span data-ttu-id="b555d-137">**資料依存路由**： 交易 toohello 右分區的路由，如下所示**DataDependentRoutingSample.cs**。</span><span class="sxs-lookup"><span data-stu-id="b555d-137">**Data-dependent routing**: Routing of transactions toohello right shard is shown in **DataDependentRoutingSample.cs**.</span></span> <span data-ttu-id="b555d-138">如需詳細資訊，請參閱[資料相依路由](http://go.microsoft.com/?linkid=9862596)。</span><span class="sxs-lookup"><span data-stu-id="b555d-138">For more information, see [Data-dependent routing](http://go.microsoft.com/?linkid=9862596).</span></span> 

* <span data-ttu-id="b555d-139">**查詢透過多個分區**： 跨分區查詢如下所示 hello 檔案**MultiShardQuerySample.cs**。</span><span class="sxs-lookup"><span data-stu-id="b555d-139">**Querying over multiple shards**: Querying across shards is illustrated in hello file **MultiShardQuerySample.cs**.</span></span> <span data-ttu-id="b555d-140">如需詳細資訊，請參閱[多分區查詢](http://go.microsoft.com/?linkid=9862597)。</span><span class="sxs-lookup"><span data-stu-id="b555d-140">For more information, see [Multi-shard querying](http://go.microsoft.com/?linkid=9862597).</span></span>

* <span data-ttu-id="b555d-141">**加入空白的分區**: hello hello 檔案中的程式碼所執行 hello 反覆加入新的空白分區**CreateShardSample.cs**。</span><span class="sxs-lookup"><span data-stu-id="b555d-141">**Adding empty shards**: hello iterative adding of new empty shards is performed by hello code in hello file **CreateShardSample.cs**.</span></span> <span data-ttu-id="b555d-142">如需詳細資訊，請參閱[hello 分區對應管理員與資料庫的延展](http://go.microsoft.com/?linkid=9862595)。</span><span class="sxs-lookup"><span data-stu-id="b555d-142">For more information, see [Scale out databases with hello shard map manager](http://go.microsoft.com/?linkid=9862595).</span></span>

### <a name="other-elastic-scale-operations"></a><span data-ttu-id="b555d-143">其他 Elastic Scale 作業</span><span class="sxs-lookup"><span data-stu-id="b555d-143">Other elastic scale operations</span></span>
* <span data-ttu-id="b555d-144">**分割現有分區**: hello 功能 toosplit 分區係由 hello**分割合併工具**。</span><span class="sxs-lookup"><span data-stu-id="b555d-144">**Splitting an existing shard**: hello capability toosplit shards is provided by hello **split-merge tool**.</span></span> <span data-ttu-id="b555d-145">如需詳細資訊，請參閱[在向外延展的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="b555d-145">For more information, see [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

* <span data-ttu-id="b555d-146">**合併現有分區**： 分區合併也會執行使用 hello**分割合併工具**。</span><span class="sxs-lookup"><span data-stu-id="b555d-146">**Merging existing shards**: Shard merges are also performed by using hello **split-merge tool**.</span></span> <span data-ttu-id="b555d-147">如需詳細資訊，請參閱[在向外延展的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="b555d-147">For more information, see [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>   

## <a name="cost"></a><span data-ttu-id="b555d-148">成本</span><span class="sxs-lookup"><span data-stu-id="b555d-148">Cost</span></span>
<span data-ttu-id="b555d-149">hello 彈性資料庫工具是免費的。</span><span class="sxs-lookup"><span data-stu-id="b555d-149">hello elastic database tools are free.</span></span> <span data-ttu-id="b555d-150">當您使用彈性資料庫工具時，您沒有收到任何額外的費用，在您的 Azure 使用量 hello 成本之上。</span><span class="sxs-lookup"><span data-stu-id="b555d-150">When you use elastic database tools, you don't receive any additional charges on top of hello cost of your Azure usage.</span></span> 

<span data-ttu-id="b555d-151">例如，hello 範例應用程式會建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b555d-151">For example, hello sample application creates new databases.</span></span> <span data-ttu-id="b555d-152">這個 hello 成本取決於您選擇的 hello SQL Database 版本和 hello Azure 應用程式的使用量。</span><span class="sxs-lookup"><span data-stu-id="b555d-152">hello cost for this depends on hello SQL Database edition you choose and hello Azure usage of your application.</span></span>

<span data-ttu-id="b555d-153">如需價格資訊，請參閱 [SQL Database 定價詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="b555d-153">For pricing information, see [SQL Database pricing details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b555d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b555d-154">Next steps</span></span>
<span data-ttu-id="b555d-155">如需彈性資料庫工具的詳細資訊，請參閱 hello 下列頁面：</span><span class="sxs-lookup"><span data-stu-id="b555d-155">For more information about elastic database tools, see hello following pages:</span></span>

* <span data-ttu-id="b555d-156">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="b555d-156">Code samples:</span></span> 
  * [<span data-ttu-id="b555d-157">適用於 Azure SQL 的彈性 DB 工具 - 開始使用 (英文)</span><span class="sxs-lookup"><span data-stu-id="b555d-157">Elastic DB Tools for Azure SQL - Getting Started</span></span>](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [<span data-ttu-id="b555d-158">適用於 Azure SQL 的彈性 DB 工具 - Entity Framework 整合 (英文)</span><span class="sxs-lookup"><span data-stu-id="b555d-158">Elastic DB Tools for Azure SQL - Entity Framework Integration</span></span>](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [<span data-ttu-id="b555d-159">指令碼中心的分區彈性</span><span class="sxs-lookup"><span data-stu-id="b555d-159">Shard Elasticity on Script Center</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* <span data-ttu-id="b555d-160">部落格：[Elastic Scale 公告 (英文)](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="b555d-160">Blog: [Elastic Scale announcement](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)</span></span>
* <span data-ttu-id="b555d-161">Microsoft Virtual Academy:[實作向外延展使用分區化以 hello 彈性資料庫用戶端程式庫視訊](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965)</span><span class="sxs-lookup"><span data-stu-id="b555d-161">Microsoft Virtual Academy: [Implementing Scale-Out Using Sharding with hello Elastic Database Client Library Video](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965)</span></span> 
* <span data-ttu-id="b555d-162">第 9 頻道：[Elastic Scale 概觀影片 (英文)](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)</span><span class="sxs-lookup"><span data-stu-id="b555d-162">Channel 9: [Elastic Scale overview video](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)</span></span>
* <span data-ttu-id="b555d-163">討論論壇：[Azure SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)</span><span class="sxs-lookup"><span data-stu-id="b555d-163">Discussion forum: [Azure SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)</span></span>
* <span data-ttu-id="b555d-164">toomeasure 效能：[分區對應管理員的效能計數器](sql-database-elastic-database-client-library.md)</span><span class="sxs-lookup"><span data-stu-id="b555d-164">toomeasure performance: [Performance counters for shard map manager](sql-database-elastic-database-client-library.md)</span></span>

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

