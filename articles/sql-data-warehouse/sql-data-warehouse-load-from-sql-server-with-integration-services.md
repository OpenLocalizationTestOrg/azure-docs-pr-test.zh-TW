---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (SSIS) |Microsoft 文件"
description: "示範如何從各種不同的資料的 SQL Server Integration Services (SSIS) 封裝 toomove 資料 toocreate 來源 tooSQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="96ac7-103">將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS)</span><span class="sxs-lookup"><span data-stu-id="96ac7-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96ac7-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="96ac7-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="96ac7-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="96ac7-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="96ac7-106">bcp</span><span class="sxs-lookup"><span data-stu-id="96ac7-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="96ac7-107">從 SQL Server 中建立 SQL Server Integration Services (SSIS) 封裝 tooload 資料到 Azure SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="96ac7-107">Create a SQL Server Integration Services (SSIS) package tooload data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-108">您可以選擇性地重建、 轉換及清理 hello 資料通過 hello SSIS 資料流程。</span><span class="sxs-lookup"><span data-stu-id="96ac7-108">You can optionally restructure, transform, and cleanse hello data as it passes through hello SSIS data flow.</span></span>

<span data-ttu-id="96ac7-109">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="96ac7-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="96ac7-110">在 Visual Studio 中建立新的整合服務專案</span><span class="sxs-lookup"><span data-stu-id="96ac7-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="96ac7-111">連接 toodata 來源，包括 SQL Server （做為來源） 和 SQL 資料倉儲 （做為目的地）。</span><span class="sxs-lookup"><span data-stu-id="96ac7-111">Connect toodata sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="96ac7-112">設計 hello 來源中的資料載入 hello 目的地的 SSIS 封裝。</span><span class="sxs-lookup"><span data-stu-id="96ac7-112">Design an SSIS package that loads data from hello source into hello destination.</span></span>
* <span data-ttu-id="96ac7-113">執行 hello SSIS 封裝 tooload hello 資料。</span><span class="sxs-lookup"><span data-stu-id="96ac7-113">Run hello SSIS package tooload hello data.</span></span>

