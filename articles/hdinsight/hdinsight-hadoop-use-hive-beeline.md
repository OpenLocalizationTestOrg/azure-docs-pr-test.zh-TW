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
# <a name="use-hello-beeline-client-with-apache-hive"></a>使用 Apache Hive hello Beeline 用戶端

深入了解如何 toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive 查詢 HDInsight 上。

Beeline 是包含 hello 的 HDInsight 叢集的前端節點的登錄區用戶端。 Beeline 會使用 JDBC tooconnect tooHiveServer2，您的 HDInsight 叢集上裝載的服務。 您也可以使用 Beeline tooaccess Hive HDInsight 上從遠端透過 hello 網際網路。 下表中的 hello 搭配 Beeline 提供連接字串：

| 您執行 Beeline 的來源 | 參數 |
| --- | --- | --- |
| SSH 連線 tooa 叢集前端節點或邊緣節點 | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| 外部 hello 叢集 | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> 取代`admin`與 hello 叢集登入帳戶，供您的叢集。
>
> 取代`password`hello hello 叢集登入帳戶的密碼。
>
> 取代`clustername`hello 名稱，為您的 HDInsight 叢集。

## <a id="prereq"></a>必要條件

* HDInsight 叢集上以 Linux 為基礎的 Hadoop。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* SSH 用戶端或本機 Beeline 用戶端。 大部分的這份文件中的 hello 步驟假設您使用 Beeline 從 SSH 工作階段 toohello 叢集中。 如需從外部 hello 叢集中執行 Beeline 資訊，請參閱 hello[從遠端使用 Beeline](#remote) > 一節。

    如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a id="beeline"></a>使用 BeeLine

1. 啟動 Beeline 時，您必須為 HDInsight 叢集上的 HiveServer2 提供連接字串。 從外部 hello 叢集 toorun hello 命令，您必須提供 hello 叢集登入帳戶名稱 (預設`admin`) 和密碼。 使用下列資料表 toofind hello 連接字串格式和參數 toouse hello:

    | 您執行 Beeline 的來源 | 參數 |
    | --- | --- | --- |
    | SSH 連線 tooa 叢集前端節點或邊緣節點 | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | 外部 hello 叢集 | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    比方說，下列命令的 hello 可以是從 SSH 工作階段 toohello 叢集中使用的 toostart Beeline:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    此命令啟動 hello Beeline 用戶端，並連接 tooHiveServer2 hello 叢集前端節點上。 Hello 命令完成之後，您會抵達`jdbc:hive2://headnodehost:10001/>`提示字元。

2. Beeline 命令以 `!` 字元開頭，例如 `!help` 顯示說明。 不過 hello`!`可以省略某些命令。 例如，`help` 也能運作。

    沒有`!sql`，而是使用的 tooexecute HiveQL 陳述式。 不過，下列 HiveQL 因此通常用於您可以省略上述 hello `!sql`。 hello 下列兩個陳述式是相等的：

    ```hiveql
    !sql show tables;
    show tables;
    ```

    新的叢集上只會列出一個資料表：**hivesampletable**。

3. 使用下列命令 toodisplay hello 結構描述的 hello hivesampletable hello:

    ```hiveql
    describe hivesampletable;
    ```

    此命令會傳回下列資訊的 hello:

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

    這項資訊會描述 hello hello 資料表中的資料行。 雖然我們無法執行一些查詢，針對此資料，讓我們改為建立全新的資料表 toodemonstrate 如何 Hive tooload 資料，並套用結構描述。

4. 輸入下列陳述式 toocreate 資料表名為 hello **log4jLogs**使用所提供與 hello HDInsight 叢集的範例資料：

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    這些陳述式會執行下列動作的 hello:

    * `DROP TABLE`-如果 hello 資料表存在，會將其刪除。

    * `CREATE EXTERNAL TABLE` - 在 Hive 中建立**外部**資料表。 外部資料表只會儲存在登錄區中的 hello 資料表定義。 hello 資料會保留在 hello 原始位置。

    * `ROW FORMAT`的 hello 資料格式化方式。 在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。

    * `STORED AS TEXTFILE LOCATION`-Hello 資料會儲存以及在何種檔案格式。

    * `SELECT`-選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。 此查詢會傳回值 **3** ，因為有 3 個資料列包含此值。

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive 嘗試 tooapply hello 結構描述 tooall 檔案 hello 目錄中。 在此情況下，hello 目錄包含不符合 hello 結構描述的檔案。 tooprevent 記憶體回收 hello 結果中的資料，此陳述式會告知登錄區，我們應該只會傳回資料從檔案結尾。 記錄檔。

  > [!NOTE]
  > 當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。 例如，自動化的資料上傳程序，或透過其他 MapReduce 作業。
  >
  > 卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。

    hello 輸出此命令為類似 toohello 下列文字：

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

5. tooexit Beeline，使用`!exit`。

## <a id="file"></a>使用 Beeline toorun HiveQL 檔案

使用下列步驟 toocreate 檔案，然後執行它使用 Beeline hello。

1. 使用 hello 下列命令 toocreate 名為**query.hql**:

    ```bash
    nano query.hql
    ```

2. 使用 hello hello hello 檔案內容為下列文字。 此查詢將建立名為 **errorLogs** 的新「內部」資料表：

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    這些陳述式會執行下列動作的 hello:

    * **建立資料表 IF NOT EXISTS** -如果 hello 資料表不存在，就會建立。 因為 hello**外部**不是關鍵字，這個陳述式會建立內部資料表。 內部資料表會儲存在 hello Hive 資料倉儲，而且都完全受登錄區。
    * **儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。 ORC 格式是高度最佳化且有效率的 Hive 資料儲存格式。
    * **INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。

    > [!NOTE]
    > 不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。

3. toosave hello 檔案，使用**Ctrl**+**_X**，然後輸入**Y**，最後再**Enter**。

4. 使用下列 toorun hello 檔使用 Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > hello`-i`參數啟動 Beeline，執行 hello hello query.hql 檔案中的陳述式。 Hello 查詢完成之後，到達 hello`jdbc:hive2://headnodehost:10001/>`提示字元。 您也可以執行檔案，使用 hello`-f`結束 Beeline hello 查詢完成後的參數。

5. hello 的 tooverify**錯誤記錄檔**建立資料表，請使用下列陳述式 tooreturn 所有 hello 中的資料列的 hello**錯誤記錄檔**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** ：

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>從遠端使用 Beeline

如果您有 Beeline 安裝在本機，或正在使用它透過 Docker 映像例如[sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/)，您必須使用下列參數的 hello:

* __連接字串__：`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __叢集登入名稱__：`-n admin`

* __叢集登入密碼__ `-p 'password'`

取代 hello `clustername` hello hello 名稱，為您的 HDInsight 叢集的連接字串中。

取代`admin`與叢集登入，以及取代 hello 名稱`password`hello 您叢集的登入的密碼。

## <a id="sparksql"></a>使用 Beeline 搭配 Spark

Spark 提供自己的 HiveServer2，通常是來參考 tooas hello Spark Thrift 伺服器實作。 此服務使用 Spark SQL tooresolve 查詢而不是登錄區，且可能會提供更佳的效能，根據您的查詢。

tooconnect toohello Spark Thrift 伺服器的 HDInsight 叢集，使用連接埠上的 Spark`10002`而不是`10001`。 例如： `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`。

> [!IMPORTANT]
> 無法直接存取 over hello 網際網路 hello Spark Thrift 伺服器。 您只能從為 SSH 工作階段連線 tooit 或內 hello 相同 Azure 虛擬網路如 hello HDInsight 叢集。

## <a id="summary"></a><a id="nextsteps"></a>後續步驟

多個一般 HDInsight 中的登錄區的詳細資訊，請參閱下列文件的 hello:

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需詳細資訊之其他方式，您可以使用 Hadoop HDInsight、 請參閱下列文件的 hello:

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

如果您正在使用 Hive Tez，請參閱下列文件的 hello:

* [使用 Windows 為基礎的 HDInsight 上的 hello Tez UI](hdinsight-debug-tez-ui.md)
* [使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視](hdinsight-debug-ambari-tez-view.md)

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
