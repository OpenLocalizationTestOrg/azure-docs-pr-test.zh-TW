---
title: "採用 Hadoop 的 Apache Sqoop - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Sqoop 在 Hadoop on HDInsight 與 Azure SQL Database 之間進行匯入和匯出。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="2cb64-104">使用 Apache Sqoop 在 HDInsight 與 SQL Database 的 Hadoop 間匯入及匯出資料</span><span class="sxs-lookup"><span data-stu-id="2cb64-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="2cb64-105">了解如何使用 Sqoop，在 Azure HDInsight 中的 Hadoop 叢集與 Azure SQL Database 或 Microsoft SQL Server 資料庫之間進行匯入和匯出。</span><span class="sxs-lookup"><span data-stu-id="2cb64-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="2cb64-106">本文件中的步驟直接從 Hadoop 叢集的前端節點使用 `sqoop` 命令。</span><span class="sxs-lookup"><span data-stu-id="2cb64-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="2cb64-107">您可以使用 SSH 連接至前端節點，並執行本文件中的命令。</span><span class="sxs-lookup"><span data-stu-id="2cb64-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cb64-108">本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2cb64-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="2cb64-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="2cb64-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2cb64-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="2cb64-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="2cb64-111">安裝 FreeTDS</span><span class="sxs-lookup"><span data-stu-id="2cb64-111">Install FreeTDS</span></span>

1. <span data-ttu-id="2cb64-112">使用 SSH 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2cb64-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="2cb64-113">例如，下列命令可連接至名為 `mycluster` 之叢集的主要前端節點：</span><span class="sxs-lookup"><span data-stu-id="2cb64-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2cb64-114">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="2cb64-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2cb64-115">使用下列命令來安裝 FreeTDS：</span><span class="sxs-lookup"><span data-stu-id="2cb64-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="2cb64-116">在數個步驟中將使用 FreeTDS 來連接到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="2cb64-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="2cb64-117">在 SQL Database 中建立資料表</span><span class="sxs-lookup"><span data-stu-id="2cb64-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cb64-118">如果您使用在[建立叢集與 SQL Database](hdinsight-use-sqoop.md) 中建立的 HDInsight 叢集和 SQL Database，請略過這一節的步驟。</span><span class="sxs-lookup"><span data-stu-id="2cb64-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="2cb64-119">在[建立叢集與 SQL database](hdinsight-use-sqoop.md) 文件的步驟中所建立的資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="2cb64-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="2cb64-120">從 SSH 工作階段中，使用下列命令來連接到 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2cb64-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="2cb64-121">您會收到如以下文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="2cb64-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="2cb64-122">在 `1>` 提示字元輸入下列查詢：</span><span class="sxs-lookup"><span data-stu-id="2cb64-122">At the `1>` prompt, enter the following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="2cb64-123">輸入 `GO` 陳述式後，將評估先前的陳述式。</span><span class="sxs-lookup"><span data-stu-id="2cb64-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="2cb64-124">首先，建立 **mobiledata** 資料表，然後將叢集索引加入至該資料表 (SQL Database 所需)。</span><span class="sxs-lookup"><span data-stu-id="2cb64-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="2cb64-125">使用下列查詢來確認已建立資料表：</span><span class="sxs-lookup"><span data-stu-id="2cb64-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="2cb64-126">您會看到類似以下的文字：</span><span class="sxs-lookup"><span data-stu-id="2cb64-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="2cb64-127">在 `exit` at the `1>` 以結束 tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="2cb64-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="2cb64-128">Sqoop export</span><span class="sxs-lookup"><span data-stu-id="2cb64-128">Sqoop export</span></span>

1. <span data-ttu-id="2cb64-129">從對叢集的 SSH 連線，使用下列命令來確認 Sqoop 看得見您的 SQL Database：</span><span class="sxs-lookup"><span data-stu-id="2cb64-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="2cb64-130">出現提示時，請輸入 SQL Database 的登入密碼。</span><span class="sxs-lookup"><span data-stu-id="2cb64-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="2cb64-131">這個命令會傳回一份資料庫清單，其中包含您稍早建立的 **sqooptest** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2cb64-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="2cb64-132">若要將資料從 **hivesampletable** 匯出至 **mobiledata** 資料表，請使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="2cb64-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="2cb64-133">這個命令會指示 Sqoop 連接至 **sqooptest** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2cb64-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="2cb64-134">Sqoop 接著會將從 **wasb:///hive/warehouse/hivesampletable** 匯出的資料匯出至 **mobiledata** 資料表。</span><span class="sxs-lookup"><span data-stu-id="2cb64-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2cb64-135">如果叢集的預設儲存體是 Azure 儲存體帳戶，請使用 `wasb:///`。</span><span class="sxs-lookup"><span data-stu-id="2cb64-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="2cb64-136">如果是 Azure Data Lake Store，請使用 `adl:///`。</span><span class="sxs-lookup"><span data-stu-id="2cb64-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="2cb64-137">在命令完成後，使用下列命令連接至使用 TSQL 的資料庫：</span><span class="sxs-lookup"><span data-stu-id="2cb64-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="2cb64-138">連線之後，使用下列陳述式來確認資料已匯出到 **mobiledata** 資料表：</span><span class="sxs-lookup"><span data-stu-id="2cb64-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="2cb64-139">您應會看到資料表中的資料清單。</span><span class="sxs-lookup"><span data-stu-id="2cb64-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="2cb64-140">輸入 `exit` 以結束 tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="2cb64-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="2cb64-141">Sqoop import</span><span class="sxs-lookup"><span data-stu-id="2cb64-141">Sqoop import</span></span>

