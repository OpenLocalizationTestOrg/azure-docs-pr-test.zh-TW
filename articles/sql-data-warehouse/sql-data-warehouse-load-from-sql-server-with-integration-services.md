---
title: "將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS) | Microsoft Docs"
description: "示範如何建立 SQL Server Integration Services (SSIS) 封裝，以將資料從各種資料來源移至 SQL 資料倉儲。"
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
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="3e37a-103">將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS)</span><span class="sxs-lookup"><span data-stu-id="3e37a-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e37a-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="3e37a-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="3e37a-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="3e37a-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="3e37a-106">bcp</span><span class="sxs-lookup"><span data-stu-id="3e37a-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="3e37a-107">建立 SQL Server Integration Services (SSIS) 來將資料從 SQL Server 載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3e37a-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-108">您可以選擇性地重建、轉換和清理通過 SSIS 資料流程傳遞的資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="3e37a-109">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="3e37a-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="3e37a-110">在 Visual Studio 中建立新的整合服務專案</span><span class="sxs-lookup"><span data-stu-id="3e37a-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="3e37a-111">連接到資料來源，包括 SQL Server (做為來源) 和 SQL 資料倉儲 (做為目的地)。</span><span class="sxs-lookup"><span data-stu-id="3e37a-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="3e37a-112">設計 SSIS 封裝，用來將資料從來源載入目的地。</span><span class="sxs-lookup"><span data-stu-id="3e37a-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="3e37a-113">執行 SSIS 封裝載入資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="3e37a-114">本教學課程中使用 SQL Server 做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="3e37a-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="3e37a-115">SQL Server 可在內部部署或在 Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="3e37a-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="3e37a-116">基本概念</span><span class="sxs-lookup"><span data-stu-id="3e37a-116">Basic concepts</span></span>
<span data-ttu-id="3e37a-117">封裝是 SSIS 的工作單位。</span><span class="sxs-lookup"><span data-stu-id="3e37a-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="3e37a-118">相關的封裝集成群組則為專案。</span><span class="sxs-lookup"><span data-stu-id="3e37a-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="3e37a-119">在 Visual Studio 中使用 SQL Server Data Tools 建立專案和設計封裝。</span><span class="sxs-lookup"><span data-stu-id="3e37a-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="3e37a-120">設計程序是視覺化的程序，您可從工具箱拖曳元件至設計介面、連接這些元件、並設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="3e37a-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="3e37a-121">完成您的封裝之後，您可以選擇性地將它部署到 SQL Server 以獲得完整管理、監視和安全性。</span><span class="sxs-lookup"><span data-stu-id="3e37a-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="3e37a-122">以 SSIS 載入資料的選項</span><span class="sxs-lookup"><span data-stu-id="3e37a-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="3e37a-123">SQL Server Integration Services (SSIS) 是彈性的工具組合，提供連接至 SQL 資料倉儲、並將資料載入 SQL 資料倉儲的各種選項。</span><span class="sxs-lookup"><span data-stu-id="3e37a-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="3e37a-124">使用「ADO NET 目的地」連接到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3e37a-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-125">本教學課程使用 ADO NET 目的地，因為它的設定選項最少。</span><span class="sxs-lookup"><span data-stu-id="3e37a-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="3e37a-126">使用「OLE DB 目的地」連接到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3e37a-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-127">此選項可能會提供比 ADO NET 目的地稍好的效能。</span><span class="sxs-lookup"><span data-stu-id="3e37a-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="3e37a-128">使用「Azure Blob 上傳」工作在 Azure Blob 儲存體中預備資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="3e37a-129">然後使用「SSIS 執行 SQL」工作來啟動可將資料載入 SQL 資料倉儲的 Polybase 指令碼。</span><span class="sxs-lookup"><span data-stu-id="3e37a-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-130">此選項提供此處所列三個選項中最佳的效能。</span><span class="sxs-lookup"><span data-stu-id="3e37a-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="3e37a-131">若要取得 Azure Blob 上傳工作，請下載[適用於 Azure 的 Microsoft SQL Server 2016 Integration Services Feature Pack][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="3e37a-132">若要深入了解 Polybase，請參閱 [PolyBase 指南][PolyBase Guide]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3e37a-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="3e37a-133">Before you start</span></span>
<span data-ttu-id="3e37a-134">若要逐步執行本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="3e37a-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="3e37a-135">**SQL Server Integration Services (SSIS)**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="3e37a-136">SSIS 是 SQL Server 的元件，需有試用版或授權版的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3e37a-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="3e37a-137">若要取得 SQL Server 2016 Preview 的試用版，請參閱 [SQL Server 試用版][SQL Server Evaluations]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="3e37a-138">**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-138">**Visual Studio**.</span></span> <span data-ttu-id="3e37a-139">若要取得免費的 Visual Studio Community Edition，請參閱 [Visual Studio Community][Visual Studio Community]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="3e37a-140">**SQL Server Data Tools for Visual Studio (SSDT)**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="3e37a-141">若要取得適用於 Visual Studio 的 SQL Server Data Tools，請參閱[下載 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="3e37a-142">**範例資料**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-142">**Sample data**.</span></span> <span data-ttu-id="3e37a-143">本教學課程會使用 AdventureWorks 範例資料庫中儲存在 SQL Server 中的範例資料，做為要載入 SQL 資料倉儲的來源資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-144">若要取得 AdventureWorks 範例資料庫，請參閱 [AdventureWorks 2014 範例資料庫][AdventureWorks 2014 Sample Databases]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="3e37a-145">**SQL 資料倉儲資料庫和權限**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="3e37a-146">本教學課程會連接到 SQL 資料倉儲執行個體，並載入資料至執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e37a-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="3e37a-147">您必須具有建立資料表以及載入資料的權限。</span><span class="sxs-lookup"><span data-stu-id="3e37a-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="3e37a-148">**防火牆規則**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-148">**A firewall rule**.</span></span> <span data-ttu-id="3e37a-149">您必須先在使用您本機電腦 IP 位址的 SQL 資料倉儲上建立防火牆規則，才您可以將資料上傳到此 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3e37a-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="3e37a-150">步驟 1：建立新的 Integration Services 專案</span><span class="sxs-lookup"><span data-stu-id="3e37a-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="3e37a-151">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3e37a-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="3e37a-152">從 [檔案] 功能表中，選取 [新增 | 專案]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="3e37a-153">瀏覽至 [安裝 |範本 |商務智慧 |整合服務]  專案類型。</span><span class="sxs-lookup"><span data-stu-id="3e37a-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="3e37a-154">選取 [整合服務專案] 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="3e37a-155">提供 [名稱] 和 [位置] 的值，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="3e37a-156">Visual Studio 隨即開啟，並建立新的整合服務 (SSIS) 專案。</span><span class="sxs-lookup"><span data-stu-id="3e37a-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="3e37a-157">然後 Visual Studio 會在專案中開啟一個新的 SSIS 封裝 (Package.dtsx) 的設計工具。</span><span class="sxs-lookup"><span data-stu-id="3e37a-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="3e37a-158">您會看到下列畫面區域：</span><span class="sxs-lookup"><span data-stu-id="3e37a-158">You see the following screen areas:</span></span>

* <span data-ttu-id="3e37a-159">左側是 SSIS 元件的 **工具箱** 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="3e37a-160">中間是設計介面，有多個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e37a-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="3e37a-161">您通常至少會使用 [控制流程] 和 [資料流程]**資料流程** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e37a-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="3e37a-162">右側是 [方案總管] 和 [屬性] 窗格。</span><span class="sxs-lookup"><span data-stu-id="3e37a-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="3e37a-163">步驟 2：建立基本資料流程</span><span class="sxs-lookup"><span data-stu-id="3e37a-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="3e37a-164">將 [資料流程工作] 從 [工具箱] 拖曳至設計介面的中心 (設計介面在 [控制流程]  索引標籤上)。</span><span class="sxs-lookup"><span data-stu-id="3e37a-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="3e37a-165">按兩下 [資料流程工作] 以切換到 [資料流程] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3e37a-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="3e37a-166">從 [工具箱] 中的 [其他來源] 清單中，將 ADO.NET 來源拖曳至設計介面。</span><span class="sxs-lookup"><span data-stu-id="3e37a-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="3e37a-167">在來源配接器仍選取的狀態下，在 [屬性] 窗格中將其名稱變更為 [SQL Server 來源]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="3e37a-168">從 [工具箱] 中的 [其他目的地] 清單中將 ADO.NET 目的地拖曳至 ADO.NET 來源下方的設計介面。</span><span class="sxs-lookup"><span data-stu-id="3e37a-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="3e37a-169">在目的地配接器仍選取的狀態下，在 [屬性] 窗格中將其名稱變更為 [SQL DW 目的地]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="3e37a-170">步驟 3︰ 設定來源配接器</span><span class="sxs-lookup"><span data-stu-id="3e37a-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="3e37a-171">按兩下來源配接器以開啟 [ADO.NET 來源編輯器] 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="3e37a-172">在 [ADO.NET 來源編輯器] 的 [連接管理員] 索引標籤上，按一下 [ADO.NET 連接管理員] 清單旁的 [新增] 按鈕開啟 [設定 ADO.NET 連接管理員] 對話方塊，並針對本教學課程會從之載入資料的 SQL Server 資料庫建立連接設定。</span><span class="sxs-lookup"><span data-stu-id="3e37a-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="3e37a-173">在 [設定 ADO.NET 連接管理員] 對話方塊中，按一下 [新增] 按鈕以開啟 [連接管理員] 對話方塊並建立新的資料連接。</span><span class="sxs-lookup"><span data-stu-id="3e37a-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="3e37a-174">在 [連接管理員]  對話方塊中，執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="3e37a-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="3e37a-175">在 [提供者] 選取 SqlClient 資料提供者。</span><span class="sxs-lookup"><span data-stu-id="3e37a-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="3e37a-176">在 [伺服器名稱] 輸入 SAP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="3e37a-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="3e37a-177">在 [登入伺服器]  區段中，選取或輸入驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="3e37a-178">在 [連接到資料庫]  區段，選取 AdventureWorksDW 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e37a-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="3e37a-179">按一下 [測試連接] 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="3e37a-180">在報告連接測試結果的對話方塊中，按一下 [確定] 以回到 [連接管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="3e37a-181">在 [連接管理員] 對話方塊中，按一下 [確定] 以回到 [設定 ADO.NET 連接管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="3e37a-182">在 [設定 ADO.NET 連接管理員] 對話方塊中，按一下 [確定] 以回到 [ADO.NET 來源編輯器]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="3e37a-183">在 [ADO.NET 來源編輯器] 的 [資料表或檢視的名稱] 清單中，選取 [Sales.SalesOrderDetail] 資料表。</span><span class="sxs-lookup"><span data-stu-id="3e37a-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="3e37a-184">按一下 [預覽] 以在 [預覽查詢結果] 對話方塊中查看來源資料表前 200 個資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="3e37a-185">在 [預覽查詢結果] 對話方塊中，按一下 [關閉] 以回到 [ADO.NET 來源編輯器]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="3e37a-186">在 [ADO.NET 來源編輯器] 中，按一下 [確定] 以完成資料來源設定。</span><span class="sxs-lookup"><span data-stu-id="3e37a-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="3e37a-187">步驟 4︰將目的地配接器連接到來源配接器</span><span class="sxs-lookup"><span data-stu-id="3e37a-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="3e37a-188">在設計介面上選取來源配接器。</span><span class="sxs-lookup"><span data-stu-id="3e37a-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="3e37a-189">選取從來源配接器延伸出來的藍色箭號，將它拖曳到目的地編輯器直到它扣住定位。</span><span class="sxs-lookup"><span data-stu-id="3e37a-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="3e37a-190">在典型 SSIS 封裝中，您可以在來源和目的地之間使用 SSIS 工具箱中的多個其他元件，在資料通過 SSIS 資料流程時重新建構、轉換、清理資料。</span><span class="sxs-lookup"><span data-stu-id="3e37a-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="3e37a-191">為了讓這個範例盡可能簡單，我們直接將來源連接到目的地。</span><span class="sxs-lookup"><span data-stu-id="3e37a-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="3e37a-192">步驟 5︰設定目的地配接器</span><span class="sxs-lookup"><span data-stu-id="3e37a-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="3e37a-193">按兩下目的地配接器開啟 [ADO.NET 目的地編輯器] 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="3e37a-194">在 [ADO.NET 目的地編輯器] 的 [連接管理員] 索引標籤上，按一下 [連接管理員] 清單旁的 [新增] 按鈕，以開啟 [設定 ADO.NET 連接管理員] 對話方塊，並針對本教學課程會將資料載入的 Azure SQL 資料倉儲資料庫建立連接設定。</span><span class="sxs-lookup"><span data-stu-id="3e37a-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="3e37a-195">在 [設定 ADO.NET 連接管理員] 對話方塊中，按一下 [新增] 按鈕以開啟 [連接管理員] 對話方塊並建立新的資料連接。</span><span class="sxs-lookup"><span data-stu-id="3e37a-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="3e37a-196">在 [連接管理員]  對話方塊中，執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="3e37a-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="3e37a-197">在 [提供者] 選取 SqlClient 資料提供者。</span><span class="sxs-lookup"><span data-stu-id="3e37a-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="3e37a-198">在 [伺服器名稱] 輸入 SQL 資料倉儲名稱。</span><span class="sxs-lookup"><span data-stu-id="3e37a-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="3e37a-199">在 [登入伺服器] 區段，選取 [使用 SQL Server 驗證] 並輸入驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="3e37a-200">在 [連接到資料庫]  區段，選取現有的 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e37a-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="3e37a-201">按一下 [測試連接] 。</span><span class="sxs-lookup"><span data-stu-id="3e37a-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="3e37a-202">在報告連接測試結果的對話方塊中，按一下 [確定] 以回到 [連接管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="3e37a-203">在 [連接管理員] 對話方塊中，按一下 [確定] 以回到 [設定 ADO.NET 連接管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3e37a-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="3e37a-204">在 [設定 ADO.NET 連接管理員] 對話方塊中，按一下 [確定] 以回到 [ADO.NET 目的地編輯器]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="3e37a-205">在 [ADO.NET 目的地編輯器] 中，按一下 [使用資料表或檢視] 清單旁的 [新增] 按鈕以開啟 [建立資料表] 對話方塊，建立具有符合來源資料表之資料行清單的新目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="3e37a-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="3e37a-206">在 [建立資料表]  對話方塊中，執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="3e37a-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="3e37a-207">將目的地資料表的名稱變更為 **SalesOrderDetail**。</span><span class="sxs-lookup"><span data-stu-id="3e37a-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="3e37a-208">移除 **rowguid** 資料行。</span><span class="sxs-lookup"><span data-stu-id="3e37a-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="3e37a-209">SQL 資料倉儲不支援 **uniqueidentifier** 資料類型。</span><span class="sxs-lookup"><span data-stu-id="3e37a-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="3e37a-210">將 **LineTotal** 資料行的資料類型變更為 [money]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="3e37a-211">SQL 資料倉儲不支援 **decimal** 資料類型。</span><span class="sxs-lookup"><span data-stu-id="3e37a-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="3e37a-212">如需支援的資料類型資訊，請參閱[建立資料表 (Azure SQL 資料倉儲，平行資料倉儲)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="3e37a-213">按一下 [確定] 以建立資料表，並回到 [ADO.NET 目的地編輯器]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="3e37a-214">在 [ADO.NET 目的地編輯器] 中選取 [對應] 索引標籤，以查看來源資料行對應到目的地資料行的方式。</span><span class="sxs-lookup"><span data-stu-id="3e37a-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="3e37a-215">按一下 [確定]  完成資料來源設定。</span><span class="sxs-lookup"><span data-stu-id="3e37a-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="3e37a-216">步驟 6︰執行封裝以載入資料</span><span class="sxs-lookup"><span data-stu-id="3e37a-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="3e37a-217">按一下工具列上的 [開始] 按鈕，或選取 [偵錯] 功能表上其中一個 [執行] 選項以執行封裝。</span><span class="sxs-lookup"><span data-stu-id="3e37a-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="3e37a-218">當封裝開始執行時，您會看到用來表示活動的黃色旋轉滾輪以及目前已處理的資料列數。</span><span class="sxs-lookup"><span data-stu-id="3e37a-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="3e37a-219">封裝執行完成時，您會看到用來表示成功的綠色打勾記號，以及從來源載入到目的地的資料列總數。</span><span class="sxs-lookup"><span data-stu-id="3e37a-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="3e37a-220">恭喜！</span><span class="sxs-lookup"><span data-stu-id="3e37a-220">Congratulations!</span></span> <span data-ttu-id="3e37a-221">您已使用 SQL Server Integration Services 成功將資料載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3e37a-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e37a-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e37a-222">Next steps</span></span>
* <span data-ttu-id="3e37a-223">深入了解 SSIS 資料流程。</span><span class="sxs-lookup"><span data-stu-id="3e37a-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="3e37a-224">從這裡開始：[資料流程][Data Flow]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="3e37a-225">了解如何在設計環境中進行封裝的偵錯和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3e37a-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="3e37a-226">從這裡開始：[套件開發的疑難排解工具][Troubleshooting Tools for Package Development]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="3e37a-227">了解如何將 SSIS 專案和封裝部署到 Integration Services 伺服器或其他儲存位置。</span><span class="sxs-lookup"><span data-stu-id="3e37a-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="3e37a-228">從這裡開始：[部署專案和套件][Deployment of Projects and Packages]。</span><span class="sxs-lookup"><span data-stu-id="3e37a-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

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
