---
title: "使用 Curl HDInsight 的 Azure 中的 Hadoop Hive aaaUse |Microsoft 文件"
description: "了解如何 tooremotely 提交 Pig 工作 tooHDInsight 使用 Curl。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>使用 REST 以 HDInsight 中的 Hadoop 執行 Hive 查詢

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

了解如何 toouse hello WebHCat REST API toorun Hive 查詢的 Hadoop 上的 Azure HDInsight 叢集。

[Curl](http://curl.haxx.se/)是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求。 hello [jq](http://stedolan.github.io/jq/)公用程式是使用的 tooprocess REST 要求所傳回的 hello JSON 資料。

> [!NOTE]
> 如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱 hello[配備相關以 Linux 為基礎的 HDInsight 上的 Hadoop tooknow](hdinsight-hadoop-linux-information.md)文件。

## <a id="curl"></a>執行 Hive 查詢

> [!NOTE]
> 當使用 WebHCat cURL 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。
>
> 本章節中的 hello 命令，請將**USERNAME** hello 使用者 tooauthenticate toohello 叢集與取代**密碼**hello hello 使用者帳戶的密碼。 取代**CLUSTERNAME**與 hello 叢集的名稱。
>
> hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。 toohelp 確保您的認證會安全地傳送 toohello 伺服器，請務必要求使用安全 HTTP (HTTPS)。

1. 從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    您會收到回應類似 toohello 下列文字：

        {"status":"ok","version":"v1"}

    此命令中使用的 hello 參數如下所示：

   * **-u** -使用 tooauthenticate hello 要求 hello 使用者名稱和密碼。
   * **-G** - 指出此要求是 GET 作業。

     hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。 hello 路徑**/status**，表示該 hello 要求 tooreturn WebHCat (也稱為 Templeton) 狀態 hello 伺服器。 您也可以使用下列命令的 hello 要求 Hive hello 版本：

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     此要求會傳回回應類似 toohello 下列文字：

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. 遵循 toocreate 名為的資料表使用 hello **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    hello 遵循與這個要求所使用的參數：

   * **-d** -自`-G`不使用 hello 要求預設 toohello POST 方法。 `-d`指定傳送嗨資料值與 hello 要求。

     * **user.name** -hello 使用者執行 hello 命令。
     * **執行**-hello HiveQL 陳述式 tooexecute。
     * **statusdir** -寫入 hello 目錄 hello 這項作業的狀態。

     這些陳述式會執行下列動作的 hello:
   * **DROP TABLE** -如果 hello 資料表已經存在，就會刪除。
   * **CREATE EXTERNAL TABLE** - 在 Hive 中建立新的「外部」資料表。 外部資料表儲存區中的 hello 資料表定義。 hello 資料會保留在 hello 原始位置。

     > [!NOTE]
     > 當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。 例如，自動化的資料上傳程序，或其他 MapReduce 作業。
     >
     > 卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。

   * **資料列格式**-hello 資料格式化的方式。 每個記錄檔中的 hello 欄位會以空格分隔。
   * **儲存為文字檔位置**-hello 資料會儲存 （hello 範例/資料目錄），則會儲存為文字。
   * **選取**-選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。 這個陳述式會傳回值 **3**，因為有三個資料列包含此值。

     > [!NOTE]
     > 請注意 hello HiveQL 陳述式之間的空格會被 hello`+`字元 Curl 搭配使用時。 引號內的值包含空格，例如 hello 分隔符號應該不會被取代的`+`。

   * **'%25.log' 像 INPUT__FILE__NAME** -此陳述式的限制 hello 搜尋 tooonly 使用檔案結尾。 記錄檔。

     > [!NOTE]
     > hello`%25`是 %，hello URL 編碼形式，因此 hello 實際的條件是`like '%.log'`。 hello %有 toobe URL 編碼，因為它會被視為在 Url 中的特殊字元。

     此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼。

       {"id":"job_1415651640909_0026"}

3. hello 工作，下列命令使用 hello toocheck hello 狀態：

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    取代**JOBID** hello hello 上一個步驟中傳回的值。 例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後**JOBID**會`job_1415651640909_0026`。

    如果 hello 工作已完成，則會 hello 狀態**SUCCEEDED**。

   > [!NOTE]
   > 此 Curl 要求會傳回 JavaScript 物件標記法 (JSON) 文件以 hello 工作的相關資訊。 使用 Jq tooretrieve 只 hello 狀態值。

4. 一旦 hello hello 作業狀態已變更過**SUCCEEDED**，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。 hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， **/範例/curl**。 此位址在 hello 儲存 hello 輸出**範例/curl** hello 中的目錄的叢集預設儲存體。

    您可以列出並下載這些檔案使用 hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。 如需有關使用 Azure CLI hello 與 Azure 儲存體的詳細資訊，請參閱 hello[與 Azure 儲存體使用 Azure CLI 2.0](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs)文件。

5. 下列陳述式 toocreate 名為 'internal' 新的資料表使用 hello**錯誤記錄檔**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    這些陳述式會執行下列動作的 hello:

   * **CREATE TABLE IF NOT EXISTS** - 建立資料表 (如果不存在)。 此陳述式會建立內部資料表中，hello Hive 資料倉儲中所儲存且受完全登錄區。

     > [!NOTE]
     > 不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。

   * **儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。 ORC 是高度最佳化且有效率的 Hive 資料儲存格式。
   * **INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。
   * **選取**-選取所有資料列，從新的 hello**錯誤記錄檔**資料表。

6. 使用 hello 傳回 toocheck hello hello 工作狀態的作業識別碼。 成功後，使用 Azure CLI 如先前所述 toodownload 和檢視 hello 結果 hello。 hello 輸出應包含三行，其中包含**[錯誤]**。

## <a id="nextsteps"></a>接續步驟

Hive 與 HDInsight 搭配使用的一般資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:

* [使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視](hdinsight-debug-ambari-tez-view.md)

如需有關 hello 本文件中使用的 REST API 的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)文件。

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