1. <span data-ttu-id="2cb64-142">使用下列命令將資料從 SQL Database 中的 **mobiledata** 資料表匯入至 HDInsight 上的 **wasb:///tutorials/usesqoop/importeddata** 目錄：</span><span class="sxs-lookup"><span data-stu-id="2cb64-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="2cb64-143">資料中的欄位是以定位字元分隔，行是以換行字元終止。</span><span class="sxs-lookup"><span data-stu-id="2cb64-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="2cb64-144">匯入完成後，使用下列命令來列出新目錄中的資料：</span><span class="sxs-lookup"><span data-stu-id="2cb64-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="2cb64-145">使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="2cb64-145">Using SQL Server</span></span>

<span data-ttu-id="2cb64-146">您也可以使用 Sqoop 從 SQL Server 匯入和匯出資料 (在資料中心或在 Azure 中裝載的虛擬機器上)。</span><span class="sxs-lookup"><span data-stu-id="2cb64-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="2cb64-147">使用 SQL Database 和 SQL Server 之間的差異如下：</span><span class="sxs-lookup"><span data-stu-id="2cb64-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="2cb64-148">HDInsight 與 SQL Server 必須位於相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2cb64-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="2cb64-149">如需範例，請參閱[將 HDInsight 連線至內部部署網路](./connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="2cb64-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="2cb64-150">如需使用 HDInsight 搭配 Azure 虛擬網路的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](hdinsight-extend-hadoop-virtual-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="2cb64-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="2cb64-151">如需 Azure 虛擬網路的詳細資訊，請參閱[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)文件。</span><span class="sxs-lookup"><span data-stu-id="2cb64-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="2cb64-152">SQL Server 也必須設定為允許 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="2cb64-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="2cb64-153">如需詳細資訊，請參閱[選擇驗證模式](https://msdn.microsoft.com/ms144284.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="2cb64-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="2cb64-154">您可能必須設定 SQL Server 以接受遠端連線。</span><span class="sxs-lookup"><span data-stu-id="2cb64-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="2cb64-155">如需詳細資訊，請參閱[如何疑難排解 SQL Server Database Engine 連線](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)文件 (英文)。</span><span class="sxs-lookup"><span data-stu-id="2cb64-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="2cb64-156">在 SQL Server 中，使用公用程式 (例如 **SQL Server Management Studio** 或 **tsql**) 建立 **sqooptest** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2cb64-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="2cb64-157">使用 Azure CLI 的步驟只適用於 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2cb64-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="2cb64-158">使用下列 Transact-SQL 陳述式建立 **mobiledata** 資料表︰</span><span class="sxs-lookup"><span data-stu-id="2cb64-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="2cb64-159">從 HDInsight 連線到 SQL Server 時，您可能必須使用 SQL Server 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2cb64-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="2cb64-160">例如：</span><span class="sxs-lookup"><span data-stu-id="2cb64-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="2cb64-161">限制</span><span class="sxs-lookup"><span data-stu-id="2cb64-161">Limitations</span></span>

* <span data-ttu-id="2cb64-162">大量匯出 - 使用 Linux 型 HDInsight，用來將資料匯出至 Microsoft SQL Server 或 Azure SQL Database 的 Sqoop 連接器目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="2cb64-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="2cb64-163">批次處理 - 使用 Linux 型 HDInsight，執行插入時若使用 `-batch` 參數，Sqoop 將會執行多個插入，而不是批次處理插入作業。</span><span class="sxs-lookup"><span data-stu-id="2cb64-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cb64-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2cb64-164">Next steps</span></span>

<span data-ttu-id="2cb64-165">現在，您已了解如何使用 Sqoop。</span><span class="sxs-lookup"><span data-stu-id="2cb64-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="2cb64-166">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="2cb64-166">To learn more, see:</span></span>

* <span data-ttu-id="2cb64-167">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="2cb64-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="2cb64-168">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-data]：使用 Hive 分析航班誤點資料，然後使用 Sqoop 將資料匯出至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="2cb64-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="2cb64-169">[將資料上傳至 HDInsight][hdinsight-upload-data]：尋找其他方法將資料上傳至 HDInsight/Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2cb64-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
