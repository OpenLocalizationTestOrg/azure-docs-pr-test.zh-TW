---
title: "aaaSQL 伺服器預存程序活動"
description: "了解您可以使用 hello SQL Server 預存程序活動 tooinvoke 從 Data Factory 管線中的 Azure SQL Database 或 Azure SQL 資料倉儲的預存程序。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="52dce-103">SQL Server 預存程序活動</span><span class="sxs-lookup"><span data-stu-id="52dce-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="52dce-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="52dce-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="52dce-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="52dce-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="52dce-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="52dce-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="52dce-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="52dce-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="52dce-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="52dce-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="52dce-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="52dce-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="52dce-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="52dce-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="52dce-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="52dce-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="52dce-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="52dce-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="52dce-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="52dce-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="52dce-114">概觀</span><span class="sxs-lookup"><span data-stu-id="52dce-114">Overview</span></span>
<span data-ttu-id="52dce-115">您使用 Data Factory 中的資料轉換活動[管線](data-factory-create-pipelines.md)tootransform 和程序到預測和深入觀點的未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="52dce-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="52dce-116">hello 預存程序活動是的 Data Factory 支援的 hello 轉換活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="52dce-117">這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和 Data Factory 中的 hello 支援轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="52dce-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="52dce-118">您可以使用其中一種 hello 下列資料的預存程序儲存在您企業中或在 Azure 虛擬機器 (VM) 上的 hello 預存程序活動 tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="52dce-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="52dce-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="52dce-119">Azure SQL Database</span></span>
- <span data-ttu-id="52dce-120">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="52dce-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="52dce-121">SQL Server Database。</span><span class="sxs-lookup"><span data-stu-id="52dce-121">SQL Server Database.</span></span>  <span data-ttu-id="52dce-122">如果您使用 SQL Server 時，資料管理閘道上安裝相同機器主機 hello 資料庫，或在不同電腦上具有存取 toohello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="52dce-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="52dce-123">資料管理閘道是一套透過安全且可管理的方式，將內部部署/Azure VM 上的資料來源連結至雲端服務的元件。</span><span class="sxs-lookup"><span data-stu-id="52dce-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="52dce-124">如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。</span><span class="sxs-lookup"><span data-stu-id="52dce-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52dce-125">當將資料複製到 Azure SQL Database 或 SQL Server，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序使用 hello **sqlWriterStoredProcedureName**屬性。</span><span class="sxs-lookup"><span data-stu-id="52dce-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="52dce-126">如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="52dce-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="52dce-127">如需有關 hello 屬性的詳細資訊，請參閱下列連接器文件： [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="52dce-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="52dce-128">不支援在使用複製活動將資料複製到「Azure SQL 資料倉儲」時叫用預存程序。</span><span class="sxs-lookup"><span data-stu-id="52dce-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="52dce-129">但是，您可以使用 SQL 資料倉儲中的 hello 預存程序活動 tooinvoke 預存程序。</span><span class="sxs-lookup"><span data-stu-id="52dce-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="52dce-130">當從 Azure SQL Database 或 SQL Server 或 Azure SQL 資料倉儲中複製資料，您可以設定**SqlSource**在複製活動 tooinvoke 使用 hello hello 來源資料庫中的預存程序 tooread 資料**sqlReaderStoredProcedureName**屬性。</span><span class="sxs-lookup"><span data-stu-id="52dce-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="52dce-131">如需詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)， [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="52dce-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="52dce-132">下列逐步解說會使用 hello hello 管線 tooinvoke Azure SQL database 中的預存程序中的預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="52dce-133">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="52dce-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="52dce-134">範例資料表與預存程序</span><span class="sxs-lookup"><span data-stu-id="52dce-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="52dce-135">建立 hello 遵循**資料表**中使用 SQL Server Management Studio 或其他任何工具，您可以輕鬆地與您 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="52dce-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="52dce-136">hello datetimestamp 資料行是 hello 日期和時間時產生 hello 相對應的識別碼。</span><span class="sxs-lookup"><span data-stu-id="52dce-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="52dce-137">識別碼 hello 唯一識別但 hello datetimestamp 資料行是 hello 日期和時間時產生 hello 相對應的識別碼。</span><span class="sxs-lookup"><span data-stu-id="52dce-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![範例資料](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="52dce-139">在此範例中，hello 預存程序是在 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="52dce-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="52dce-140">Hello 預存程序是在 Azure SQL 資料倉儲和 SQL Server 資料庫中，如果 hello 方法相似。</span><span class="sxs-lookup"><span data-stu-id="52dce-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="52dce-141">對於 SQL Server 資料庫中，您必須安裝[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="52dce-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="52dce-142">建立 hello 遵循**預存程序**，將資料插入 toohello**範例資料表**。</span><span class="sxs-lookup"><span data-stu-id="52dce-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="52dce-143">**名稱**和**大小寫**hello 的參數 （在此範例中的日期時間） 必須符合的 hello 管線/活動 JSON 中指定的參數。</span><span class="sxs-lookup"><span data-stu-id="52dce-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="52dce-144">在 hello 預存程序定義中，確定 **@**  hello 參數做為前置字元。</span><span class="sxs-lookup"><span data-stu-id="52dce-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="52dce-145">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="52dce-145">Create a data factory</span></span>
1. <span data-ttu-id="52dce-146">登入太[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="52dce-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="52dce-147">按一下**新增**hello 左窗格中，按一下 **智慧 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="52dce-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="52dce-149">在 hello**新的 data factory**刀鋒視窗中，輸入**SProcDF** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="52dce-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="52dce-150">Azure Data Factory 名稱必須是**全域唯一的**。</span><span class="sxs-lookup"><span data-stu-id="52dce-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="52dce-151">您需要 tooprefix hello hello data factory 名稱與您的名稱，tooenable hello 成功建立 hello factory。</span><span class="sxs-lookup"><span data-stu-id="52dce-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="52dce-153">選取您的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="52dce-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="52dce-154">如**資源群組**，執行下列步驟的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="52dce-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="52dce-155">按一下**建立新**，然後輸入 hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="52dce-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="52dce-156">按一下 [使用現有的] 並選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="52dce-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="52dce-157">選取 hello**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="52dce-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="52dce-158">選取**Pin toodashboard** ，讓您能夠查看 hello 資料 factory hello 儀表板上登入的下一次。</span><span class="sxs-lookup"><span data-stu-id="52dce-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="52dce-159">按一下**建立**上 hello**新的 data factory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="52dce-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="52dce-160">您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="52dce-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="52dce-161">已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="52dce-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Data Factory 首頁](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="52dce-163">建立 Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="52dce-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="52dce-164">建立 hello 資料處理站之後, 您可以建立連結您的 Azure SQL 資料庫，其中包含 hello 範例資料表的資料表和 sp_sample 預存程序、 tooyour 資料處理站的 Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="52dce-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="52dce-165">按一下**作者及部署**上 hello **Data Factory**刀鋒伺服器**SProcDF** toolaunch hello Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="52dce-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="52dce-166">按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="52dce-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="52dce-167">您應該會看到 hello JSON 指令碼來建立 Azure SQL 連結服務 hello 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="52dce-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![新增資料存放區](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="52dce-169">在 hello JSON 指令碼，進行下列變更 hello:</span><span class="sxs-lookup"><span data-stu-id="52dce-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="52dce-170">取代`<servername>`hello Azure SQL Database 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="52dce-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="52dce-171">取代`<databasename>`hello 資料庫建立 hello 資料表和 hello 與預存程序。</span><span class="sxs-lookup"><span data-stu-id="52dce-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="52dce-172">取代`<username@servername>`hello 使用者帳戶具有存取 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="52dce-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="52dce-173">取代`<password>`hello hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="52dce-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![新增資料存放區](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="52dce-175">toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="52dce-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="52dce-176">確認您看到 hello AzureSqlLinkedService hello 樹狀結構中的檢視 hello 左側。</span><span class="sxs-lookup"><span data-stu-id="52dce-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="52dce-178">建立輸出資料表</span><span class="sxs-lookup"><span data-stu-id="52dce-178">Create an output dataset</span></span>
<span data-ttu-id="52dce-179">您必須指定預存程序活動的輸出資料集即使 hello 預存程序不會產生任何資料。</span><span class="sxs-lookup"><span data-stu-id="52dce-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="52dce-180">這是因為它的 hello 輸出 hello 排程 hello 活動 （頻率 hello 活動執行的每小時、 每日等） 的磁碟機的資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="52dce-181">hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="52dce-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="52dce-182">hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)hello 管線中。</span><span class="sxs-lookup"><span data-stu-id="52dce-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="52dce-183">不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="52dce-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="52dce-184">它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="52dce-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="52dce-185">在某些情況下，可以是 hello 輸出資料集**空資料集**（點 tooa 資料表實際上不會保存 hello 的輸出資料集預存程序）。</span><span class="sxs-lookup"><span data-stu-id="52dce-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="52dce-186">執行 hello toospecify hello 排程預存程序活動僅用於此空的資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="52dce-187">按一下**...多個**hello 工具列上，按一下**新的資料集**，然後按一下**Azure SQL**。</span><span class="sxs-lookup"><span data-stu-id="52dce-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="52dce-188">**新的資料集**上 hello 命令列，並選取**Azure SQL**。</span><span class="sxs-lookup"><span data-stu-id="52dce-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="52dce-190">複製/貼上下列 JSON 指令碼 toohello JSON 編輯器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="52dce-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="52dce-191">toodeploy hello 資料集，請按一下**部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="52dce-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="52dce-192">確認您看到 hello hello 樹狀檢視中的資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="52dce-194">使用 SqlServerStoredProcedure 活動建立管線</span><span class="sxs-lookup"><span data-stu-id="52dce-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="52dce-195">現在，讓我們使用預存程序活動來建立管線。</span><span class="sxs-lookup"><span data-stu-id="52dce-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="52dce-196">請注意下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="52dce-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="52dce-197">hello**類型**屬性設定太**SqlServerStoredProcedure**。</span><span class="sxs-lookup"><span data-stu-id="52dce-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="52dce-198">hello **storedProcedureName**在型別屬性設定太**sp_sample** （hello 名稱預存程序）。</span><span class="sxs-lookup"><span data-stu-id="52dce-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="52dce-199">hello **storedProcedureParameters**區段包含一個名為**DataTime**。</span><span class="sxs-lookup"><span data-stu-id="52dce-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="52dce-200">名稱和 JSON 中的 hello 參數的大小寫必須符合 hello 名稱和大小寫的 hello 預存程序定義中的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="52dce-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="52dce-201">如果您需要傳遞 null 做為參數，使用 hello 語法： `"param1": null` （全部小寫）。</span><span class="sxs-lookup"><span data-stu-id="52dce-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="52dce-202">按一下**...多個**在 hello 命令列，然後按一下**新管線**。</span><span class="sxs-lookup"><span data-stu-id="52dce-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="52dce-203">複製/貼上下列 JSON 片段 hello:</span><span class="sxs-lookup"><span data-stu-id="52dce-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="52dce-204">toodeploy hello 管線中，按一下 **部署**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="52dce-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="52dce-205">監視 hello 管線</span><span class="sxs-lookup"><span data-stu-id="52dce-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="52dce-206">按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 刀鋒視窗中，並按一下**圖表**。</span><span class="sxs-lookup"><span data-stu-id="52dce-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="52dce-208">在 hello**圖表檢視**、 看見 hello 管線的概觀，以及資料集用在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="52dce-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="52dce-210">在 hello 圖表檢視中，按兩下 hello 資料集`sprocsampleout`。</span><span class="sxs-lookup"><span data-stu-id="52dce-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="52dce-211">您會看到 hello 配量處於就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="52dce-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="52dce-212">因為每個小時 hello 開始時間和結束時間從 hello JSON 之間產生配量時，則應該是五個配量。</span><span class="sxs-lookup"><span data-stu-id="52dce-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="52dce-214">當配量處於**準備**執行狀態`select * from sampletable`hello 資料的 hello Azure SQL database tooverify 查詢 toohello 資料表中插入 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="52dce-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![輸出資料](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="52dce-216">請參閱[監視器 hello 管線](data-factory-monitor-manage-pipelines.md)監視 Azure Data Factory 管線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="52dce-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="52dce-217">指定輸入資料集</span><span class="sxs-lookup"><span data-stu-id="52dce-217">Specify an input dataset</span></span>
<span data-ttu-id="52dce-218">在 hello 逐步解說中，預存程序活動沒有任何輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="52dce-219">如果您指定的輸入資料集，hello 預存程序活動才會開始執行的輸入資料集的 hello 配量處於可用 （就緒狀態）。</span><span class="sxs-lookup"><span data-stu-id="52dce-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="52dce-220">hello 資料集可以是外部的資料集 (hello 中另一個活動不產生的同一個管線) 或上游活動 （這項活動之前執行 hello 活動） 所產生的內部資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="52dce-221">您可以指定 hello 預存程序活動的多個輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="52dce-222">如果您這樣做，hello 預存程序活動只時執行所有的 hello 輸入資料集配量中有可用 （就緒狀態）。</span><span class="sxs-lookup"><span data-stu-id="52dce-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="52dce-223">hello 輸入資料集無法取用 hello 預存程序中，做為參數。</span><span class="sxs-lookup"><span data-stu-id="52dce-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="52dce-224">起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="52dce-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="52dce-225">與其他活動鏈結</span><span class="sxs-lookup"><span data-stu-id="52dce-225">Chaining with other activities</span></span>
<span data-ttu-id="52dce-226">如果您想 toochain 上游活動與此活動，指定 hello 的 hello 上游活動的輸出做為輸入，此活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="52dce-227">當您這樣做時，hello 預存程序活動不會執行直到 hello 上游活動完成而且 hello 的 hello 上游活動的輸出資料集 （在就緒狀態）。</span><span class="sxs-lookup"><span data-stu-id="52dce-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="52dce-228">您可以指定多個上游活動的輸出資料集為 hello 預存程序活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="52dce-229">當您這樣做，hello 預存程序活動在只在所有 hello 輸入資料集配量都可用時，才執行。</span><span class="sxs-lookup"><span data-stu-id="52dce-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="52dce-230">在下列範例的 hello 的 hello 複製活動的 hello 輸出是： OutputDataset，也就是輸入 hello 的預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="52dce-231">因此，hello 預存程序活動無法執行 hello 複製活動完成，然後再 hello OutputDataset 配量處於可用 （就緒）。</span><span class="sxs-lookup"><span data-stu-id="52dce-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="52dce-232">如果您指定多個輸入資料集，hello 預存程序活動不會執行直到所有 hello 輸入資料集配量中有都可用 （就緒狀態）。</span><span class="sxs-lookup"><span data-stu-id="52dce-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="52dce-233">hello 輸入資料集不能做為參數 toohello 預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="52dce-234">如需有關將活動鏈結的詳細資訊，請參閱[管線中的多個活動](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="52dce-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="52dce-235">同樣地，toolink hello 存放區程序活動，具有**下游活動**（hello hello 預存程序活動完成後，執行），指定活動的 hello 預存程序活動與 hello 輸出資料集hello 管線中的 hello 下游活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="52dce-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52dce-236">當將資料複製到 Azure SQL Database 或 SQL Server，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序使用 hello **sqlWriterStoredProcedureName**屬性。</span><span class="sxs-lookup"><span data-stu-id="52dce-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="52dce-237">如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="52dce-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="52dce-238">如需有關 hello 屬性的詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="52dce-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="52dce-239">當從 Azure SQL Database 或 SQL Server 或 Azure SQL 資料倉儲中複製資料，您可以設定**SqlSource**在複製活動 tooinvoke 使用 hello hello 來源資料庫中的預存程序 tooread 資料**sqlReaderStoredProcedureName**屬性。</span><span class="sxs-lookup"><span data-stu-id="52dce-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="52dce-240">如需詳細資訊，請參閱下列連接器的發行項的 hello: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)， [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)， [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="52dce-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="52dce-241">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="52dce-241">JSON format</span></span>
<span data-ttu-id="52dce-242">以下是用於定義預存程序活動的 hello JSON 格式：</span><span class="sxs-lookup"><span data-stu-id="52dce-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="52dce-243">hello 下表描述這些 JSON 屬性：</span><span class="sxs-lookup"><span data-stu-id="52dce-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="52dce-244">屬性</span><span class="sxs-lookup"><span data-stu-id="52dce-244">Property</span></span> | <span data-ttu-id="52dce-245">說明</span><span class="sxs-lookup"><span data-stu-id="52dce-245">Description</span></span> | <span data-ttu-id="52dce-246">必要</span><span class="sxs-lookup"><span data-stu-id="52dce-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52dce-247">名稱</span><span class="sxs-lookup"><span data-stu-id="52dce-247">name</span></span> | <span data-ttu-id="52dce-248">Hello 活動的名稱。</span><span class="sxs-lookup"><span data-stu-id="52dce-248">Name of hello activity</span></span> |<span data-ttu-id="52dce-249">是</span><span class="sxs-lookup"><span data-stu-id="52dce-249">Yes</span></span> |
| <span data-ttu-id="52dce-250">說明</span><span class="sxs-lookup"><span data-stu-id="52dce-250">description</span></span> |<span data-ttu-id="52dce-251">描述用於 hello 活動的文字</span><span class="sxs-lookup"><span data-stu-id="52dce-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="52dce-252">否</span><span class="sxs-lookup"><span data-stu-id="52dce-252">No</span></span> |
| <span data-ttu-id="52dce-253">類型</span><span class="sxs-lookup"><span data-stu-id="52dce-253">type</span></span> | <span data-ttu-id="52dce-254">必須設定為：**SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="52dce-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="52dce-255">是</span><span class="sxs-lookup"><span data-stu-id="52dce-255">Yes</span></span> |
| <span data-ttu-id="52dce-256">輸入</span><span class="sxs-lookup"><span data-stu-id="52dce-256">inputs</span></span> | <span data-ttu-id="52dce-257">選用。</span><span class="sxs-lookup"><span data-stu-id="52dce-257">Optional.</span></span> <span data-ttu-id="52dce-258">如果您指定的輸入資料集，它必須可用 （處於 [就緒]' 的狀態） hello 預存程序活動 toorun。</span><span class="sxs-lookup"><span data-stu-id="52dce-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="52dce-259">hello 輸入資料集無法取用 hello 預存程序中，做為參數。</span><span class="sxs-lookup"><span data-stu-id="52dce-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="52dce-260">起始 hello 預存程序活動之前，它是只使用的 toocheck hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="52dce-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="52dce-261">否</span><span class="sxs-lookup"><span data-stu-id="52dce-261">No</span></span> |
| <span data-ttu-id="52dce-262">輸出</span><span class="sxs-lookup"><span data-stu-id="52dce-262">outputs</span></span> | <span data-ttu-id="52dce-263">您必須指定預存程序活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="52dce-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="52dce-264">輸出資料集指定 hello**排程**hello 預存程序活動 （每小時、 每週、 每月等）。</span><span class="sxs-lookup"><span data-stu-id="52dce-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="52dce-265">hello 輸出資料集必須使用**連結服務**參考 tooan Azure SQL Database 或 Azure SQL 資料倉儲或您想在其中 hello toorun 預存程序的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="52dce-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="52dce-266">hello 輸出資料集可以做為方法 toopass hello hello 預存程序的結果進行後續處理另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)hello 管線中。</span><span class="sxs-lookup"><span data-stu-id="52dce-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="52dce-267">不過，Data Factory 不會自動寫入預存程序 toothis 資料集的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="52dce-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="52dce-268">它是 hello 預存程序 hello 輸出資料集指向該寫入 tooa SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="52dce-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="52dce-269">在某些情況下，可以是 hello 輸出資料集**空資料集**，用僅執行 hello toospecify hello 排程預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="52dce-270">是</span><span class="sxs-lookup"><span data-stu-id="52dce-270">Yes</span></span> |
| <span data-ttu-id="52dce-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="52dce-271">storedProcedureName</span></span> |<span data-ttu-id="52dce-272">指定 hello Azure SQL database 或 Azure SQL 資料倉儲或 SQL Server 由 hello 輸出資料表中使用的 hello 連結服務的資料庫中的 hello hello 預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="52dce-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="52dce-273">是</span><span class="sxs-lookup"><span data-stu-id="52dce-273">Yes</span></span> |
| <span data-ttu-id="52dce-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="52dce-274">storedProcedureParameters</span></span> |<span data-ttu-id="52dce-275">指定預存程序參數的值。</span><span class="sxs-lookup"><span data-stu-id="52dce-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="52dce-276">如果您需要 toopass null 參數，使用 hello 語法:"param1": null （所有大小寫）。</span><span class="sxs-lookup"><span data-stu-id="52dce-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="52dce-277">請參閱下列有關使用這個屬性的範例 toolearn hello。</span><span class="sxs-lookup"><span data-stu-id="52dce-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="52dce-278">否</span><span class="sxs-lookup"><span data-stu-id="52dce-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="52dce-279">傳遞靜態值</span><span class="sxs-lookup"><span data-stu-id="52dce-279">Passing a static value</span></span>
<span data-ttu-id="52dce-280">現在，讓我們考慮 hello 資料表包含名稱為 '文件範例' 的靜態值中的 新增另一個名為 '案例' 的資料行。</span><span class="sxs-lookup"><span data-stu-id="52dce-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![範例資料 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="52dce-282">**資料表：**</span><span class="sxs-lookup"><span data-stu-id="52dce-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="52dce-283">**預存程序：**</span><span class="sxs-lookup"><span data-stu-id="52dce-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="52dce-284">現在，傳遞 hello**案例**hello 的參數和 hello 取值預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="52dce-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="52dce-285">hello **typeProperties** hello 前面範例看起來像是下列程式碼片段的 hello > 一節：</span><span class="sxs-lookup"><span data-stu-id="52dce-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="52dce-286">**Data Factory 資料集：**</span><span class="sxs-lookup"><span data-stu-id="52dce-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="52dce-287">**Data Factory 管線**</span><span class="sxs-lookup"><span data-stu-id="52dce-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```