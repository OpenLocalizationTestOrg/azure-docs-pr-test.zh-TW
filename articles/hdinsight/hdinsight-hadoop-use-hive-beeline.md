---
title: "使用 Apache Hive-Azure HDInsight Beeline aaaUse |Microsoft 文件"
description: "了解 toouse hello Beeline 用戶端 toorun Hive 查詢的 Hadoop HDInsight 上的方式。 Beeline 是透過 JDBC 與 HiveServer2 搭配作業的公用程式。"
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
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="ce056-105">使用 Apache Hive hello Beeline 用戶端</span><span class="sxs-lookup"><span data-stu-id="ce056-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="ce056-106">深入了解如何 toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive 查詢 HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="ce056-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="ce056-107">Beeline 是包含 hello 的 HDInsight 叢集的前端節點的登錄區用戶端。</span><span class="sxs-lookup"><span data-stu-id="ce056-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="ce056-108">Beeline 會使用 JDBC tooconnect tooHiveServer2，您的 HDInsight 叢集上裝載的服務。</span><span class="sxs-lookup"><span data-stu-id="ce056-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="ce056-109">您也可以使用 Beeline tooaccess Hive HDInsight 上從遠端透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ce056-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="ce056-110">下表中的 hello 搭配 Beeline 提供連接字串：</span><span class="sxs-lookup"><span data-stu-id="ce056-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="ce056-111">您執行 Beeline 的來源</span><span class="sxs-lookup"><span data-stu-id="ce056-111">Where you run Beeline from</span></span> | <span data-ttu-id="ce056-112">參數</span><span class="sxs-lookup"><span data-stu-id="ce056-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce056-113">SSH 連線 tooa 叢集前端節點或邊緣節點</span><span class="sxs-lookup"><span data-stu-id="ce056-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="ce056-114">外部 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="ce056-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="ce056-115">取代`admin`與 hello 叢集登入帳戶，供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="ce056-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="ce056-116">取代`password`hello hello 叢集登入帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ce056-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="ce056-117">取代`clustername`hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce056-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="ce056-118"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="ce056-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ce056-119">HDInsight 叢集上以 Linux 為基礎的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="ce056-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ce056-120">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="ce056-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ce056-121">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ce056-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ce056-122">SSH 用戶端或本機 Beeline 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ce056-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="ce056-123">大部分的這份文件中的 hello 步驟假設您使用 Beeline 從 SSH 工作階段 toohello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ce056-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="ce056-124">如需從外部 hello 叢集中執行 Beeline 資訊，請參閱 hello[從遠端使用 Beeline](#remote) > 一節。</span><span class="sxs-lookup"><span data-stu-id="ce056-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="ce056-125">如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ce056-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="ce056-126"><a id="beeline"></a>使用 BeeLine</span><span class="sxs-lookup"><span data-stu-id="ce056-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="ce056-127">啟動 Beeline 時，您必須為 HDInsight 叢集上的 HiveServer2 提供連接字串。</span><span class="sxs-lookup"><span data-stu-id="ce056-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="ce056-128">從外部 hello 叢集 toorun hello 命令，您必須提供 hello 叢集登入帳戶名稱 (預設`admin`) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="ce056-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="ce056-129">使用下列資料表 toofind hello 連接字串格式和參數 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="ce056-130">您執行 Beeline 的來源</span><span class="sxs-lookup"><span data-stu-id="ce056-130">Where you run Beeline from</span></span> | <span data-ttu-id="ce056-131">參數</span><span class="sxs-lookup"><span data-stu-id="ce056-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="ce056-132">SSH 連線 tooa 叢集前端節點或邊緣節點</span><span class="sxs-lookup"><span data-stu-id="ce056-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="ce056-133">外部 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="ce056-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="ce056-134">比方說，下列命令的 hello 可以是從 SSH 工作階段 toohello 叢集中使用的 toostart Beeline:</span><span class="sxs-lookup"><span data-stu-id="ce056-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="ce056-135">此命令啟動 hello Beeline 用戶端，並連接 tooHiveServer2 hello 叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="ce056-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="ce056-136">Hello 命令完成之後，您會抵達`jdbc:hive2://headnodehost:10001/>`提示字元。</span><span class="sxs-lookup"><span data-stu-id="ce056-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="ce056-137">Beeline 命令以 `!` 字元開頭，例如 `!help` 顯示說明。</span><span class="sxs-lookup"><span data-stu-id="ce056-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="ce056-138">不過 hello`!`可以省略某些命令。</span><span class="sxs-lookup"><span data-stu-id="ce056-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="ce056-139">例如，`help` 也能運作。</span><span class="sxs-lookup"><span data-stu-id="ce056-139">For example, `help` also works.</span></span>

    <span data-ttu-id="ce056-140">沒有`!sql`，而是使用的 tooexecute HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ce056-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="ce056-141">不過，下列 HiveQL 因此通常用於您可以省略上述 hello `!sql`。</span><span class="sxs-lookup"><span data-stu-id="ce056-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="ce056-142">hello 下列兩個陳述式是相等的：</span><span class="sxs-lookup"><span data-stu-id="ce056-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="ce056-143">新的叢集上只會列出一個資料表：**hivesampletable**。</span><span class="sxs-lookup"><span data-stu-id="ce056-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="ce056-144">使用下列命令 toodisplay hello 結構描述的 hello hivesampletable hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="ce056-145">此命令會傳回下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="ce056-146">這項資訊會描述 hello hello 資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="ce056-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="ce056-147">雖然我們無法執行一些查詢，針對此資料，讓我們改為建立全新的資料表 toodemonstrate 如何 Hive tooload 資料，並套用結構描述。</span><span class="sxs-lookup"><span data-stu-id="ce056-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="ce056-148">輸入下列陳述式 toocreate 資料表名為 hello **log4jLogs**使用所提供與 hello HDInsight 叢集的範例資料：</span><span class="sxs-lookup"><span data-stu-id="ce056-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="ce056-149">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="ce056-150">`DROP TABLE`-如果 hello 資料表存在，會將其刪除。</span><span class="sxs-lookup"><span data-stu-id="ce056-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="ce056-151">`CREATE EXTERNAL TABLE` - 在 Hive 中建立**外部**資料表。</span><span class="sxs-lookup"><span data-stu-id="ce056-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="ce056-152">外部資料表只會儲存在登錄區中的 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ce056-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="ce056-153">hello 資料會保留在 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="ce056-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="ce056-154">`ROW FORMAT`的 hello 資料格式化方式。</span><span class="sxs-lookup"><span data-stu-id="ce056-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="ce056-155">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="ce056-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="ce056-156">`STORED AS TEXTFILE LOCATION`-Hello 資料會儲存以及在何種檔案格式。</span><span class="sxs-lookup"><span data-stu-id="ce056-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="ce056-157">`SELECT`-選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="ce056-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="ce056-158">此查詢會傳回值 **3** ，因為有 3 個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="ce056-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="ce056-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive 嘗試 tooapply hello 結構描述 tooall 檔案 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ce056-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="ce056-160">在此情況下，hello 目錄包含不符合 hello 結構描述的檔案。</span><span class="sxs-lookup"><span data-stu-id="ce056-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="ce056-161">tooprevent 記憶體回收 hello 結果中的資料，此陳述式會告知登錄區，我們應該只會傳回資料從檔案結尾。 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ce056-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce056-162">當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="ce056-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="ce056-163">例如，自動化的資料上傳程序，或透過其他 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="ce056-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="ce056-164">卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ce056-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="ce056-165">hello 輸出此命令為類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="ce056-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="ce056-166">tooexit Beeline，使用`!exit`。</span><span class="sxs-lookup"><span data-stu-id="ce056-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="ce056-167"><a id="file"></a>使用 Beeline toorun HiveQL 檔案</span><span class="sxs-lookup"><span data-stu-id="ce056-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="ce056-168">使用下列步驟 toocreate 檔案，然後執行它使用 Beeline hello。</span><span class="sxs-lookup"><span data-stu-id="ce056-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="ce056-169">使用 hello 下列命令 toocreate 名為**query.hql**:</span><span class="sxs-lookup"><span data-stu-id="ce056-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="ce056-170">使用 hello hello hello 檔案內容為下列文字。</span><span class="sxs-lookup"><span data-stu-id="ce056-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="ce056-171">此查詢將建立名為 **errorLogs** 的新「內部」資料表：</span><span class="sxs-lookup"><span data-stu-id="ce056-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="ce056-172">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="ce056-173">**建立資料表 IF NOT EXISTS** -如果 hello 資料表不存在，就會建立。</span><span class="sxs-lookup"><span data-stu-id="ce056-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="ce056-174">因為 hello**外部**不是關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="ce056-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="ce056-175">內部資料表會儲存在 hello Hive 資料倉儲，而且都完全受登錄區。</span><span class="sxs-lookup"><span data-stu-id="ce056-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="ce056-176">**儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。</span><span class="sxs-lookup"><span data-stu-id="ce056-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ce056-177">ORC 格式是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="ce056-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="ce056-178">**INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="ce056-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ce056-179">不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。</span><span class="sxs-lookup"><span data-stu-id="ce056-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="ce056-180">toosave hello 檔案，使用**Ctrl**+**_X**，然後輸入**Y**，最後再**Enter**。</span><span class="sxs-lookup"><span data-stu-id="ce056-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="ce056-181">使用下列 toorun hello 檔使用 Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="ce056-182">hello`-i`參數啟動 Beeline，執行 hello hello query.hql 檔案中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="ce056-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="ce056-183">Hello 查詢完成之後，到達 hello`jdbc:hive2://headnodehost:10001/>`提示字元。</span><span class="sxs-lookup"><span data-stu-id="ce056-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="ce056-184">您也可以執行檔案，使用 hello`-f`結束 Beeline hello 查詢完成後的參數。</span><span class="sxs-lookup"><span data-stu-id="ce056-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="ce056-185">hello 的 tooverify**錯誤記錄檔**建立資料表，請使用下列陳述式 tooreturn 所有 hello 中的資料列的 hello**錯誤記錄檔**:</span><span class="sxs-lookup"><span data-stu-id="ce056-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="ce056-186">應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** ：</span><span class="sxs-lookup"><span data-stu-id="ce056-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="ce056-187"><a id="remote"></a>從遠端使用 Beeline</span><span class="sxs-lookup"><span data-stu-id="ce056-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="ce056-188">如果您有 Beeline 安裝在本機，或正在使用它透過 Docker 映像例如[sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/)，您必須使用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="ce056-189">__連接字串__：`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="ce056-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="ce056-190">__叢集登入名稱__：`-n admin`</span><span class="sxs-lookup"><span data-stu-id="ce056-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="ce056-191">__叢集登入密碼__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="ce056-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="ce056-192">取代 hello `clustername` hello hello 名稱，為您的 HDInsight 叢集的連接字串中。</span><span class="sxs-lookup"><span data-stu-id="ce056-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="ce056-193">取代`admin`與叢集登入，以及取代 hello 名稱`password`hello 您叢集的登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="ce056-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="ce056-194"><a id="sparksql"></a>使用 Beeline 搭配 Spark</span><span class="sxs-lookup"><span data-stu-id="ce056-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="ce056-195">Spark 提供自己的 HiveServer2，通常是來參考 tooas hello Spark Thrift 伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="ce056-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="ce056-196">此服務使用 Spark SQL tooresolve 查詢而不是登錄區，且可能會提供更佳的效能，根據您的查詢。</span><span class="sxs-lookup"><span data-stu-id="ce056-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="ce056-197">tooconnect toohello Spark Thrift 伺服器的 HDInsight 叢集，使用連接埠上的 Spark`10002`而不是`10001`。</span><span class="sxs-lookup"><span data-stu-id="ce056-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="ce056-198">例如： `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`。</span><span class="sxs-lookup"><span data-stu-id="ce056-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce056-199">無法直接存取 over hello 網際網路 hello Spark Thrift 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ce056-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="ce056-200">您只能從為 SSH 工作階段連線 tooit 或內 hello 相同 Azure 虛擬網路如 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce056-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="ce056-201"><a id="summary"></a><a id="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce056-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ce056-202">多個一般 HDInsight 中的登錄區的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="ce056-203">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ce056-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ce056-204">如需詳細資訊之其他方式，您可以使用 Hadoop HDInsight、 請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="ce056-205">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ce056-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ce056-206">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ce056-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ce056-207">如果您正在使用 Hive Tez，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce056-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="ce056-208">使用 Windows 為基礎的 HDInsight 上的 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="ce056-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="ce056-209">使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視</span><span class="sxs-lookup"><span data-stu-id="ce056-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
