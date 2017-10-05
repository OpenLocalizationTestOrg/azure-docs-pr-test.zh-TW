---
title: "SQL Server 預存程序活動"
description: "深入了解如何使用 SQL Server 預存程序活動，以從 Data Factory 管線叫用 Azure SQL Database 或 Azure SQL 資料倉儲中的預存程序。"
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="30e04-103">SQL Server 預存程序活動</span><span class="sxs-lookup"><span data-stu-id="30e04-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="30e04-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="30e04-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="30e04-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="30e04-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="30e04-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="30e04-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="30e04-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="30e04-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="30e04-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="30e04-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="30e04-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="30e04-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="30e04-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="30e04-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="30e04-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="30e04-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="30e04-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="30e04-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="30e04-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="30e04-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="30e04-114">概觀</span><span class="sxs-lookup"><span data-stu-id="30e04-114">Overview</span></span>
<span data-ttu-id="30e04-115">您在 Data Factory [管線](data-factory-create-pipelines.md)中使用資料轉換活動，以轉換和處理您的原始資料以進行預測和深入了解。</span><span class="sxs-lookup"><span data-stu-id="30e04-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="30e04-116">預存程序活動是 Data Factory 支援的其中一個轉換活動。</span><span class="sxs-lookup"><span data-stu-id="30e04-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="30e04-117">本文是以[資料轉換活動](data-factory-data-transformation-activities.md)一文為基礎，提供 Data Factory 中資料轉換及所支援轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="30e04-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="30e04-118">您可以使用「預存程序活動」來叫用您企業或 Azure 虛擬機器 (VM) 中的下列其中一個資料存放區：</span><span class="sxs-lookup"><span data-stu-id="30e04-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="30e04-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="30e04-119">Azure SQL Database</span></span>
- <span data-ttu-id="30e04-120">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="30e04-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="30e04-121">SQL Server Database。</span><span class="sxs-lookup"><span data-stu-id="30e04-121">SQL Server Database.</span></span>  <span data-ttu-id="30e04-122">如果您使用 SQL Server，請在裝載資料庫的同一部電腦上或可存取資料庫的個別電腦上安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="30e04-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="30e04-123">資料管理閘道是一套透過安全且可管理的方式，將內部部署/Azure VM 上的資料來源連結至雲端服務的元件。</span><span class="sxs-lookup"><span data-stu-id="30e04-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="30e04-124">如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。</span><span class="sxs-lookup"><span data-stu-id="30e04-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30e04-125">將資料複製到 Azure SQL Database 或 SQL Server 時，您可以使用 **sqlWriterStoredProcedureName** 屬性在複製活動中設定 **SqlSink** 以叫用預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="30e04-126">如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="30e04-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="30e04-127">如需有關此屬性的詳細資料，請參閱下列連接器文章：[Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)、[SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="30e04-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="30e04-128">不支援在使用複製活動將資料複製到「Azure SQL 資料倉儲」時叫用預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="30e04-129">但是，您可以使用預存程序活動來叫用「SQL 資料倉儲」中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="30e04-130">從 Azure SQL Database、SQL Server 或「Azure SQL 資料倉儲」複製資料時，您可以使用 **sqlReaderStoredProcedureName** 屬性在複製活動中設定 **SqlSource**，以叫用預存程序從來源資料庫讀取資料。</span><span class="sxs-lookup"><span data-stu-id="30e04-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="30e04-131">如需詳細資訊，請參閱下列連接器文章：[Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)、[SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)、[Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="30e04-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="30e04-132">下列逐步解說會在管線中使用預存程序活動，來叫用 Azure SQL Database 中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="30e04-133">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="30e04-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="30e04-134">範例資料表與預存程序</span><span class="sxs-lookup"><span data-stu-id="30e04-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="30e04-135">在您的 Azure SQL Database 中，使用 SQL Server Management Studio 或任何其他您很熟悉的工具，來建立下列 **資料表** 。</span><span class="sxs-lookup"><span data-stu-id="30e04-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="30e04-136">Datetimestamp 資料行是產生對應識別碼的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="30e04-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="30e04-137">Id 是可唯一識別的，而 datetimestamp 資料行是產生對應識別碼的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="30e04-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![範例資料](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="30e04-139">在此範例中，預存程序在 Azure SQL Database 中。</span><span class="sxs-lookup"><span data-stu-id="30e04-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="30e04-140">如果預存程序是在 Azure SQL 資料倉儲和 SQL Server Database 中，此方式是類似的。</span><span class="sxs-lookup"><span data-stu-id="30e04-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="30e04-141">對於 SQL Server 資料庫中，您必須安裝[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="30e04-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="30e04-142">建立下列**預存程序**，將資料插入 **sampletable**。</span><span class="sxs-lookup"><span data-stu-id="30e04-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="30e04-143">參數 (在此範例中是 DateTime) 的**名稱**和**大小寫**必須與下列管線/活動 JSON 中指定的參數相符。</span><span class="sxs-lookup"><span data-stu-id="30e04-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="30e04-144">在預存程序定義中，請務必使用 **@** 做為參數前置詞。</span><span class="sxs-lookup"><span data-stu-id="30e04-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="30e04-145">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="30e04-145">Create a data factory</span></span>
1. <span data-ttu-id="30e04-146">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="30e04-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="30e04-147">按一下左側功能表上的 [新增]、[資料 + 分析]，再按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="30e04-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="30e04-149">在 [新增 Data Factory] 刀鋒視窗中，輸入 **SProcDF** 做為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="30e04-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="30e04-150">Azure Data Factory 名稱必須是**全域唯一的**。</span><span class="sxs-lookup"><span data-stu-id="30e04-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="30e04-151">您必須在 Data Factory 的名稱前面加上您的名稱，才能成功建立 Factory。</span><span class="sxs-lookup"><span data-stu-id="30e04-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![新增 Data Factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="30e04-153">選取您的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="30e04-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="30e04-154">針對**資源群組**，請執行下列其中一個步驟︰</span><span class="sxs-lookup"><span data-stu-id="30e04-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="30e04-155">按一下 [新建] 並輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="30e04-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="30e04-156">按一下 [使用現有的] 並選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="30e04-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="30e04-157">選取 Data Factory 的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="30e04-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="30e04-158">選取 [釘選到儀表板]，讓您下一次登入時可以在儀表板上看到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="30e04-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="30e04-159">按一下 [新增 Data Factory] 刀鋒視窗上的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="30e04-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="30e04-160">您會看到 Data Factory 建立在 Azure 入口網站的 [儀表板] 中。</span><span class="sxs-lookup"><span data-stu-id="30e04-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="30e04-161">在 Data Factory 成功建立後，您會看到 Data Factory 頁面，顯示 Data Factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="30e04-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory 首頁](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="30e04-163">建立 Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="30e04-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="30e04-164">建立 Data Factory 之後，您需建立 Azure SQL 已連結服務，將包含 sampletable 資料表和 sp_sample 預存程序的 Azure SQL Database 連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="30e04-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="30e04-165">在 **SProcDF** 的 [Data Factory] 刀鋒視窗上，按一下 [製作和部署] 來啟動 Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="30e04-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="30e04-166">在命令列上按一下 [新增資料儲存區]，然後選擇 [Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="30e04-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="30e04-167">您應該會在編輯器中看到用來建立 Azure SQL 連結服務的 JSON 指令碼。</span><span class="sxs-lookup"><span data-stu-id="30e04-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![新增資料存放區](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="30e04-169">在 JSON 指令碼中，進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="30e04-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="30e04-170">以 Azure SQL Database 伺服器的名稱取代 `<servername>`。</span><span class="sxs-lookup"><span data-stu-id="30e04-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="30e04-171">以建立資料表和預存程序的資料庫取代 `<databasename>`。</span><span class="sxs-lookup"><span data-stu-id="30e04-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="30e04-172">以具有資料庫存取權的使用者帳戶取代 `<username@servername>`。</span><span class="sxs-lookup"><span data-stu-id="30e04-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="30e04-173">以使用者帳戶的密碼取代 `<password>`。</span><span class="sxs-lookup"><span data-stu-id="30e04-173">Replace `<password>` with the password for the user account.</span></span>

      ![新增資料存放區](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="30e04-175">若要部署連結服務，請按一下命令列的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="30e04-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="30e04-176">在左側的樹狀檢視中確認您已看到 AzureSqlLinkedService。</span><span class="sxs-lookup"><span data-stu-id="30e04-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="30e04-178">建立輸出資料表</span><span class="sxs-lookup"><span data-stu-id="30e04-178">Create an output dataset</span></span>
<span data-ttu-id="30e04-179">即使預存程序不會產生任何資料，您也必須為預存程序活動指定輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="30e04-180">這是因為輸出資料集會驅動活動排程 (活動的執行頻率 - 每小時、每天等)。</span><span class="sxs-lookup"><span data-stu-id="30e04-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="30e04-181">輸出資料集必須使用參考了想在其中執行預存程序之 Azure SQL Database、Azure SQL 資料倉儲或 SQL Server Database 的 **連結服務** 。</span><span class="sxs-lookup"><span data-stu-id="30e04-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="30e04-182">輸出資料集可以用來傳遞預存程序結果，以供管線中的另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) 進行後續處理。</span><span class="sxs-lookup"><span data-stu-id="30e04-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="30e04-183">不過，Data Factory 不會自動將預存程序的輸出寫入至此資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="30e04-184">它是會寫入至輸出資料集所指向之 SQL 資料表的預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="30e04-185">在某些情況下，輸出資料集可以是「虛擬資料集」(此資料集指向並未真正存有預存程序輸出資料的資料表)。</span><span class="sxs-lookup"><span data-stu-id="30e04-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="30e04-186">此虛擬資料集僅用來指定用於執行預存程序活動的排程。</span><span class="sxs-lookup"><span data-stu-id="30e04-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="30e04-187">按一下 **...更多** (工具列上)，按一下 新增資料集，然後按一下 Azure SQL。</span><span class="sxs-lookup"><span data-stu-id="30e04-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="30e04-188">命令列的 [新資料集]，然後選取 [Azure SQL]。</span><span class="sxs-lookup"><span data-stu-id="30e04-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="30e04-190">將下列 JSON 指令碼複製/貼到 JSON 編輯器。</span><span class="sxs-lookup"><span data-stu-id="30e04-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="30e04-191">若要部署資料集，請按一下命令列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="30e04-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="30e04-192">確認您已在樹狀檢視中看到該資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-192">Confirm that you see the dataset in the tree view.</span></span>

    ![含連結服務的樹狀檢視](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="30e04-194">使用 SqlServerStoredProcedure 活動建立管線</span><span class="sxs-lookup"><span data-stu-id="30e04-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="30e04-195">現在，讓我們使用預存程序活動來建立管線。</span><span class="sxs-lookup"><span data-stu-id="30e04-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="30e04-196">請注意下列屬性：</span><span class="sxs-lookup"><span data-stu-id="30e04-196">Notice the following properties:</span></span> 

- <span data-ttu-id="30e04-197">**type** 屬性會設定為 **SqlServerStoredProcedure**。</span><span class="sxs-lookup"><span data-stu-id="30e04-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="30e04-198">類型屬性中的 **storedProcedureName** 會設定為 **sp_sample** (預存程序的名稱)。</span><span class="sxs-lookup"><span data-stu-id="30e04-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="30e04-199">**storedProcedureParameters** 區段包含一個名為 **DataTime** 的參數。</span><span class="sxs-lookup"><span data-stu-id="30e04-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="30e04-200">JSON 中參數的名稱和大小寫必須符合預存程序定義中參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="30e04-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="30e04-201">如果您需要為參數傳遞 null，請使用此語法：`"param1": null` (全部小寫)。</span><span class="sxs-lookup"><span data-stu-id="30e04-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="30e04-202">按一下 **...命令列上的 [更多]**，然後按一下 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="30e04-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="30e04-203">複製/貼上下列 JSON 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="30e04-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="30e04-204">若要部署管線，請按一下工具列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="30e04-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="30e04-205">監視管線</span><span class="sxs-lookup"><span data-stu-id="30e04-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="30e04-206">按一下 **X** 以關閉 [Data Factory 編輯器] 刀鋒視窗、瀏覽回 [Data Factory] 刀鋒視窗，然後按一下 [圖表]。</span><span class="sxs-lookup"><span data-stu-id="30e04-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="30e04-208">在 [圖表檢視] 中，您會看到管線的概觀，以及在本教學課程中使用的資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="30e04-210">在 [圖表檢視] 中，按兩下 `sprocsampleout` 資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="30e04-211">您會看到就緒狀態的配量。</span><span class="sxs-lookup"><span data-stu-id="30e04-211">You see the slices in Ready state.</span></span> <span data-ttu-id="30e04-212">由於配量是針對 JSON 的開始時間和結束時間之間的每一個小時所產生，因此，應該會有 5 個配量。</span><span class="sxs-lookup"><span data-stu-id="30e04-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![圖表圖格](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="30e04-214">當配量處於**就緒**狀態時，請對 Azure SQL Database 執行 `select * from sampletable` 查詢，以驗證預存程序已將資料插入資料表。</span><span class="sxs-lookup"><span data-stu-id="30e04-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![輸出資料](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="30e04-216">如需監視 Azure Data Factory 管線的詳細資訊，請參閱 [監視管線](data-factory-monitor-manage-pipelines.md) 。</span><span class="sxs-lookup"><span data-stu-id="30e04-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="30e04-217">指定輸入資料集</span><span class="sxs-lookup"><span data-stu-id="30e04-217">Specify an input dataset</span></span>
<span data-ttu-id="30e04-218">在本逐步解說中，預存程序活動沒有任何輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="30e04-219">如果您指定輸入資料集，則預存程序活動將會等到輸入資料集配量可供使用 (處於「就緒」狀態) 之後，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="30e04-220">此資料集可以是外部資料集 (不是由相同管線中的另一個活動所產生)，也可以是上游活動 (執行順序在此活動之前的活動) 所產生的內部資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="30e04-221">您可以為預存程序活動指定多個輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="30e04-222">如果您這麼做，預存程序活動將只會在所有輸入資料集配量都可供使用 (處於「就緒」狀態) 時，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="30e04-223">在預存程序中輸入資料集無法做為參數取用。</span><span class="sxs-lookup"><span data-stu-id="30e04-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="30e04-224">它只會用來在啟動預存程序活動之前檢查相依性。</span><span class="sxs-lookup"><span data-stu-id="30e04-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="30e04-225">與其他活動鏈結</span><span class="sxs-lookup"><span data-stu-id="30e04-225">Chaining with other activities</span></span>
<span data-ttu-id="30e04-226">如果您想要將此活動與上游活動進行鏈結，請指定上游活動的輸出作為此活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="30e04-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="30e04-227">當您這麼做時，預存程序活動將會等到上游活動完成且上游活動的輸出資料集可供使用 (處於「就緒」狀態) 之後，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="30e04-228">您可以指定多個上游活動的輸出資料集作為預存程序活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="30e04-229">如果您這麼做，預存程序活動將只會在所有輸入資料集配量都可供使用時，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="30e04-230">在下列範例中，複製活動的輸出是 OutputDataset，這是預存程序活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="30e04-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="30e04-231">因此，預存程序活動將會等到複製活動完成且 OutputDataset 配量可供使用 (處於「就緒」狀態) 之後，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="30e04-232">如果您指定多個輸入資料集，則預存程序活動將會等到所有輸入資料集配量都可供使用 (處於「就緒」狀態) 之後，才會執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="30e04-233">輸入資料集無法直接用來作為預存程序活動的參數。</span><span class="sxs-lookup"><span data-stu-id="30e04-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="30e04-234">如需有關將活動鏈結的詳細資訊，請參閱[管線中的多個活動](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="30e04-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="30e04-235">同樣地，若要將預存程序活動與「下游活動」(執行順序在預存程序活動之後的活動) 連結，請在管線中指定預存程序活動的輸出資料集作為下游活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="30e04-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30e04-236">將資料複製到 Azure SQL Database 或 SQL Server 時，您可以使用 **sqlWriterStoredProcedureName** 屬性在複製活動中設定 **SqlSink** 以叫用預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="30e04-237">如需詳細資訊，請參閱[從複製活動叫用預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="30e04-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="30e04-238">如需有關此屬性的詳細資料，請參閱下列連接器文章：[Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)、[SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="30e04-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="30e04-239">從 Azure SQL Database、SQL Server 或「Azure SQL 資料倉儲」複製資料時，您可以使用 **sqlReaderStoredProcedureName** 屬性在複製活動中設定 **SqlSource**，以叫用預存程序從來源資料庫讀取資料。</span><span class="sxs-lookup"><span data-stu-id="30e04-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="30e04-240">如需詳細資訊，請參閱下列連接器文章：[Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties)、[SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)、[Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="30e04-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="30e04-241">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="30e04-241">JSON format</span></span>
<span data-ttu-id="30e04-242">以下是 JSON 格式來定義預存程序活動︰</span><span class="sxs-lookup"><span data-stu-id="30e04-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="30e04-243">下表說明這些 JSON 屬性：</span><span class="sxs-lookup"><span data-stu-id="30e04-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="30e04-244">屬性</span><span class="sxs-lookup"><span data-stu-id="30e04-244">Property</span></span> | <span data-ttu-id="30e04-245">說明</span><span class="sxs-lookup"><span data-stu-id="30e04-245">Description</span></span> | <span data-ttu-id="30e04-246">必要</span><span class="sxs-lookup"><span data-stu-id="30e04-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30e04-247">名稱</span><span class="sxs-lookup"><span data-stu-id="30e04-247">name</span></span> | <span data-ttu-id="30e04-248">活動的名稱</span><span class="sxs-lookup"><span data-stu-id="30e04-248">Name of the activity</span></span> |<span data-ttu-id="30e04-249">是</span><span class="sxs-lookup"><span data-stu-id="30e04-249">Yes</span></span> |
| <span data-ttu-id="30e04-250">說明</span><span class="sxs-lookup"><span data-stu-id="30e04-250">description</span></span> |<span data-ttu-id="30e04-251">說明活動用途的文字</span><span class="sxs-lookup"><span data-stu-id="30e04-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="30e04-252">否</span><span class="sxs-lookup"><span data-stu-id="30e04-252">No</span></span> |
| <span data-ttu-id="30e04-253">類型</span><span class="sxs-lookup"><span data-stu-id="30e04-253">type</span></span> | <span data-ttu-id="30e04-254">必須設定為：**SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="30e04-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="30e04-255">是</span><span class="sxs-lookup"><span data-stu-id="30e04-255">Yes</span></span> |
| <span data-ttu-id="30e04-256">輸入</span><span class="sxs-lookup"><span data-stu-id="30e04-256">inputs</span></span> | <span data-ttu-id="30e04-257">選用。</span><span class="sxs-lookup"><span data-stu-id="30e04-257">Optional.</span></span> <span data-ttu-id="30e04-258">如果您有指定輸入資料集，它必須可供使用 (「就緒」狀態)，預存程序活動才能執行。</span><span class="sxs-lookup"><span data-stu-id="30e04-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="30e04-259">在預存程序中輸入資料集無法做為參數取用。</span><span class="sxs-lookup"><span data-stu-id="30e04-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="30e04-260">它只會用來在啟動預存程序活動之前檢查相依性。</span><span class="sxs-lookup"><span data-stu-id="30e04-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="30e04-261">否</span><span class="sxs-lookup"><span data-stu-id="30e04-261">No</span></span> |
| <span data-ttu-id="30e04-262">輸出</span><span class="sxs-lookup"><span data-stu-id="30e04-262">outputs</span></span> | <span data-ttu-id="30e04-263">您必須指定預存程序活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="30e04-264">輸出資料集會指定預存程序活動的 **排程** (每小時、每週、每月等)。</span><span class="sxs-lookup"><span data-stu-id="30e04-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="30e04-265">輸出資料集必須使用參考了想在其中執行預存程序之 Azure SQL Database、Azure SQL 資料倉儲或 SQL Server Database 的 **連結服務** 。</span><span class="sxs-lookup"><span data-stu-id="30e04-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="30e04-266">輸出資料集可以用來傳遞預存程序結果，以供管線中的另一個活動 ([鏈結活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) 進行後續處理。</span><span class="sxs-lookup"><span data-stu-id="30e04-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="30e04-267">不過，Data Factory 不會自動將預存程序的輸出寫入至此資料集。</span><span class="sxs-lookup"><span data-stu-id="30e04-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="30e04-268">它是會寫入至輸出資料集所指向之 SQL 資料表的預存程序。</span><span class="sxs-lookup"><span data-stu-id="30e04-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="30e04-269">在某些情況下，輸出資料集可以是 **虛擬資料集**，只會用來指定用於執行預存程序活動的排程。</span><span class="sxs-lookup"><span data-stu-id="30e04-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="30e04-270">是</span><span class="sxs-lookup"><span data-stu-id="30e04-270">Yes</span></span> |
| <span data-ttu-id="30e04-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="30e04-271">storedProcedureName</span></span> |<span data-ttu-id="30e04-272">指定 Azure SQL Database、「Azure SQL 資料倉儲」或 SQL Server 資料庫中預存程序 (由輸出資料表所使用的已連結服務代表) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="30e04-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="30e04-273">是</span><span class="sxs-lookup"><span data-stu-id="30e04-273">Yes</span></span> |
| <span data-ttu-id="30e04-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="30e04-274">storedProcedureParameters</span></span> |<span data-ttu-id="30e04-275">指定預存程序參數的值。</span><span class="sxs-lookup"><span data-stu-id="30e04-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="30e04-276">如果您要為參數傳遞 null，請使用語法："param1": null (全部小寫)。</span><span class="sxs-lookup"><span data-stu-id="30e04-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="30e04-277">請參閱下列範例以了解如何使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="30e04-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="30e04-278">否</span><span class="sxs-lookup"><span data-stu-id="30e04-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="30e04-279">傳遞靜態值</span><span class="sxs-lookup"><span data-stu-id="30e04-279">Passing a static value</span></span>
<span data-ttu-id="30e04-280">現在我們來考量在包含稱為「文件範例」的靜態值的資料表中，新增另一個名為「案例」的資料行。</span><span class="sxs-lookup"><span data-stu-id="30e04-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![範例資料 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="30e04-282">**資料表：**</span><span class="sxs-lookup"><span data-stu-id="30e04-282">**Table:**</span></span>

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

<span data-ttu-id="30e04-283">**預存程序：**</span><span class="sxs-lookup"><span data-stu-id="30e04-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="30e04-284">現在，從預存程序活動傳遞**案例**參數和值。</span><span class="sxs-lookup"><span data-stu-id="30e04-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="30e04-285">在前述範例中，**typeProperties** 區段看起來像下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="30e04-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="30e04-286">**Data Factory 資料集：**</span><span class="sxs-lookup"><span data-stu-id="30e04-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="30e04-287">**Data Factory 管線**</span><span class="sxs-lookup"><span data-stu-id="30e04-287">**Data Factory pipeline**</span></span>

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