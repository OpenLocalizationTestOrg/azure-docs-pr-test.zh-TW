---
title: "在 HDInsight 上使用 Hive 分析航班延誤資料 - Azure | Microsoft Docs"
description: "了解如何在 Linux 型 HDInsight 上使用 Hive 分析航班資料，然後使用 Sqoop 將資料匯出至 SQL Database。"
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="64b6e-103">在以 Linux 為基礎的 HDInsight 上使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="64b6e-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="64b6e-104">了解如何在以 Linux 為基礎的 HDInsight 上使用 Hive 分析航班延誤資料，然後使用 Sqoop 將資料匯出至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="64b6e-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64b6e-105">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64b6e-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="64b6e-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="64b6e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="64b6e-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="64b6e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="64b6e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="64b6e-108">Prerequisites</span></span>

* <span data-ttu-id="64b6e-109">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="64b6e-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="64b6e-110">請參閱[在 Linux 上於 HDInsight 中搭配使用 Hadoop 與 Hive 入門](hdinsight-hadoop-linux-tutorial-get-started.md) ，取得建立新的 Linux 型 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="64b6e-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="64b6e-111">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="64b6e-111">**Azure SQL Database**.</span></span> <span data-ttu-id="64b6e-112">您會使用 Azure SQL Database 做為目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="64b6e-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="64b6e-113">如果您還沒有 SQL Database，請參閱 [SQL Database 教學課程：在幾分鐘內建立 SQL Database](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="64b6e-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="64b6e-114">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="64b6e-114">**Azure CLI**.</span></span> <span data-ttu-id="64b6e-115">如果您尚未安裝 Azure CLI，請參閱 [安裝與設定 Azure CLI](../cli-install-nodejs.md) 的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="64b6e-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="64b6e-116">下載航班資料</span><span class="sxs-lookup"><span data-stu-id="64b6e-116">Download the flight data</span></span>

1. <span data-ttu-id="64b6e-117">瀏覽至[創新技術研究管理部運輸統計處][rita-website]。</span><span class="sxs-lookup"><span data-stu-id="64b6e-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="64b6e-118">在此頁面上選取下列值：</span><span class="sxs-lookup"><span data-stu-id="64b6e-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="64b6e-119">名稱</span><span class="sxs-lookup"><span data-stu-id="64b6e-119">Name</span></span> | <span data-ttu-id="64b6e-120">值</span><span class="sxs-lookup"><span data-stu-id="64b6e-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="64b6e-121">篩選年份</span><span class="sxs-lookup"><span data-stu-id="64b6e-121">Filter Year</span></span> |<span data-ttu-id="64b6e-122">2013</span><span class="sxs-lookup"><span data-stu-id="64b6e-122">2013</span></span> |
   | <span data-ttu-id="64b6e-123">篩選期間</span><span class="sxs-lookup"><span data-stu-id="64b6e-123">Filter Period</span></span> |<span data-ttu-id="64b6e-124">一月</span><span class="sxs-lookup"><span data-stu-id="64b6e-124">January</span></span> |
   | <span data-ttu-id="64b6e-125">欄位</span><span class="sxs-lookup"><span data-stu-id="64b6e-125">Fields</span></span> |<span data-ttu-id="64b6e-126">Year、FlightDate、UniqueCarrier、Carrier、FlightNum、OriginAirportID、Origin、OriginCityName、OriginState、DestAirportID、Dest、DestCityName、DestState、DepDelayMinutes、ArrDelay、ArrDelayMinutes、CarrierDelay、WeatherDelay、NASDelay、SecurityDelay、LateAircraftDelay。</span><span class="sxs-lookup"><span data-stu-id="64b6e-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="64b6e-127">清除所有其他欄位</span><span class="sxs-lookup"><span data-stu-id="64b6e-127">Clear all other fields</span></span> |

3. <span data-ttu-id="64b6e-128">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="64b6e-129">上傳資料</span><span class="sxs-lookup"><span data-stu-id="64b6e-129">Upload the data</span></span>

