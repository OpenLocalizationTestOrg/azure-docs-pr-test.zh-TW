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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>在以 Linux 為基礎的 HDInsight 上使用 Hive 分析航班延誤資料

了解如何以 Linux 為基礎的 HDInsight 上使用 Hive 則 tooanalyze 飛行延遲資料匯出 hello 資料 tooAzure SQL Database 使用 Sqoop。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

### <a name="prerequisites"></a>必要條件

* **HDInsight 叢集**。 請參閱[在 Linux 上於 HDInsight 中搭配使用 Hadoop 與 Hive 入門](hdinsight-hadoop-linux-tutorial-get-started.md) ，取得建立新的 Linux 型 HDInsight 叢集的步驟。

* **Azure SQL Database**。 您會使用 Azure SQL Database 做為目的地資料存放區。 如果您還沒有 SQL Database，請參閱 [SQL Database 教學課程：在幾分鐘內建立 SQL Database](../sql-database/sql-database-get-started.md)。

* **Azure CLI**。 如果您尚未安裝 hello Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)的更多的步驟。

## <a name="download-hello-flight-data"></a>下載 hello 飛行資料

1. 瀏覽過[研究和創新的技術管理、 運輸局所免費提供統計][rita-website]。

2. 在 hello 頁面上，選取下列值的 hello:

   | 名稱 | 值 |
   | --- | --- |
   | 篩選年份 |2013 |
   | 篩選期間 |一月 |
   | 欄位 |Year、FlightDate、UniqueCarrier、Carrier、FlightNum、OriginAirportID、Origin、OriginCityName、OriginState、DestAirportID、Dest、DestCityName、DestState、DepDelayMinutes、ArrDelay、ArrDelayMinutes、CarrierDelay、WeatherDelay、NASDelay、SecurityDelay、LateAircraftDelay。 清除所有其他欄位 |

3. 按一下 [下載] 。

## <a name="upload-hello-data"></a>上傳 hello 資料

1. 使用下列命令 tooupload hello zip 檔案 toohello HDInsight 叢集前端節點的 hello:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    取代**FILENAME** hello hello zip 檔案的名稱。 取代**USERNAME**與 hello hello HDInsight 叢集的 SSH 登入。 CLUSTERNAME 取代 hello hello HDInsight 叢集名稱。

   > [!NOTE]
   > 如果您使用密碼 tooauthenticate SSH 登入，系統會提示您輸入 hello 密碼。 如果您使用公開金鑰，您可能需要 toouse hello`-i`參數並指定 hello 路徑 toohello 相符的私密金鑰。 例如： `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`。

2. Hello 上傳完成後，請使用 SSH toohello 叢集的連線：

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. 一旦連接之後，請使用下列 toounzip hello.zip 檔 hello:

    ```
    unzip FILENAME.zip
    ```

    此命令會解壓縮一個 .csv 檔案 (約為 60MB)。

4. 使用 hello HDInsight 存放區中，下列命令 toocreate 目錄並複製 hello 檔案 toohello 目錄：

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>建立和執行 hello HiveQL

使用 hello 下列步驟從 hello CSV 檔案至名為的 Hive 資料表 tooimport 資料**延遲**。

1. 使用 hello 下列命令 toocreate 和編輯新的檔案命名為**flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    使用 hello hello 這個檔案的內容為下列文字：

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

2. toosave hello 檔案，使用**Ctrl + X**，然後**Y** 。

3. toostart Hive 和執行的 hello **flightdelays.hql**檔案，請使用下列命令的 hello:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > 在此範例中，`localhost`因為您是連接的 toohello hello HDInsight 叢集，也就是正在 HiveServer2 前端節點。

4. 一次 hello __flightdelays.hql__完成執行時，使用 hello 下列命令 tooopen 互動式 Beeline 工作階段的指令碼：

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. 當您收到 hello`jdbc:hive2://localhost:10001/>`提示，請使用 匯入的 hello 飛行延遲資料中的下列查詢 tooretrieve 資料 hello。

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    此查詢會擷取一份城市有經驗的天氣延遲，以及 hello 平均延遲時間，並將它儲存到太`/tutorials/flightdelays/output`。 稍後，Sqoop 讀取 hello 資料從這個位置，將它匯出 tooAzure SQL 資料庫。

6. tooexit Beeline，輸入`!quit`在 hello 提示字元。

## <a name="create-a-sql-database"></a>建立 SQL Database

如果您已經有 SQL 資料庫，您必須取得 hello 伺服器名稱。 您可以在 hello 找到 hello 伺服器名稱[Azure 入口網站](https://portal.azure.com)選取**SQL 資料庫**，然後在 hello hello 名稱上篩選資料庫和想 toouse。 hello 伺服器名稱會列在 hello**伺服器**資料行。

如果您已經沒有 SQL 資料庫，使用中的 hello 資訊[SQL Database 教學課程： 建立 SQL 資料庫，以分鐘為單位](../sql-database/sql-database-get-started.md)toocreate 其中一個。 儲存 hello hello 資料庫所使用的伺服器名稱。

## <a name="create-a-sql-database-table"></a>建立 SQL Database 資料表

> [!NOTE]
> 有許多方式 tooconnect tooSQL 資料庫及建立資料表。 hello 下列步驟使用[freetds 才能使用](http://www.freetds.org/)從 hello HDInsight 叢集。


1. 使用 SSH tooconnect toohello 以 Linux 為基礎的 HDInsight 叢集，並執行下列步驟從 hello SSH 工作階段的 hello。

2. 使用下列命令 tooinstall freetds 才能使用 hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Hello 安裝完成之後，請使用下列命令 tooconnect toohello SQL Database 伺服器 hello。 取代**serverName** hello SQL Database 伺服器名稱。 取代**adminLogin**和**adminPassword**與 SQL Database 的 hello 登入。 取代**databaseName** hello 資料庫名稱。

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    您收到的輸出類似 toohello 下列文字：

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. 在 hello`1>`提示字元中，輸入下列行 hello:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。 此查詢會建立名為 **delays** 的資料表 (具有叢集索引)。

    已建立下列 hello 資料表的查詢 tooverify 使用 hello:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    hello 輸出是類似 toohello 下列文字：

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. 輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。

## <a name="export-data-with-sqoop"></a>使用 Sqoop 匯出資料

1. 使用下列命令 tooverify Sqoop 可以看到您的 SQL Database 的 hello:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    此命令會傳回一份資料庫，包括您稍早建立 hello 延遲資料表中的 hello 資料庫。

2. 使用 hello hivesampletable toohello mobiledata 資料表中的下列命令 tooexport 資料：

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop 連接 toohello 資料庫包含 hello 延遲資料表，並將資料從 hello 匯出`/tutorials/flightdelays/output`目錄 toohello 延遲資料表。

3. Hello 命令完成之後，使用下列 tooconnect toohello 資料庫使用 TSQL hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    一旦連接之後，使用下列陳述式 tooverify hello 資料已匯出的 toohello mobiledata 資料表 hello:

    ```
    SELECT * FROM delays
    GO
    ```

    您應該會看到 hello 資料表中資料的清單。 型別`exit`tooexit hello tsql 公用程式。

## <a id="nextsteps"></a> 後續步驟

toolearn HDInsight 中的資料的多個方式 toowork 請參閱下列文件 hello:

* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]
* [搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]
* [開發適用於 HDInsight 的 Python Hadoop 串流程式][hdinsight-develop-streaming]

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
