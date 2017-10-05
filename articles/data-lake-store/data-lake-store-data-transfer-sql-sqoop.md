---
title: "使用 Sqoop 在 Data Lake Store和 Azure SQL Database 之間複製資料 | Microsoft Docs"
description: "使用 Sqoop 在 Azure SQL Database 和 Data Lake Store 之間複製資料"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="c10e8-103">使用 Sqoop 在 Data Lake Store 和 Azure SQL Database 之間複製資料</span><span class="sxs-lookup"><span data-stu-id="c10e8-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="c10e8-104">了解如何使用 Apache Sqoop 在 Azure SQL Database 和 Data Lake Store 之間匯入及匯出資料。</span><span class="sxs-lookup"><span data-stu-id="c10e8-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="c10e8-105">什麼是 Sqoop？</span><span class="sxs-lookup"><span data-stu-id="c10e8-105">What is Sqoop?</span></span>
<span data-ttu-id="c10e8-106">巨量資料應用程式是處理非結構化和半結構化資料 (例如記錄和檔案)，很自然的一個選擇。</span><span class="sxs-lookup"><span data-stu-id="c10e8-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="c10e8-107">不過，也有可能需要處理儲存在關聯式資料庫中的結構化資料。</span><span class="sxs-lookup"><span data-stu-id="c10e8-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="c10e8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) 是一個專門設計來在關聯式資料庫和巨量資料儲存機制 (例如 Data Lake Store) 之間傳送資料的工具。</span><span class="sxs-lookup"><span data-stu-id="c10e8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="c10e8-109">您可以使用它從像是 Azure SQL Database 這類的關聯式資料庫管理系統 (RDBMS)，匯入資料至 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="c10e8-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="c10e8-110">您可以使用巨量資料工作負載來轉換和分析資料，然後重新將資料匯出到 RDBMS。</span><span class="sxs-lookup"><span data-stu-id="c10e8-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="c10e8-111">在本教學課程中，您會使用 Azure SQL Database 做為匯入/匯出之來源關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="c10e8-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c10e8-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="c10e8-112">Prerequisites</span></span>
<span data-ttu-id="c10e8-113">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="c10e8-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c10e8-114">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="c10e8-114">**An Azure subscription**.</span></span> <span data-ttu-id="c10e8-115">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c10e8-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c10e8-116">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="c10e8-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="c10e8-117">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c10e8-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="c10e8-118">**Azure HDInsight 叢集** 。</span><span class="sxs-lookup"><span data-stu-id="c10e8-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="c10e8-119">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c10e8-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="c10e8-120">本文假設您已使用 Data Lake Store 存取 HDInsight Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="c10e8-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="c10e8-121">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="c10e8-121">**Azure SQL Database**.</span></span> <span data-ttu-id="c10e8-122">如需建立方式的指示，請參閱 [建立 Azure SQL Database](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c10e8-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="c10e8-123">使用影片快速學習？</span><span class="sxs-lookup"><span data-stu-id="c10e8-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="c10e8-124">[觀看這部影片](https://mix.office.com/watch/1butcdjxmu114) ，主題是關於如何使用 DistCp 在 Azure 儲存體 Blob 與 Data Lake Store 之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="c10e8-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="c10e8-125">在 Azure SQL Database 中建立範例資料表</span><span class="sxs-lookup"><span data-stu-id="c10e8-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="c10e8-126">若要開始，請在 Azure SQL Database 中建立兩個範例資料表。</span><span class="sxs-lookup"><span data-stu-id="c10e8-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="c10e8-127">使用 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 或 Visual Studio 連接至 Azure SQL Database，然後執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="c10e8-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="c10e8-128">**建立 Table1**</span><span class="sxs-lookup"><span data-stu-id="c10e8-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="c10e8-129">**建立 Table2**</span><span class="sxs-lookup"><span data-stu-id="c10e8-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="c10e8-130">在 **Table1**中，新增一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="c10e8-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="c10e8-131">保留 **Table2** 空白。</span><span class="sxs-lookup"><span data-stu-id="c10e8-131">Leave **Table2** empty.</span></span> <span data-ttu-id="c10e8-132">我們從 **Table1** 匯入資料至 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="c10e8-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="c10e8-133">然後，我們會從 Data Lake Store 將資料匯出到 **Table2**。</span><span class="sxs-lookup"><span data-stu-id="c10e8-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="c10e8-134">執行下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c10e8-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="c10e8-135">從使用 Data Lake Store 存取的 HDInsight Linux 叢集使用 Sqoop。</span><span class="sxs-lookup"><span data-stu-id="c10e8-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="c10e8-136">HDInsight 叢集已有可用的 Sqoop 套件。</span><span class="sxs-lookup"><span data-stu-id="c10e8-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="c10e8-137">如果您已設定 HDInsight 叢集使用 Data Lake Store 做為額外的儲存體，您可以使用 Sqoop (不需要任何組態變更) 在關聯式資料庫 (本範例中為 Azure SQL Database) 與 Data Lake Store 帳戶之間匯入/匯出資料。</span><span class="sxs-lookup"><span data-stu-id="c10e8-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="c10e8-138">在本教學課程中，我們假設您已經建立 Linux 叢集，因此您應該使用 SSH 來連線至叢集。</span><span class="sxs-lookup"><span data-stu-id="c10e8-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="c10e8-139">請參閱 [連線至以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c10e8-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="c10e8-140">請確認您是否可從叢集存取 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c10e8-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="c10e8-141">從 SSH 提示字元執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c10e8-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="c10e8-142">這應會提供 Data Lake Store 帳戶中的檔案/資料夾清單。</span><span class="sxs-lookup"><span data-stu-id="c10e8-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="c10e8-143">從 Azure SQL Database 將資料匯入至 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c10e8-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="c10e8-144">瀏覽至提供 Sqoop 封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="c10e8-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="c10e8-145">一般而言，這會在 `/usr/hdp/<version>/sqoop/bin`。</span><span class="sxs-lookup"><span data-stu-id="c10e8-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="c10e8-146">從 **Table1** 將資料匯入至 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="c10e8-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="c10e8-147">使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="c10e8-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="c10e8-148">請注意， **sql-database-server-name** 預留位置代表正在執行 Azure SQL Database 之伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c10e8-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="c10e8-149">**sql-database-name** 預留位置代表實際的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c10e8-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="c10e8-150">例如，</span><span class="sxs-lookup"><span data-stu-id="c10e8-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="c10e8-151">請確認資料已被傳輸至 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c10e8-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="c10e8-152">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="c10e8-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="c10e8-153">您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="c10e8-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="c10e8-154">每個 **part-m-*** 檔案會對應至來源資料表 **Table1**中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c10e8-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="c10e8-155">您可以檢視 part-m-* 檔案的內容來確認。</span><span class="sxs-lookup"><span data-stu-id="c10e8-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="c10e8-156">從 Data Lake Store 將資料匯出到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c10e8-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="c10e8-157">從 Data Lake Store 帳戶將資料匯出到 Azure SQL Database 中的空白資料表 **Table2**。</span><span class="sxs-lookup"><span data-stu-id="c10e8-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="c10e8-158">使用下列語法。</span><span class="sxs-lookup"><span data-stu-id="c10e8-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="c10e8-159">例如，</span><span class="sxs-lookup"><span data-stu-id="c10e8-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="c10e8-160">確認資料已上傳至 SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="c10e8-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="c10e8-161">使用 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 或 Visual Studio 連接至 Azure SQL Database，然後執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="c10e8-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="c10e8-162">這應該會有下列的輸出。</span><span class="sxs-lookup"><span data-stu-id="c10e8-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="c10e8-163">使用 Sqoop 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="c10e8-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="c10e8-164">關於 Sqoop 作業將資料複製到 Data Lake Store 時的效能調整，請參閱 [Sqoop 效能文件](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)。</span><span class="sxs-lookup"><span data-stu-id="c10e8-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="c10e8-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c10e8-165">See also</span></span>
* [<span data-ttu-id="c10e8-166">將資料從 Azure 儲存體 Blob 複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c10e8-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="c10e8-167">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="c10e8-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c10e8-168">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c10e8-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c10e8-169">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c10e8-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