1. <span data-ttu-id="64b6e-130">使用以下命令將 zip 檔案上傳到 HDInsight 叢集前端節點：</span><span class="sxs-lookup"><span data-stu-id="64b6e-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="64b6e-131">以 zip 檔案名稱取代 **FILENAME** 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="64b6e-132">以 HDInsight 叢集的 SSH 登入取代 **USERNAME** 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="64b6e-133">將 CLUSTERNAME 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="64b6e-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="64b6e-134">如果您使用密碼來驗證您的 SSH 登入，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="64b6e-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="64b6e-135">如果您使用的是公開金鑰，您可能必須使用 `-i` 參數並指定對應的私密金鑰路徑。</span><span class="sxs-lookup"><span data-stu-id="64b6e-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="64b6e-136">例如， `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`。</span><span class="sxs-lookup"><span data-stu-id="64b6e-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="64b6e-137">完成上傳之後，使用 SSH 連線到叢集：</span><span class="sxs-lookup"><span data-stu-id="64b6e-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="64b6e-138">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="64b6e-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="64b6e-139">連線之後，請使用以下命令解壓縮 .zip 檔案：</span><span class="sxs-lookup"><span data-stu-id="64b6e-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="64b6e-140">此命令會解壓縮一個 .csv 檔案 (約為 60MB)。</span><span class="sxs-lookup"><span data-stu-id="64b6e-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="64b6e-141">使用下列命令在 HDInsight 儲存體上建立目錄，然後將檔案複製到目錄︰</span><span class="sxs-lookup"><span data-stu-id="64b6e-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="64b6e-142">建立並執行 HiveQL</span><span class="sxs-lookup"><span data-stu-id="64b6e-142">Create and run the HiveQL</span></span>

<span data-ttu-id="64b6e-143">使用下列步驟將 CSV 檔案的資料匯入到名為 **Delays**的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="64b6e-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="64b6e-144">使用以下命令建立並編輯名為 **flightdelays.hql** 的新檔案：</span><span class="sxs-lookup"><span data-stu-id="64b6e-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="64b6e-145">使用下列文字做為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="64b6e-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="64b6e-146">若要儲存檔案，請按 **Ctrl + X**，再按 **Y**。</span><span class="sxs-lookup"><span data-stu-id="64b6e-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="64b6e-147">若要啟動 Hive 並執行 **flightdelays.hql** 檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="64b6e-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="64b6e-148">此範例會使用 `localhost`，因為您是連接到 HDInsight 叢集的前端節點，也就是 HiveServer2 執行所在位置。</span><span class="sxs-lookup"><span data-stu-id="64b6e-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="64b6e-149">當 __flightdelays.hql__指令碼執行完畢之後，請使用下列命令來開啟互動式 Beeline 工作階段：</span><span class="sxs-lookup"><span data-stu-id="64b6e-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="64b6e-150">當您接收 `jdbc:hive2://localhost:10001/>` 提示字元時，請使用以下查詢從匯入的航班延誤資料中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="64b6e-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="64b6e-151">此查詢會擷取因氣候因素而延誤的城市清單，以及平均延誤時間，並會儲存到 `/tutorials/flightdelays/output`。</span><span class="sxs-lookup"><span data-stu-id="64b6e-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="64b6e-152">稍後，Sqoop 會從此位置讀取該資料，並匯出到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="64b6e-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="64b6e-153">若要結束 Beeline，請在提示字元中輸入 `!quit` 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="64b6e-154">建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="64b6e-154">Create a SQL Database</span></span>

