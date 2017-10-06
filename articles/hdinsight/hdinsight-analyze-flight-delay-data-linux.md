---
title: "aaaAnalyze 飛行延遲資料與 HDInsight 的 Azure 上的登錄區 |Microsoft 文件"
description: "了解如何 toouse tooanalyze 飛行資料上以 Linux 為基礎的 HDInsight hive 控制檔，然後再匯出 hello 資料 tooSQL Sqoop 資料庫。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="c84c5-103">在以 Linux 為基礎的 HDInsight 上使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="c84c5-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="c84c5-104">了解如何以 Linux 為基礎的 HDInsight 上使用 Hive 則 tooanalyze 飛行延遲資料匯出 hello 資料 tooAzure SQL Database 使用 Sqoop。</span><span class="sxs-lookup"><span data-stu-id="c84c5-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c84c5-105">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c84c5-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c84c5-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c84c5-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c84c5-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c84c5-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c84c5-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c84c5-108">Prerequisites</span></span>

* <span data-ttu-id="c84c5-109">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="c84c5-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="c84c5-110">請參閱[在 Linux 上於 HDInsight 中搭配使用 Hadoop 與 Hive 入門](hdinsight-hadoop-linux-tutorial-get-started.md) ，取得建立新的 Linux 型 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="c84c5-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="c84c5-111">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="c84c5-111">**Azure SQL Database**.</span></span> <span data-ttu-id="c84c5-112">您會使用 Azure SQL Database 做為目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="c84c5-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="c84c5-113">如果您還沒有 SQL Database，請參閱 [SQL Database 教學課程：在幾分鐘內建立 SQL Database](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c84c5-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="c84c5-114">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="c84c5-114">**Azure CLI**.</span></span> <span data-ttu-id="c84c5-115">如果您尚未安裝 hello Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)的更多的步驟。</span><span class="sxs-lookup"><span data-stu-id="c84c5-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="c84c5-116">下載 hello 飛行資料</span><span class="sxs-lookup"><span data-stu-id="c84c5-116">Download hello flight data</span></span>

1. <span data-ttu-id="c84c5-117">瀏覽過[研究和創新的技術管理、 運輸局所免費提供統計][rita-website]。</span><span class="sxs-lookup"><span data-stu-id="c84c5-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="c84c5-118">在 hello 頁面上，選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="c84c5-119">名稱</span><span class="sxs-lookup"><span data-stu-id="c84c5-119">Name</span></span> | <span data-ttu-id="c84c5-120">值</span><span class="sxs-lookup"><span data-stu-id="c84c5-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c84c5-121">篩選年份</span><span class="sxs-lookup"><span data-stu-id="c84c5-121">Filter Year</span></span> |<span data-ttu-id="c84c5-122">2013</span><span class="sxs-lookup"><span data-stu-id="c84c5-122">2013</span></span> |
   | <span data-ttu-id="c84c5-123">篩選期間</span><span class="sxs-lookup"><span data-stu-id="c84c5-123">Filter Period</span></span> |<span data-ttu-id="c84c5-124">一月</span><span class="sxs-lookup"><span data-stu-id="c84c5-124">January</span></span> |
   | <span data-ttu-id="c84c5-125">欄位</span><span class="sxs-lookup"><span data-stu-id="c84c5-125">Fields</span></span> |<span data-ttu-id="c84c5-126">Year、FlightDate、UniqueCarrier、Carrier、FlightNum、OriginAirportID、Origin、OriginCityName、OriginState、DestAirportID、Dest、DestCityName、DestState、DepDelayMinutes、ArrDelay、ArrDelayMinutes、CarrierDelay、WeatherDelay、NASDelay、SecurityDelay、LateAircraftDelay。</span><span class="sxs-lookup"><span data-stu-id="c84c5-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="c84c5-127">清除所有其他欄位</span><span class="sxs-lookup"><span data-stu-id="c84c5-127">Clear all other fields</span></span> |