<span data-ttu-id="96ac7-114">本教學課程會使用 SQL Server 作為 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="96ac7-114">This tutorial uses SQL Server as hello data source.</span></span> <span data-ttu-id="96ac7-115">SQL Server 可在內部部署或在 Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="96ac7-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="96ac7-116">基本概念</span><span class="sxs-lookup"><span data-stu-id="96ac7-116">Basic concepts</span></span>
<span data-ttu-id="96ac7-117">hello 封裝是工作的 hello 在 SSIS 中單位。</span><span class="sxs-lookup"><span data-stu-id="96ac7-117">hello package is hello unit of work in SSIS.</span></span> <span data-ttu-id="96ac7-118">相關的封裝集成群組則為專案。</span><span class="sxs-lookup"><span data-stu-id="96ac7-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="96ac7-119">在 Visual Studio 中使用 SQL Server Data Tools 建立專案和設計封裝。</span><span class="sxs-lookup"><span data-stu-id="96ac7-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="96ac7-120">hello 設計程序是視覺化的程序中您拖放元件 hello 工具箱 toohello 設計介面，從連接它們，並設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="96ac7-120">hello design process is a visual process in which you drag and drop components from hello Toolbox toohello design surface, connect them, and set their properties.</span></span> <span data-ttu-id="96ac7-121">完成您的封裝之後，您可以選擇性地部署 tooSQL 伺服器的全方位管理、 監視及安全性。</span><span class="sxs-lookup"><span data-stu-id="96ac7-121">After you finish your package, you can optionally deploy it tooSQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="96ac7-122">以 SSIS 載入資料的選項</span><span class="sxs-lookup"><span data-stu-id="96ac7-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="96ac7-123">SQL Server Integration Services (SSIS) 是彈性的工具組合，提供連接至 SQL 資料倉儲、並將資料載入 SQL 資料倉儲的各種選項。</span><span class="sxs-lookup"><span data-stu-id="96ac7-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="96ac7-124">使用 ADO NET 目的地 tooconnect tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96ac7-124">Use an ADO NET Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-125">本教學課程會使用 ADO NET 目的地，因為它有 hello 最少的組態選項。</span><span class="sxs-lookup"><span data-stu-id="96ac7-125">This tutorial uses an ADO NET Destination because it has hello fewest configuration options.</span></span>
2. <span data-ttu-id="96ac7-126">使用 OLE DB 目的地 tooconnect tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96ac7-126">Use an OLE DB Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-127">這個選項可能會提供稍微較佳的效能比 hello ADO NET 目的地。</span><span class="sxs-lookup"><span data-stu-id="96ac7-127">This option may provide slightly better performance than hello ADO NET Destination.</span></span>
3. <span data-ttu-id="96ac7-128">使用 Azure Blob 儲存體中的 hello Azure Blob 上傳工作 toostage hello 資料。</span><span class="sxs-lookup"><span data-stu-id="96ac7-128">Use hello Azure Blob Upload Task toostage hello data in Azure Blob Storage.</span></span> <span data-ttu-id="96ac7-129">然後，使用 hello SSIS 執行 SQL 工作 toolaunch hello 資料載入 SQL 資料倉儲 Polybase 指令碼。</span><span class="sxs-lookup"><span data-stu-id="96ac7-129">Then use hello SSIS Execute SQL task toolaunch a Polybase script that loads hello data into SQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-130">此選項提供 hello 的 hello 此處所列的三個選項的最佳效能。</span><span class="sxs-lookup"><span data-stu-id="96ac7-130">This option provides hello best performance of hello three options listed here.</span></span> <span data-ttu-id="96ac7-131">tooget hello Azure Blob 上傳工作，下載 hello [Microsoft SQL Server 2016 Integration Services 功能套件 azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-131">tooget hello Azure Blob Upload task, download hello [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="96ac7-132">toolearn 深入了解 Polybase，請參閱[PolyBase 指南][PolyBase Guide]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-132">toolearn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="96ac7-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="96ac7-133">Before you start</span></span>
<span data-ttu-id="96ac7-134">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="96ac7-134">toostep through this tutorial, you need:</span></span>

1. <span data-ttu-id="96ac7-135">**SQL Server Integration Services (SSIS)**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="96ac7-136">SSIS 是 SQL Server 的元件，需有試用版或授權版的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="96ac7-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="96ac7-137">tooget 評估版的 SQL Server 2016 Preview，請參閱[SQL Server 評估版][SQL Server Evaluations]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-137">tooget an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="96ac7-138">**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-138">**Visual Studio**.</span></span> <span data-ttu-id="96ac7-139">tooget hello 免費的 Visual Studio Community Edition，請參閱[Visual Studio Community][Visual Studio Community]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-139">tooget hello free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="96ac7-140">**SQL Server Data Tools for Visual Studio (SSDT)**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="96ac7-141">tooget SQL Server Data Tools for Visual Studio，請參閱[下載 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-141">tooget SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="96ac7-142">**範例資料**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-142">**Sample data**.</span></span> <span data-ttu-id="96ac7-143">本教學課程使用範例資料為 hello 載入 SQL 資料倉儲的來源資料 toobe hello AdventureWorks 範例資料庫中儲存在 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="96ac7-143">This tutorial uses sample data stored in SQL Server in hello AdventureWorks sample database as hello source data toobe loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-144">tooget hello AdventureWorks 範例資料庫，請參閱[AdventureWorks 2014 範例資料庫][AdventureWorks 2014 Sample Databases]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-144">tooget hello AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="96ac7-145">**SQL 資料倉儲資料庫和權限**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="96ac7-146">本教學課程 tooa SQL 資料倉儲執行個體連接並載入資料。</span><span class="sxs-lookup"><span data-stu-id="96ac7-146">This tutorial connects tooa SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="96ac7-147">您有 toohave 權限 toocreate 資料表和 tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="96ac7-147">You have toohave permissions toocreate a table and tooload data.</span></span>
6. <span data-ttu-id="96ac7-148">**防火牆規則**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-148">**A firewall rule**.</span></span> <span data-ttu-id="96ac7-149">Toocreate 防火牆規則含有上有 SQL 資料倉儲 hello 您本機電腦的 IP 位址之前，您可以上傳資料 toohello SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96ac7-149">You have toocreate a firewall rule on SQL Data Warehouse with hello IP address of your local computer before you can upload data toohello SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="96ac7-150">步驟 1：建立新的 Integration Services 專案</span><span class="sxs-lookup"><span data-stu-id="96ac7-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="96ac7-151">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="96ac7-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="96ac7-152">在 hello**檔案**功能表上，選取**新增 |專案**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-152">On hello **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="96ac7-153">瀏覽 toohello**已安裝 |範本 |Business Intelligence |Integration Services**專案類型。</span><span class="sxs-lookup"><span data-stu-id="96ac7-153">Navigate toohello **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="96ac7-154">選取 [整合服務專案] 。</span><span class="sxs-lookup"><span data-stu-id="96ac7-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="96ac7-155">提供 [名稱] 和 [位置] 的值，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="96ac7-156">Visual Studio 隨即開啟，並建立新的整合服務 (SSIS) 專案。</span><span class="sxs-lookup"><span data-stu-id="96ac7-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="96ac7-157">然後 Visual Studio 會在 hello 專案開啟 hello hello 單一新的 SSIS 封裝 (Package.dtsx) 的設計工具。</span><span class="sxs-lookup"><span data-stu-id="96ac7-157">Then Visual Studio opens hello designer for hello single new SSIS package (Package.dtsx) in hello project.</span></span> <span data-ttu-id="96ac7-158">您會看到下列畫面區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="96ac7-158">You see hello following screen areas:</span></span>

* <span data-ttu-id="96ac7-159">Hello 左側 hello**工具箱**的 SSIS 元件。</span><span class="sxs-lookup"><span data-stu-id="96ac7-159">On hello left, hello **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="96ac7-160">Hello 中間 hello 與多個索引標籤的設計介面。</span><span class="sxs-lookup"><span data-stu-id="96ac7-160">In hello middle, hello design surface, with multiple tabs.</span></span> <span data-ttu-id="96ac7-161">您通常會使用至少 hello**控制流程**和 hello**資料流程**索引標籤。</span><span class="sxs-lookup"><span data-stu-id="96ac7-161">You typically use at least hello **Control Flow** and hello **Data Flow** tabs.</span></span>
* <span data-ttu-id="96ac7-162">在右邊的 hello，hello**方案總管 中**和 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="96ac7-162">On hello right, hello **Solution Explorer** and hello **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a><span data-ttu-id="96ac7-163">步驟 2： 建立 hello 基本資料流程</span><span class="sxs-lookup"><span data-stu-id="96ac7-163">Step 2: Create hello basic data flow</span></span>
1. <span data-ttu-id="96ac7-164">資料流程工作拖曳 hello 設計介面的 hello 工具箱 toohello 中心 (在 hello**控制流程** 索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="96ac7-164">Drag a Data Flow Task from hello Toolbox toohello center of hello design surface (on hello **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="96ac7-165">按兩下 hello Data Flow Task tooswitch toohello 資料流程 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="96ac7-165">Double-click hello Data Flow Task tooswitch toohello Data Flow tab.</span></span>
3. <span data-ttu-id="96ac7-166">從 hello [其他來源] 清單中 hello 工具箱，拖曳 ADO.NET 來源 toohello 設計介面。</span><span class="sxs-lookup"><span data-stu-id="96ac7-166">From hello Other Sources list in hello Toolbox, drag an ADO.NET Source toohello design surface.</span></span> <span data-ttu-id="96ac7-167">Hello 仍已選取的來源配接器，變更其名稱太**SQL Server 來源**在 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="96ac7-167">With hello source adapter still selected, change its name too**SQL Server source** in hello **Properties** pane.</span></span>
4. <span data-ttu-id="96ac7-168">從 hello 工具箱中的 hello 其他目的地清單，拖曳 hello ADO.NET 來源下的 ADO.NET 目的地 toohello 設計介面。</span><span class="sxs-lookup"><span data-stu-id="96ac7-168">From hello Other Destinations list in hello Toolbox, drag an ADO.NET Destination toohello design surface under hello ADO.NET Source.</span></span> <span data-ttu-id="96ac7-169">Hello 仍已選取的目的地配接器，變更其名稱太**SQL DW 目的地**在 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="96ac7-169">With hello destination adapter still selected, change its name too**SQL DW destination** in hello **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a><span data-ttu-id="96ac7-170">步驟 3： 設定 hello 來源配接器</span><span class="sxs-lookup"><span data-stu-id="96ac7-170">Step 3: Configure hello source adapter</span></span>
1. <span data-ttu-id="96ac7-171">按兩下 hello 來源配接器 tooopen hello **ADO.NET 來源編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-171">Double-click hello source adapter tooopen hello **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="96ac7-172">在 hello**連線管理員**hello 索引標籤**ADO.NET 來源編輯器**，按一下 hello**新增**按鈕的下一個 toohello **ADO.NET 連接管理員**清單 tooopen hello**設定 ADO.NET 連接管理員**對話方塊並建立本教學課程將資料載入從中 hello SQL Server 資料庫的連接設定。</span><span class="sxs-lookup"><span data-stu-id="96ac7-172">On hello **Connection Manager** tab of hello **ADO.NET Source Editor**, click hello **New** button next toohello **ADO.NET connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="96ac7-173">在 hello**設定 ADO.NET 連接管理員**對話方塊方塊中，按一下 hello**新增**按鈕 tooopen hello**連線管理員**對話方塊並建立新的資料連接。</span><span class="sxs-lookup"><span data-stu-id="96ac7-173">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="96ac7-174">在 hello**連線管理員**對話方塊方塊中，執行下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="96ac7-174">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="96ac7-175">如**提供者**，選取 hello SqlClient 資料提供者。</span><span class="sxs-lookup"><span data-stu-id="96ac7-175">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="96ac7-176">如**伺服器名稱**，輸入 hello SQL Server 名稱。</span><span class="sxs-lookup"><span data-stu-id="96ac7-176">For **Server name**, enter hello SQL Server name.</span></span>
   3. <span data-ttu-id="96ac7-177">在 hello **toohello 伺服器上的記錄**區段中，選取或輸入驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-177">In hello **Log on toohello server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="96ac7-178">在 hello**連接 tooa 資料庫**區段中，選取 hello AdventureWorks 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="96ac7-178">In hello **Connect tooa database** section, select hello AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="96ac7-179">按一下 [測試連接] 。</span><span class="sxs-lookup"><span data-stu-id="96ac7-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="96ac7-180">在 報告 hello hello 連線測試結果的 hello 對話方塊中，按一下 **確定**tooreturn toohello**連接管理員** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-180">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="96ac7-181">在 hello**連接管理員**對話方塊中，按一下 [**確定**tooreturn toohello**設定 ADO.NET 連接管理員**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-181">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="96ac7-182">在 hello**設定 ADO.NET 連接管理員**對話方塊中，按一下**確定**tooreturn toohello **ADO.NET 來源編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-182">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="96ac7-183">在 hello **ADO.NET 來源編輯器**，在 hello **hello 資料表或檢視 hello 名稱**清單中，選取 hello **Sales.SalesOrderDetail**資料表。</span><span class="sxs-lookup"><span data-stu-id="96ac7-183">In hello **ADO.NET Source Editor**, in hello **Name of hello table or hello view** list, select hello **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="96ac7-184">按一下**預覽**toosee hello hello hello 中的來源資料表中資料的前 200 個資料列**預覽 Query Results**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-184">Click **Preview** toosee hello first 200 rows of data in hello source table in hello **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="96ac7-185">在 hello**預覽 Query Results**對話方塊中，按一下 **關閉**tooreturn toohello **ADO.NET 來源編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-185">In hello **Preview Query Results** dialog box, click **Close** tooreturn toohello **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="96ac7-186">在 hello **ADO.NET 來源編輯器**，按一下**確定**toofinish 設定 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="96ac7-186">In hello **ADO.NET Source Editor**, click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a><span data-ttu-id="96ac7-187">步驟 4： 連接 hello 來源配接器 toohello 目的地配接器</span><span class="sxs-lookup"><span data-stu-id="96ac7-187">Step 4: Connect hello source adapter toohello destination adapter</span></span>
1. <span data-ttu-id="96ac7-188">選取 hello hello 設計介面上的來源配接器。</span><span class="sxs-lookup"><span data-stu-id="96ac7-188">Select hello source adapter on hello design surface.</span></span>
2. <span data-ttu-id="96ac7-189">選取 hello 來源配接器從延伸的 hello 藍色箭號，並將它拖曳 toohello 目的地編輯器，直到它的地方貼齊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-189">Select hello blue arrow that extends from hello source adapter and drag it toohello destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="96ac7-190">在典型的 SSIS 封裝中，您可以使用其他元件從 hello SSIS 工具箱 之間 hello 來源和 hello 目的地 toorestructure、 轉換的數字，並清理通過 hello SSIS 資料流程的資料。</span><span class="sxs-lookup"><span data-stu-id="96ac7-190">In a typical SSIS package, you use a number of other components from hello SSIS Toolbox in between hello source and hello destination toorestructure, transform, and cleanse your data as it passes through hello SSIS data flow.</span></span> <span data-ttu-id="96ac7-191">tookeep 越簡單越好這個範例中，我們正在連接 hello 直接來源 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="96ac7-191">tookeep this example as simple as possible, we’re connecting hello source directly toohello destination.</span></span>

## <a name="step-5-configure-hello-destination-adapter"></a><span data-ttu-id="96ac7-192">步驟 5： 設定 hello 目的地配接器</span><span class="sxs-lookup"><span data-stu-id="96ac7-192">Step 5: Configure hello destination adapter</span></span>
1. <span data-ttu-id="96ac7-193">按兩下 hello 目的地配接器 tooopen hello **ADO.NET 目的地編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-193">Double-click hello destination adapter tooopen hello **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="96ac7-194">在 hello**連線管理員**hello 索引標籤**ADO.NET 目的地編輯器**，按一下 hello**新增**按鈕的下一個 toohello**連線管理員**清單 tooopen hello**設定 ADO.NET 連接管理員**對話方塊並建立本教學課程將資料載入到其中的 hello Azure SQL 資料倉儲資料庫的連接設定。</span><span class="sxs-lookup"><span data-stu-id="96ac7-194">On hello **Connection Manager** tab of hello **ADO.NET Destination Editor**, click hello **New** button next toohello **Connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="96ac7-195">在 hello**設定 ADO.NET 連接管理員**對話方塊方塊中，按一下 hello**新增**按鈕 tooopen hello**連線管理員**對話方塊並建立新的資料連接。</span><span class="sxs-lookup"><span data-stu-id="96ac7-195">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="96ac7-196">在 hello**連線管理員**對話方塊方塊中，執行下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="96ac7-196">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   1. <span data-ttu-id="96ac7-197">如**提供者**，選取 hello SqlClient 資料提供者。</span><span class="sxs-lookup"><span data-stu-id="96ac7-197">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="96ac7-198">如**伺服器名稱**，輸入 hello SQL 資料倉儲的名稱。</span><span class="sxs-lookup"><span data-stu-id="96ac7-198">For **Server name**, enter hello SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="96ac7-199">在 hello **toohello 伺服器上的記錄**區段中，選取**使用 SQL Server 驗證**並輸入驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-199">In hello **Log on toohello server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="96ac7-200">在 hello**連接 tooa 資料庫**區段中，選取現有的 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="96ac7-200">In hello **Connect tooa database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="96ac7-201">按一下 [測試連接] 。</span><span class="sxs-lookup"><span data-stu-id="96ac7-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="96ac7-202">在 報告 hello hello 連線測試結果的 hello 對話方塊中，按一下 **確定**tooreturn toohello**連接管理員** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-202">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="96ac7-203">在 hello**連接管理員**對話方塊中，按一下 [**確定**tooreturn toohello**設定 ADO.NET 連接管理員**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96ac7-203">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="96ac7-204">在 hello**設定 ADO.NET 連接管理員**對話方塊中，按一下**確定**tooreturn toohello **ADO.NET 目的地編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-204">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="96ac7-205">在 hello **ADO.NET 目的地編輯器**，按一下 **新增**下一步 toohello**使用資料表或檢視**清單 tooopen hello **Create Table**對話方塊toocreate 具有符合 hello 來源資料表的資料行清單的新目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="96ac7-205">In hello **ADO.NET Destination Editor**, click **New** next toohello **Use a table or view** list tooopen hello **Create Table** dialog box toocreate a new destination table with a column list that matches hello source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="96ac7-206">在 hello **Create Table**對話方塊方塊中，執行下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="96ac7-206">In hello **Create Table** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="96ac7-207">變更 hello hello 目的地資料表名稱太**SalesOrderDetail**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-207">Change hello name of hello destination table too**SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="96ac7-208">移除 hello **rowguid**資料行。</span><span class="sxs-lookup"><span data-stu-id="96ac7-208">Remove hello **rowguid** column.</span></span> <span data-ttu-id="96ac7-209">hello **uniqueidentifier** SQL 資料倉儲中不支援資料類型。</span><span class="sxs-lookup"><span data-stu-id="96ac7-209">hello **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="96ac7-210">變更資料型別 hello hello **LineTotal**資料行太**money**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-210">Change hello data type of hello **LineTotal** column too**money**.</span></span> <span data-ttu-id="96ac7-211">hello**十進位**SQL 資料倉儲中不支援資料類型。</span><span class="sxs-lookup"><span data-stu-id="96ac7-211">hello **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="96ac7-212">如需支援的資料類型資訊，請參閱[建立資料表 (Azure SQL 資料倉儲，平行資料倉儲)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="96ac7-213">按一下**確定**toocreate hello 資料表並傳回 toohello **ADO.NET 目的地編輯器**。</span><span class="sxs-lookup"><span data-stu-id="96ac7-213">Click **OK** toocreate hello table and return toohello **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="96ac7-214">在 hello **ADO.NET 目的地編輯器**，選取 hello**對應**toosee 索引標籤上 hello 來源中的資料行的方式對應 toocolumns hello 目的地中的。</span><span class="sxs-lookup"><span data-stu-id="96ac7-214">In hello **ADO.NET Destination Editor**, select hello **Mappings** tab toosee how columns in hello source are mapped toocolumns in hello destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="96ac7-215">按一下**確定**toofinish 設定 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="96ac7-215">Click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-6-run-hello-package-tooload-hello-data"></a><span data-ttu-id="96ac7-216">步驟 6： 執行 hello 封裝 tooload hello 資料</span><span class="sxs-lookup"><span data-stu-id="96ac7-216">Step 6: Run hello package tooload hello data</span></span>
<span data-ttu-id="96ac7-217">依序按一下 hello 執行的 hello 封裝**啟動**按鈕 hello 工具列上，或選取其中一個 hello**執行**hello 選項**偵錯**功能表。</span><span class="sxs-lookup"><span data-stu-id="96ac7-217">Run hello package by clicking hello **Start** button on hello toolbar or by selecting one of hello **Run** options on hello **Debug** menu.</span></span>

<span data-ttu-id="96ac7-218">Hello 封裝開始 toorun，您會看到黃色旋轉滾輪 tooindicate 活動與 hello 處理資料列數目為止。</span><span class="sxs-lookup"><span data-stu-id="96ac7-218">As hello package begins toorun, you see yellow spinning wheels tooindicate activity as well as hello number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="96ac7-219">當 hello 封裝完成執行時，您看到綠色的核取記號 tooindicate 成功以及 hello 從 hello 來源 toohello 目的地載入資料的資料列總數。</span><span class="sxs-lookup"><span data-stu-id="96ac7-219">When hello package has finished running, you see green check marks tooindicate success as well as hello total number of rows of data loaded from hello source toohello destination.</span></span>

![][15]

<span data-ttu-id="96ac7-220">恭喜！</span><span class="sxs-lookup"><span data-stu-id="96ac7-220">Congratulations!</span></span> <span data-ttu-id="96ac7-221">您已成功使用 SQL Server Integration Services tooload 資料到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96ac7-221">You’ve successfully used SQL Server Integration Services tooload data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96ac7-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96ac7-222">Next steps</span></span>
* <span data-ttu-id="96ac7-223">深入了解 SSIS 資料流程 hello。</span><span class="sxs-lookup"><span data-stu-id="96ac7-223">Learn more about hello SSIS data flow.</span></span> <span data-ttu-id="96ac7-224">從這裡開始：[資料流程][Data Flow]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="96ac7-225">深入了解如何 toodebug 和疑難排解您在 hello 設計環境中的封裝權限。</span><span class="sxs-lookup"><span data-stu-id="96ac7-225">Learn how toodebug and troubleshoot your packages right in hello design environment.</span></span> <span data-ttu-id="96ac7-226">從這裡開始：[套件開發的疑難排解工具][Troubleshooting Tools for Package Development]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="96ac7-227">了解 toodeploy 您 SSIS 專案，並封裝 tooIntegration 服務伺服器或 tooanother 儲存位置。</span><span class="sxs-lookup"><span data-stu-id="96ac7-227">Learn how toodeploy your SSIS projects and packages tooIntegration Services Server or tooanother storage location.</span></span> <span data-ttu-id="96ac7-228">從這裡開始：[部署專案和套件][Deployment of Projects and Packages]。</span><span class="sxs-lookup"><span data-stu-id="96ac7-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
