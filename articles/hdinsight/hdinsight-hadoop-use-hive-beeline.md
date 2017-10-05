---
title: "使用 Beeline 搭配 Apache Hive - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Beeline 用戶端以 Hadoop on HDInsight 執行 Hive 查詢。 Beeline 是透過 JDBC 與 HiveServer2 搭配作業的公用程式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="c8918-105">使用 Beeline 用戶端搭配 Apache Hive</span><span class="sxs-lookup"><span data-stu-id="c8918-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="c8918-106">了解如何使用 [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) 在 HDInsight 上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="c8918-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="c8918-107">Beeline 是 Hive 用戶端，隨附於您的 HDInsight 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="c8918-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="c8918-108">Beeline 會使用 JDBC 連線至 HiveServer2，它是裝載在 HDInsight 叢集上的服務。</span><span class="sxs-lookup"><span data-stu-id="c8918-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="c8918-109">您也可以使用 Beeline 透過網際網路從遠端存取 HDInsight 上的 Hive。</span><span class="sxs-lookup"><span data-stu-id="c8918-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="c8918-110">下表提供與 Beeline 搭配使用的連接字串：</span><span class="sxs-lookup"><span data-stu-id="c8918-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="c8918-111">您執行 Beeline 的來源</span><span class="sxs-lookup"><span data-stu-id="c8918-111">Where you run Beeline from</span></span> | <span data-ttu-id="c8918-112">參數</span><span class="sxs-lookup"><span data-stu-id="c8918-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8918-113">對前端或邊緣節點的 SSH 連線</span><span class="sxs-lookup"><span data-stu-id="c8918-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="c8918-114">叢集外部</span><span class="sxs-lookup"><span data-stu-id="c8918-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="c8918-115">將 `admin` 取代為叢集的叢集登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8918-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="c8918-116">將 `password` 取代為叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="c8918-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="c8918-117">將 `clustername` 替換為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="c8918-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="c8918-118"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="c8918-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c8918-119">HDInsight 叢集上以 Linux 為基礎的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="c8918-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c8918-120">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c8918-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c8918-121">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c8918-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c8918-122">SSH 用戶端或本機 Beeline 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c8918-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="c8918-123">本文件中的大部分步驟都假設您從連往叢集的 SSH 工作階段使用 Beeline。</span><span class="sxs-lookup"><span data-stu-id="c8918-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="c8918-124">如需從叢集外部執行 Beeline 的相關資訊，請參閱[從遠端使用 Beeline](#remote) 一節。</span><span class="sxs-lookup"><span data-stu-id="c8918-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="c8918-125">如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c8918-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="c8918-126"><a id="beeline"></a>使用 BeeLine</span><span class="sxs-lookup"><span data-stu-id="c8918-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="c8918-127">啟動 Beeline 時，您必須為 HDInsight 叢集上的 HiveServer2 提供連接字串。</span><span class="sxs-lookup"><span data-stu-id="c8918-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="c8918-128">若要從叢集外部執行命令，您也必須提供叢集登入帳戶名稱 (預設為 `admin`) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="c8918-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="c8918-129">使用下表來尋找要使用的連接字串格式和參數︰</span><span class="sxs-lookup"><span data-stu-id="c8918-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="c8918-130">您執行 Beeline 的來源</span><span class="sxs-lookup"><span data-stu-id="c8918-130">Where you run Beeline from</span></span> | <span data-ttu-id="c8918-131">參數</span><span class="sxs-lookup"><span data-stu-id="c8918-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="c8918-132">對前端或邊緣節點的 SSH 連線</span><span class="sxs-lookup"><span data-stu-id="c8918-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="c8918-133">叢集外部</span><span class="sxs-lookup"><span data-stu-id="c8918-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="c8918-134">例如，下列命令可用來啟動從連往叢集的 SSH 工作階段啟動 Beeline：</span><span class="sxs-lookup"><span data-stu-id="c8918-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="c8918-135">此命令會啟動 Beeline 用戶端，然後連線至叢集前端節點上的 HiveServer2。</span><span class="sxs-lookup"><span data-stu-id="c8918-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="c8918-136">命令完成之後，您會看見 `jdbc:hive2://headnodehost:10001/>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="c8918-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="c8918-137">Beeline 命令以 `!` 字元開頭，例如 `!help` 顯示說明。</span><span class="sxs-lookup"><span data-stu-id="c8918-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="c8918-138">不過，一些命令可以省略 `!`。</span><span class="sxs-lookup"><span data-stu-id="c8918-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="c8918-139">例如，`help` 也能運作。</span><span class="sxs-lookup"><span data-stu-id="c8918-139">For example, `help` also works.</span></span>

    <span data-ttu-id="c8918-140">會有一個 `!sql`，用來執行 HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c8918-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="c8918-141">不過，HiveQL 如此常用，因此您可以省略前面的 `!sql`。</span><span class="sxs-lookup"><span data-stu-id="c8918-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="c8918-142">下列兩個陳述式是相等的：</span><span class="sxs-lookup"><span data-stu-id="c8918-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="c8918-143">新的叢集上只會列出一個資料表：**hivesampletable**。</span><span class="sxs-lookup"><span data-stu-id="c8918-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="c8918-144">使用下列命令來顯示 hivesampletable 的結構描述：</span><span class="sxs-lookup"><span data-stu-id="c8918-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="c8918-145">此命令會傳回下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c8918-145">This command returns the following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="c8918-146">此資訊描述資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="c8918-146">This information describes the columns in the table.</span></span> <span data-ttu-id="c8918-147">我們雖可對此資料執行某些查詢，但讓我們改為建立全新的資料表來示範如何將資料載入 Hive 及套用結構描述。</span><span class="sxs-lookup"><span data-stu-id="c8918-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="c8918-148">輸入下列陳述式，以使用 HDInsight 叢集隨附的範例資料來建立名為 **log4jLogs** 的資料表：</span><span class="sxs-lookup"><span data-stu-id="c8918-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="c8918-149">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c8918-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="c8918-150">`DROP TABLE` - 如果資料表存在，則會刪除它。</span><span class="sxs-lookup"><span data-stu-id="c8918-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="c8918-151">`CREATE EXTERNAL TABLE` - 在 Hive 中建立**外部**資料表。</span><span class="sxs-lookup"><span data-stu-id="c8918-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="c8918-152">外部資料表只會將資料表定義儲存在 Hive 中。</span><span class="sxs-lookup"><span data-stu-id="c8918-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="c8918-153">資料會留在原來的位置。</span><span class="sxs-lookup"><span data-stu-id="c8918-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="c8918-154">`ROW FORMAT` - 設定資料格式的方式。</span><span class="sxs-lookup"><span data-stu-id="c8918-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="c8918-155">在此情況下，每個記錄中的欄位會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="c8918-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="c8918-156">`STORED AS TEXTFILE LOCATION` - 儲存資料的所在位置以及以何種檔案格式儲存。</span><span class="sxs-lookup"><span data-stu-id="c8918-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="c8918-157">`SELECT` - 選取其資料行 **t4** 包含值 **[ERROR]** 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="c8918-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="c8918-158">此查詢會傳回值 **3** ，因為有 3 個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="c8918-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="c8918-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive 嘗試將結構描述套用至目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="c8918-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="c8918-160">在此情況下，目錄包含不符合結構描述的檔案。</span><span class="sxs-lookup"><span data-stu-id="c8918-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="c8918-161">若要防止結果中出現亂碼資料，此陳述式會告訴 Hive 我們只應該從檔名以 log 結尾的檔案傳回資料。</span><span class="sxs-lookup"><span data-stu-id="c8918-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c8918-162">當您預期會由外部來源來更新基礎資料時，請使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="c8918-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="c8918-163">例如，自動化的資料上傳程序，或透過其他 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="c8918-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="c8918-164">捨棄外部資料表並 **不會** 刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="c8918-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="c8918-165">此命令的輸出類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="c8918-165">The output of this command is similar to the following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="c8918-166">若要結束 Beeline，請使用 `!exit`。</span><span class="sxs-lookup"><span data-stu-id="c8918-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="c8918-167"><a id="file"></a>使用 Beeline 執行 HiveQL 檔案</span><span class="sxs-lookup"><span data-stu-id="c8918-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="c8918-168">使用下列步驟建立檔案，然後利用執行該檔案。</span><span class="sxs-lookup"><span data-stu-id="c8918-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="c8918-169">使用以下命令，建立名為 **query.hql** 的檔案：</span><span class="sxs-lookup"><span data-stu-id="c8918-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="c8918-170">使用下列文字做為檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="c8918-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="c8918-171">此查詢將建立名為 **errorLogs** 的新「內部」資料表：</span><span class="sxs-lookup"><span data-stu-id="c8918-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="c8918-172">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c8918-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="c8918-173">**CREATE TABLE IF NOT EXISTS** - 如果資料表尚不存在，則會建立它。</span><span class="sxs-lookup"><span data-stu-id="c8918-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="c8918-174">因為未使用 **EXTERNAL** 關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="c8918-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="c8918-175">內部資料表儲存在 Hive 資料倉儲中，並完全由 Hive 管理。</span><span class="sxs-lookup"><span data-stu-id="c8918-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="c8918-176">**STORED AS ORC** - 以最佳化資料列單欄式 (Optimized Row Columnar, ORC) 格式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="c8918-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="c8918-177">ORC 格式是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="c8918-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="c8918-178">**INSERT OVERWRITE ...SELECT**- 從包含 **[ERROR]** 的 **log4jLogs** 資料表選取資料列，然後將資料插入 **errorLogs** 資料表。</span><span class="sxs-lookup"><span data-stu-id="c8918-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8918-179">與外部資料表不同之處在於，捨棄內部資料表也會刪除基礎資料。</span><span class="sxs-lookup"><span data-stu-id="c8918-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="c8918-180">若要儲存檔案，請使用 **Ctrl**+**_X**，然後輸入 **Y**，最後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="c8918-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="c8918-181">使用下列命令，以使用 Beeline 來執行檔案：</span><span class="sxs-lookup"><span data-stu-id="c8918-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="c8918-182">`-i` 參數會啟動 Beeline、執行 query.hql 檔案中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="c8918-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="c8918-183">當查詢完成時，您會看到 `jdbc:hive2://headnodehost:10001/>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="c8918-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="c8918-184">您也可以使用 `-f` 參數執行檔案，它會在查詢完成後結束 Beeline。</span><span class="sxs-lookup"><span data-stu-id="c8918-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="c8918-185">若要確認 **errorLogs** 資料表已建立，請使用下列陳述式傳回 **errorLogs** 的所有資料列：</span><span class="sxs-lookup"><span data-stu-id="c8918-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="c8918-186">應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** ：</span><span class="sxs-lookup"><span data-stu-id="c8918-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="c8918-187"><a id="remote"></a>從遠端使用 Beeline</span><span class="sxs-lookup"><span data-stu-id="c8918-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="c8918-188">如果您已在本機安裝 Beeline，或是正透過 Docker 映像如 [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/) 使用它，您必須使用下列參數：</span><span class="sxs-lookup"><span data-stu-id="c8918-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="c8918-189">__連接字串__：`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="c8918-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="c8918-190">__叢集登入名稱__：`-n admin`</span><span class="sxs-lookup"><span data-stu-id="c8918-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="c8918-191">__叢集登入密碼__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="c8918-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="c8918-192">將連接字串中的 `clustername` 取代為您的 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="c8918-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="c8918-193">將 `admin` 取代為叢集登入的名稱，以及將 `password` 取代為您的叢集登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="c8918-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="c8918-194"><a id="sparksql"></a>使用 Beeline 搭配 Spark</span><span class="sxs-lookup"><span data-stu-id="c8918-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="c8918-195">Spark 提供自己的 HiveServer2 實作，這通常是指 Spark Thrift 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c8918-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="c8918-196">此服務會使用 Spark SQL 來解析查詢而不是 Hive，並可能提供更佳的效能 (視您的查詢而定)。</span><span class="sxs-lookup"><span data-stu-id="c8918-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="c8918-197">若要連線到 HDInsight 叢集上 Spark 的 Spark Thrift 伺服器，請使用連接埠 `10002` 而不是 `10001`。</span><span class="sxs-lookup"><span data-stu-id="c8918-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="c8918-198">例如， `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`。</span><span class="sxs-lookup"><span data-stu-id="c8918-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8918-199">無法透過網際網路直接存取 Spark Thrift 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c8918-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="c8918-200">您只能從 SSH 工作階段或在與 HDInsight 叢集相同的 Azure 虛擬網路內連線到它。</span><span class="sxs-lookup"><span data-stu-id="c8918-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="c8918-201"><a id="summary"></a><a id="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8918-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c8918-202">如需有關 HDInsight 中 Hive 的更多一般資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="c8918-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="c8918-203">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8918-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="c8918-204">如需您可以使用 HDInsight 上的 Hadoop 之其他方式的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="c8918-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="c8918-205">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8918-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c8918-206">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8918-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c8918-207">如果您搭配使用 Tez 和 Hive，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="c8918-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="c8918-208">在以 Windows 為基礎的 HDInsight 上使用 Tez UI</span><span class="sxs-lookup"><span data-stu-id="c8918-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="c8918-209">在以 Linux 為基礎的 HDInsight 上使用 Ambari Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="c8918-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