3. <span data-ttu-id="c84c5-128">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="c84c5-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="c84c5-129">上傳 hello 資料</span><span class="sxs-lookup"><span data-stu-id="c84c5-129">Upload hello data</span></span>

1. <span data-ttu-id="c84c5-130">使用下列命令 tooupload hello zip 檔案 toohello HDInsight 叢集前端節點的 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="c84c5-131">取代**FILENAME** hello hello zip 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="c84c5-132">取代**USERNAME**與 hello hello HDInsight 叢集的 SSH 登入。</span><span class="sxs-lookup"><span data-stu-id="c84c5-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="c84c5-133">CLUSTERNAME 取代 hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c84c5-134">如果您使用密碼 tooauthenticate SSH 登入，系統會提示您輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="c84c5-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="c84c5-135">如果您使用公開金鑰，您可能需要 toouse hello`-i`參數並指定 hello 路徑 toohello 相符的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="c84c5-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="c84c5-136">例如： `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`。</span><span class="sxs-lookup"><span data-stu-id="c84c5-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="c84c5-137">Hello 上傳完成後，請使用 SSH toohello 叢集的連線：</span><span class="sxs-lookup"><span data-stu-id="c84c5-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="c84c5-138">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c84c5-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c84c5-139">一旦連接之後，請使用下列 toounzip hello.zip 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="c84c5-140">此命令會解壓縮一個 .csv 檔案 (約為 60MB)。</span><span class="sxs-lookup"><span data-stu-id="c84c5-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="c84c5-141">使用 hello HDInsight 存放區中，下列命令 toocreate 目錄並複製 hello 檔案 toohello 目錄：</span><span class="sxs-lookup"><span data-stu-id="c84c5-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="c84c5-142">建立和執行 hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="c84c5-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="c84c5-143">使用 hello 下列步驟從 hello CSV 檔案至名為的 Hive 資料表 tooimport 資料**延遲**。</span><span class="sxs-lookup"><span data-stu-id="c84c5-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="c84c5-144">使用 hello 下列命令 toocreate 和編輯新的檔案命名為**flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="c84c5-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="c84c5-145">使用 hello hello 這個檔案的內容為下列文字：</span><span class="sxs-lookup"><span data-stu-id="c84c5-145">Use hello following text as hello contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. <span data-ttu-id="c84c5-146">toosave hello 檔案，使用**Ctrl + X**，然後**Y** 。</span><span class="sxs-lookup"><span data-stu-id="c84c5-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="c84c5-147">toostart Hive 和執行的 hello **flightdelays.hql**檔案，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="c84c5-148">在此範例中，`localhost`因為您是連接的 toohello hello HDInsight 叢集，也就是正在 HiveServer2 前端節點。</span><span class="sxs-lookup"><span data-stu-id="c84c5-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="c84c5-149">一次 hello __flightdelays.hql__完成執行時，使用 hello 下列命令 tooopen 互動式 Beeline 工作階段的指令碼：</span><span class="sxs-lookup"><span data-stu-id="c84c5-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="c84c5-150">當您收到 hello`jdbc:hive2://localhost:10001/>`提示，請使用 匯入的 hello 飛行延遲資料中的下列查詢 tooretrieve 資料 hello。</span><span class="sxs-lookup"><span data-stu-id="c84c5-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="c84c5-151">此查詢會擷取一份城市有經驗的天氣延遲，以及 hello 平均延遲時間，並將它儲存到太`/tutorials/flightdelays/output`。</span><span class="sxs-lookup"><span data-stu-id="c84c5-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="c84c5-152">稍後，Sqoop 讀取 hello 資料從這個位置，將它匯出 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c84c5-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="c84c5-153">tooexit Beeline，輸入`!quit`在 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="c84c5-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="c84c5-154">建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="c84c5-154">Create a SQL Database</span></span>