<span data-ttu-id="64b6e-155">如果您已經有 SQL Database，就必須取得伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="64b6e-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="64b6e-156">您可以在 [Azure 入口網站](https://portal.azure.com)中找到伺服器名稱，方法是選取 [SQL Database]，然後篩選您想要使用的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="64b6e-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="64b6e-157">伺服器名稱會列在 [伺服器]  資料行中。</span><span class="sxs-lookup"><span data-stu-id="64b6e-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="64b6e-158">如果您還沒有 SQL Database，請使用 [SQL Database 教學課程：在幾分鐘內建立 SQL Database](../sql-database/sql-database-get-started.md) 中的相關資訊來建立一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b6e-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="64b6e-159">儲存用於資料庫的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="64b6e-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="64b6e-160">建立 SQL Database 資料表</span><span class="sxs-lookup"><span data-stu-id="64b6e-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="64b6e-161">連接至 SQL Database 並建立資料表的方法有很多種。</span><span class="sxs-lookup"><span data-stu-id="64b6e-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="64b6e-162">下列步驟會從 HDInsight 叢集使用 [FreeTDS](http://www.freetds.org/) 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="64b6e-163">使用 SSH 連線到 Linux 型 HDInsight 叢集，並從 SSH 工作階段執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="64b6e-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="64b6e-164">使用下列命令來安裝 FreeTDS：</span><span class="sxs-lookup"><span data-stu-id="64b6e-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="64b6e-165">安裝完成後，請使用下列命令來連接到 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="64b6e-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="64b6e-166">使用 SQL Database 伺服器名稱取代 **serverName** 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="64b6e-167">使用 SQL Database 的登入取代 **adminLogin** 和 **adminPassword**。</span><span class="sxs-lookup"><span data-stu-id="64b6e-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="64b6e-168">使用資料庫名稱取代 **databaseName** 。</span><span class="sxs-lookup"><span data-stu-id="64b6e-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="64b6e-169">您會收到如以下文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="64b6e-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="64b6e-170">在 `1>` 提示字元輸入下列幾行：</span><span class="sxs-lookup"><span data-stu-id="64b6e-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="64b6e-171">輸入 `GO` 陳述式後，將評估先前的陳述式。</span><span class="sxs-lookup"><span data-stu-id="64b6e-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="64b6e-172">此查詢會建立名為 **delays** 的資料表 (具有叢集索引)。</span><span class="sxs-lookup"><span data-stu-id="64b6e-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="64b6e-173">使用下列查詢來確認已建立資料表：</span><span class="sxs-lookup"><span data-stu-id="64b6e-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="64b6e-174">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="64b6e-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="64b6e-175">在 `exit` at the `1>` 以結束 tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="64b6e-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="64b6e-176">使用 Sqoop 匯出資料</span><span class="sxs-lookup"><span data-stu-id="64b6e-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="64b6e-177">使用下列命令以確認 Sqoop 看得見您的 SQL Database：</span><span class="sxs-lookup"><span data-stu-id="64b6e-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="64b6e-178">此命令會傳回一份資料庫清單，包含您稍早在其中建立 delays 資料表的資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b6e-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="64b6e-179">使用以下命令，將資料從 hivesampletable 匯出至 mobiledata 資料表：</span><span class="sxs-lookup"><span data-stu-id="64b6e-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="64b6e-180">Sqoop 會連接到包含 delays 資料表的資料庫，並將資料從 `/tutorials/flightdelays/output` 目錄匯出至 delays 資料表。</span><span class="sxs-lookup"><span data-stu-id="64b6e-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="64b6e-181">在命令完成後，使用下列程式碼連接至使用 TSQL 的資料庫：</span><span class="sxs-lookup"><span data-stu-id="64b6e-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="64b6e-182">連線之後，使用下列陳述式來確認資料已匯出到 mobiledata 資料表：</span><span class="sxs-lookup"><span data-stu-id="64b6e-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="64b6e-183">您應會看到資料表中的資料清單。</span><span class="sxs-lookup"><span data-stu-id="64b6e-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="64b6e-184">輸入 `exit` 以結束 tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="64b6e-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="64b6e-185"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="64b6e-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="64b6e-186">若要了解更多 HDInsight 中資料的使用方式，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="64b6e-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="64b6e-187">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="64b6e-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="64b6e-188">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="64b6e-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="64b6e-189">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="64b6e-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="64b6e-190">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="64b6e-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="64b6e-191">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="64b6e-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="64b6e-192">[開發適用於 HDInsight 的 Python Hadoop 串流程式][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="64b6e-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
