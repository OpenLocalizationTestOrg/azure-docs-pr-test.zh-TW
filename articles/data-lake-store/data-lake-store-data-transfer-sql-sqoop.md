---
title: "資料湖存放區和 Sqoop Azure SQL database 之間的 aaaCopy 資料 |Microsoft 文件"
description: "使用 Azure SQL Database 與資料湖存放區之間的 Sqoop toocopy 資料"
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
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="e2aa1-103">使用 Sqoop 在 Data Lake Store 和 Azure SQL Database 之間複製資料</span><span class="sxs-lookup"><span data-stu-id="e2aa1-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="e2aa1-104">深入了解如何 toouse Apache Sqoop tooimport 和匯出資料與 Azure SQL Database 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="e2aa1-105">什麼是 Sqoop？</span><span class="sxs-lookup"><span data-stu-id="e2aa1-105">What is Sqoop?</span></span>
<span data-ttu-id="e2aa1-106">巨量資料應用程式是處理非結構化和半結構化資料 (例如記錄和檔案)，很自然的一個選擇。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="e2aa1-107">不過，可能也有需要 tooprocess 結構化資料儲存在關聯式資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="e2aa1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html)是設計工具 tootransfer 關聯式資料庫和巨量資料儲存機制，例如資料湖存放區之間的資料。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="e2aa1-109">您可以使用它從關聯式資料庫管理系統 (RDBMS) 例如 Azure SQL Database 的 tooimport 資料至資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="e2aa1-110">您可以再轉換和分析使用巨量資料工作負載的 hello 資料然後回 RDBMS 匯出 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="e2aa1-111">在本教學課程中，您可以使用 Azure SQL Database 為您關聯式資料庫 tooimport/從匯出。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2aa1-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="e2aa1-112">Prerequisites</span></span>
<span data-ttu-id="e2aa1-113">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e2aa1-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e2aa1-114">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-114">**An Azure subscription**.</span></span> <span data-ttu-id="e2aa1-115">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e2aa1-116">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="e2aa1-117">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e2aa1-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="e2aa1-118">**Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="e2aa1-119">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="e2aa1-120">本文假設您已使用 Data Lake Store 存取 HDInsight Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="e2aa1-121">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-121">**Azure SQL Database**.</span></span> <span data-ttu-id="e2aa1-122">如需有關指示 toocreate 一個，請參閱[建立 Azure SQL database](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e2aa1-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="e2aa1-123">使用影片快速學習？</span><span class="sxs-lookup"><span data-stu-id="e2aa1-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="e2aa1-124">[觀賞此視訊](https://mix.office.com/watch/1butcdjxmu114)如何與 Azure 儲存體 Blob 資料湖存放區使用 DistCp toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="e2aa1-125">在 hello Azure SQL Database 中建立範例資料表</span><span class="sxs-lookup"><span data-stu-id="e2aa1-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="e2aa1-126">toostart，hello Azure SQL Database 中建立兩個範例資料表。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="e2aa1-127">使用[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)或 Visual Studio tooconnect toohello Azure SQL Database 執行的 hello 然後遵從查詢。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="e2aa1-128">**建立 Table1**</span><span class="sxs-lookup"><span data-stu-id="e2aa1-128">**Create Table1**</span></span>

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

    <span data-ttu-id="e2aa1-129">**建立 Table2**</span><span class="sxs-lookup"><span data-stu-id="e2aa1-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="e2aa1-130">在 **Table1**中，新增一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="e2aa1-131">保留 **Table2** 空白。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-131">Leave **Table2** empty.</span></span> <span data-ttu-id="e2aa1-132">我們從 **Table1** 匯入資料至 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="e2aa1-133">然後，我們會從 Data Lake Store 將資料匯出到 **Table2**。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="e2aa1-134">執行下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="e2aa1-135">從與 HDInsight 叢集使用 Sqoop 存取 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="e2aa1-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="e2aa1-136">HDInsight 叢集已有可用的 hello Sqoop 封裝。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="e2aa1-137">如果您已設定 hello HDInsight 叢集 toouse 資料湖存放區做為額外的存放裝置，您可以使用關聯式資料庫 （在此範例中，Azure SQL Database） 之間 （不含任何組態變更） 的 Sqoop tooimport/匯出資料和資料湖存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="e2aa1-138">此教學課程中，我們假設您建立 Linux 叢集，因此您應該使用 SSH tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="e2aa1-139">請參閱[連接 tooa 以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="e2aa1-140">請確認您是否可以從 hello 叢集存取 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="e2aa1-141">執行 hello hello SSH 提示字元中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="e2aa1-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="e2aa1-142">這樣應該會提供一份 hello Data Lake Store 帳戶中的檔案/資料夾。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="e2aa1-143">從 Azure SQL Database 將資料匯入至 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e2aa1-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="e2aa1-144">瀏覽 toohello 目錄有可用 Sqoop 封裝。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="e2aa1-145">一般而言，這會在 `/usr/hdp/<version>/sqoop/bin`。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="e2aa1-146">Hello 資料匯入**Table1**到 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="e2aa1-147">使用下列語法的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2aa1-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="e2aa1-148">請注意， **sql 資料庫的伺服器名稱**預留位置代表 hello hello hello Azure SQL 資料庫正在執行的伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="e2aa1-149">**sql 資料庫名稱**預留位置代表 hello 實際資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="e2aa1-150">例如，</span><span class="sxs-lookup"><span data-stu-id="e2aa1-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="e2aa1-151">確認資料已該 hello 轉移 toohello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="e2aa1-152">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2aa1-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="e2aa1-153">您應該會看到下列輸出的 hello。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="e2aa1-154">每個**一部分-m-*** 檔案對應 tooa hello 來源資料表中的資料列**Table1**。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="e2aa1-155">您可以檢視 hello 內容 hello 組件-m-* 檔案 tooverify。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="e2aa1-156">從 Data Lake Store 將資料匯出到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e2aa1-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="e2aa1-157">Data Lake Store 帳戶 toohello 空白資料表，從匯出 hello 資料**Table2**，hello Azure SQL Database 中。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="e2aa1-158">使用下列語法的 hello。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="e2aa1-159">例如，</span><span class="sxs-lookup"><span data-stu-id="e2aa1-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="e2aa1-160">請確認該 hello 資料已上傳 toohello SQL Database 的資料表。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="e2aa1-161">使用[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)或 Visual Studio tooconnect toohello Azure SQL Database 執行的 hello 然後遵從查詢。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="e2aa1-162">這應該 hello 遵循輸出。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="e2aa1-163">使用 Sqoop 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="e2aa1-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="e2aa1-164">如需效能微調您的 Sqoop 工作 toocopy 資料 tooData 湖存放區，請參閱[Sqoop 效能文件](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)。</span><span class="sxs-lookup"><span data-stu-id="e2aa1-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="e2aa1-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e2aa1-165">See also</span></span>
* [<span data-ttu-id="e2aa1-166">從 Azure 儲存體 Blob tooData 湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="e2aa1-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="e2aa1-167">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="e2aa1-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e2aa1-168">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e2aa1-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e2aa1-169">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2aa1-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