<span data-ttu-id="c84c5-155">如果您已經有 SQL 資料庫，您必須取得 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="c84c5-156">您可以在 hello 找到 hello 伺服器名稱[Azure 入口網站](https://portal.azure.com)選取**SQL 資料庫**，然後在 hello hello 名稱上篩選資料庫和想 toouse。</span><span class="sxs-lookup"><span data-stu-id="c84c5-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="c84c5-157">hello 伺服器名稱會列在 hello**伺服器**資料行。</span><span class="sxs-lookup"><span data-stu-id="c84c5-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="c84c5-158">如果您已經沒有 SQL 資料庫，使用中的 hello 資訊[SQL Database 教學課程： 建立 SQL 資料庫，以分鐘為單位](../sql-database/sql-database-get-started.md)toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="c84c5-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="c84c5-159">儲存 hello hello 資料庫所使用的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="c84c5-160">建立 SQL Database 資料表</span><span class="sxs-lookup"><span data-stu-id="c84c5-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="c84c5-161">有許多方式 tooconnect tooSQL 資料庫及建立資料表。</span><span class="sxs-lookup"><span data-stu-id="c84c5-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="c84c5-162">hello 下列步驟使用[freetds 才能使用](http://www.freetds.org/)從 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c84c5-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="c84c5-163">使用 SSH tooconnect toohello 以 Linux 為基礎的 HDInsight 叢集，並執行下列步驟從 hello SSH 工作階段的 hello。</span><span class="sxs-lookup"><span data-stu-id="c84c5-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="c84c5-164">使用下列命令 tooinstall freetds 才能使用 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="c84c5-165">Hello 安裝完成之後，請使用下列命令 tooconnect toohello SQL Database 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="c84c5-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="c84c5-166">取代**serverName** hello SQL Database 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="c84c5-167">取代**adminLogin**和**adminPassword**與 SQL Database 的 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="c84c5-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="c84c5-168">取代**databaseName** hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c84c5-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="c84c5-169">您收到的輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="c84c5-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="c84c5-170">在 hello`1>`提示字元中，輸入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="c84c5-171">當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。</span><span class="sxs-lookup"><span data-stu-id="c84c5-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="c84c5-172">此查詢會建立名為 **delays** 的資料表 (具有叢集索引)。</span><span class="sxs-lookup"><span data-stu-id="c84c5-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="c84c5-173">已建立下列 hello 資料表的查詢 tooverify 使用 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="c84c5-174">hello 輸出是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="c84c5-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="c84c5-175">輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="c84c5-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="c84c5-176">使用 Sqoop 匯出資料</span><span class="sxs-lookup"><span data-stu-id="c84c5-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="c84c5-177">使用下列命令 tooverify Sqoop 可以看到您的 SQL Database 的 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="c84c5-178">此命令會傳回一份資料庫，包括您稍早建立 hello 延遲資料表中的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c84c5-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="c84c5-179">使用 hello hivesampletable toohello mobiledata 資料表中的下列命令 tooexport 資料：</span><span class="sxs-lookup"><span data-stu-id="c84c5-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="c84c5-180">Sqoop 連接 toohello 資料庫包含 hello 延遲資料表，並將資料從 hello 匯出`/tutorials/flightdelays/output`目錄 toohello 延遲資料表。</span><span class="sxs-lookup"><span data-stu-id="c84c5-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="c84c5-181">Hello 命令完成之後，使用下列 tooconnect toohello 資料庫使用 TSQL hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="c84c5-182">一旦連接之後，使用下列陳述式 tooverify hello 資料已匯出的 toohello mobiledata 資料表 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="c84c5-183">您應該會看到 hello 資料表中資料的清單。</span><span class="sxs-lookup"><span data-stu-id="c84c5-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="c84c5-184">型別`exit`tooexit hello tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="c84c5-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="c84c5-185"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="c84c5-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="c84c5-186">toolearn HDInsight 中的資料的多個方式 toowork 請參閱下列文件 hello:</span><span class="sxs-lookup"><span data-stu-id="c84c5-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="c84c5-187">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c84c5-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c84c5-188">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="c84c5-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="c84c5-189">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="c84c5-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="c84c5-190">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c84c5-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c84c5-191">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="c84c5-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="c84c5-192">[開發適用於 HDInsight 的 Python Hadoop 串流程式][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="c84c5-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
