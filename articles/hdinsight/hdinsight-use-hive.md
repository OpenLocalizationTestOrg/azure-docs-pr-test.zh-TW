---
title: "aaaWhat 是 Apache Hive 和 HiveQL-Azure HDInsight |Microsoft 文件"
description: "Apache Hive 是適用於 Hadoop 的資料倉儲系統。 您可以查詢資料儲存在登錄區利用 HiveQL，哪些類似 tooTransact SQL。 在這份文件，了解如何 toouse hive 控制檔和使用 Azure HDInsight HiveQL。"
keywords: "hiveql，什麼是登錄區，hadoop hiveql 如何 toouse hive 控制檔，了解什麼是登錄區的 hive"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Azure HDInsight 上的 Apache Hive 和 HiveQL 是什麼？

[Apache Hive](http://hive.apache.org/) 是適用於 Hadoop 的資料倉儲系統。 Hive 可執行資料摘要、查詢以及資料分析。 已寫入下列 HiveQL，也就是查詢語言類似 tooSQL hive 查詢。

登錄區可讓您 tooproject 結構上大部分的非結構化資料。 您可以定義 hello 結構之後，您可以使用 HiveQL tooquery hello 資料的 Java 或 MapReduce 不知情的情況下。

HDInsight 提供數種已針對特定工作負載進行微調的叢集類型。 下列叢集類型的 hello 最常使用 Hive 查詢：

* __互動式 Hive__： 提供的 Hadoop 叢集[低延遲分析處理 (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP)互動式查詢功能 tooimprove 回應時間。 如需詳細資訊，請參閱 hello[開頭 HDInsight 中的互動式 Hive](hdinsight-hadoop-use-interactive-hive.md)文件。

* __Hadoop__︰已針對批次處理工作負載進行微調的 Hadoop 叢集。 如需詳細資訊，請參閱 hello[啟動 HDInsight 中的 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)文件。

* __Spark__：Apache Spark 有可用於 Hive 的內建功能。 如需詳細資訊，請參閱 hello[開頭 HDInsight 上的 Spark](hdinsight-apache-spark-jupyter-spark-sql.md)文件。

* __對 HBase__: HiveQL 可以是使用的 tooquery 對 HBase 中所儲存的資料。 如需詳細資訊，請參閱 hello[開始在 HDInsight HBase](hdinsight-hbase-tutorial-get-started-linux.md)文件。

## <a name="how-toouse-hive"></a>如何 toouse hive 控制檔

使用下列資料表 toodiscover toouse hive 控制檔與 HDInsight hello:

| **使用此方法**，如果您想要... | ...一個 **互動式** 殼層 | ...**批次** 處理 | ...搭配此 **叢集作業系統** | ...從此 **用戶端作業系統** |
|:--- |:---:|:---:|:--- |:--- |
| [Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |任何 (以瀏覽器為基礎) |
| [Beeline 用戶端](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux、Unix、Mac OS X 或 Windows |
| [REST API](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux 或 Windows* |Linux、Unix、Mac OS X 或 Windows |
| [HDInsight Tools for Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux 或 Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux 或 Windows* |Windows |

> [!IMPORTANT]
> \*Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> 如果您使用 Windows 為基礎的 HDInsight 叢集，您可以使用 hello[查詢主控台](hdinsight-hadoop-use-hive-query-console.md)從瀏覽器或[遠端桌面](hdinsight-hadoop-use-hive-remote-desktop.md)toorun Hive 查詢。

## <a name="hiveql-language-reference"></a>HiveQL 語言參考

這個語言參考位於 hello[語言手動 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)。

## <a name="hive-and-data-structure"></a>Hive 和資料結構

登錄區了解與 toowork 的結構化和半結構化的資料。 例如，文字檔 hello 欄位，以特定字元分隔。 hello HiveQL 陳述式之後建立的資料表，以空格分隔的資料：

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive 也支援自訂複雜或不規則結構化資料的 **序列化/反序列化程式 (SerDe)** 。 如需詳細資訊，請參閱 hello[如何 toouse 與 HDInsight 自訂 JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx)文件。

如需有關登錄區所支援的檔案格式的詳細資訊，請參閱 hello[語言手動 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Hive 內部和外部資料表比較。

您可以使用 Hive 建立兩種類型的資料表：

* __內部__: hello Hive 資料倉儲中所儲存的資料。 hello 資料倉儲位於`/hive/warehouse/`hello hello 叢集的預設儲存體上。

    使用內部資料表的時機︰

    * 資料是暫存的。
    * 您想 Hive toomanage hello 生命週期的 hello 資料表和資料。

* __外部__： 資料會儲存外 hello 資料倉儲。 hello 資料可以儲存在任何可存取的存放裝置，由 hello 叢集。

    使用外部資料表的時機︰

    * hello 資料也會使用登錄區之外。 例如，hello 資料檔案會更新由其他處理序 （也就不會鎖定 hello 檔案。）
    * 需要 tooremain hello 基礎位置，即使之後卸除 hello 資料表中的資料。
    * 您需要自訂位置，例如非預設儲存體帳戶。
    * 登錄區以外的程式管理 hello 資料格式、 位置等等。

如需詳細資訊，請參閱 hello [hive 控制檔內部和外部資料表簡介][ cindygross-hive-tables]部落格文章。

## <a name="user-defined-functions-udf"></a>使用者定義函數 (UDF)

Hive 也可透過 **使用者定義函數 (UDF)**延伸。 UDF 可讓您 tooimplement 功能或 HiveQL 不容易模型化的邏輯。 使用 Hive Udf 的範例，請參閱下列文件的 hello:

* [將 Java 使用者定義的函式與 Hive 搭配使用](hdinsight-hadoop-hive-java-udf.md)

* [使用 Python 使用者定義的函式搭配 Hive 和 Pig](hdinsight-python.md)

* [使用 C# 使用者定義的函式搭配 Hive 和 Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [使用者定義的自訂 Hive tooadd tooHDInsight 的運作方式](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [範例登錄區的使用者定義函數 tooconvert 日期/時間格式 tooHive 時間戳記](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>範例資料

HDInsight 上的 Hive 已預先載入名為 `hivesampletable` 的內部資料表。 HDInsight 也提供可搭配 Hive 使用的範例資料集。 這些資料集儲存在 hello`/example/data`和`/HdiSamples`目錄。 這些目錄存在於 hello 預設儲存體叢集。

## <a id="job"></a>範例 Hive 查詢

hello 下列 HiveQL 陳述式投射資料行拖曳至 hello`/example/data/sample.log`檔案：

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

Hello 上述範例中，在 hello HiveQL 陳述式會執行下列動作的 hello:

* `set hive.execution.engine=tez;`： 設定 hello 執行引擎 toouse Tez。 使用 Tez 而非 MapReduce，可以提升查詢效能。 如需有關 Tez 的詳細資訊，請參閱 hello[來改善效能的使用 Apache Tez](#usetez) > 一節。

    > [!NOTE]
    > 只有在使用以 Windows 為基礎的 HDInsight 叢集時，才需要此陳述式。 Tez 是以 Linux 為基礎的 HDInsight hello 預設執行引擎。

* `DROP TABLE`： 如果 hello 資料表已經存在，請將它刪除。

* `CREATE EXTERNAL TABLE`：在 Hive 中建立新的**外部**資料表。 外部資料表只會儲存在登錄區中的 hello 資料表定義。 hello 原始位置，並以 hello 原始格式保留 hello 資料。

* `ROW FORMAT`： 會告知的 Hive hello 資料格式化的方式。 在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。

* `STORED AS TEXTFILE LOCATION`： 會告知 Hive 其中 hello 資料會儲存 (hello`example/data`目錄)，則會儲存為文字。 hello 資料可以在一個檔案，或分散 hello 目錄內的多個檔案。

* `SELECT`： 選取所有資料列計數，其中 hello 資料行**t4**包含 hello 值**[錯誤]**。 這個陳述式會傳回值 **3**，因為有三個資料列包含此值。

* `INPUT__FILE__NAME LIKE '%.log'`-Hive 嘗試 tooapply hello 結構描述 tooall 檔案 hello 目錄中。 在此情況下，hello 目錄包含不符合 hello 結構描述的檔案。 tooprevent 記憶體回收 hello 結果中的資料，此陳述式會告知登錄區，我們應該只會傳回資料從檔案結尾。 記錄檔。

> [!NOTE]
> 當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。 例如，自動化的資料上傳程序，或 MapReduce 作業。
>
> 卸除的外部資料表沒有**不**刪除 hello 資料，它只會刪除 hello 資料表定義。

toocreate**內部**而不是外部資料表，請使用下列 HiveQL hello:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

這些陳述式會執行下列動作的 hello:

* `CREATE TABLE IF NOT EXISTS`： 如果 hello 資料表不存在，建立它。 因為 hello**外部**不是關鍵字，這個陳述式會建立內部資料表。 hello 資料表儲存在 hello Hive 資料倉儲和 Hive 完全管理。

* `STORED AS ORC`: Hello 資料最佳化的資料列單欄式 (ORC) 格式儲存。 ORC 是高度最佳化且有效率的 Hive 資料儲存格式。

* `INSERT OVERWRITE ... SELECT`： 選取資料列從 hello **log4jLogs**資料表，其中包含**[錯誤]**，然後插入 hello 資料到 hello 和**錯誤記錄檔**資料表。

> [!NOTE]
> 不同於外部資料表，卸除內部資料表也會刪除 hello 基礎資料。

## <a name="improve-hive-query-performance"></a>改善 Hive 查詢效能

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org)是此架構可讓資料密集應用程式，例如登錄區，能更有效率地在標尺 toorun。 對於以 Linux 為基礎的 HDInsight 叢集，Tez 預設為開啟。

> [!NOTE]
> 對於 Windows 型的 HDInsight 叢集，Tez 目前預設為關閉，因而必須啟用。 Hive 查詢必須設定 tootake 優點 Tez，hello 下列值：
>
> `set hive.execution.engine=tez;`
>
> Tez 是 hello 預設引擎以 Linux 為基礎的 HDInsight 叢集。

hello [Hive Tez 設計文件上](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)包含 hello 實作選項和微調組態詳細資料。

使用 Tez tooaid 偵錯作業中的執行，HDInsight 提供下列 Tez 工作的 tooview 詳細資料可讓您的 web Ui 的 hello:

* [使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視](hdinsight-debug-ambari-tez-view.md)

* [使用 Windows 為基礎的 HDInsight 上的 hello Tez UI](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>低延遲分析處理 (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (有時也稱為 Live Long and Process) 是 Hive 2.0 的新功能，允許在記憶體中快取查詢。 LLAP 會更快，向上的 Hive 查詢太[26 x 比 Hive 在某些情況下 1.x](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/)。

HDInsight 提供 LLAP hello 互動式 Hive 叢集類型中。 如需詳細資訊，請參閱 hello[開頭互動式 Hive](hdinsight-hadoop-use-interactive-hive.md)文件。

## <a name="hive-jobs-and-sql-server-integration-services"></a>Hive 工作和 SQL Server 整合服務

您可以使用 SQL Server Integration Services (SSIS) toorun Hive 工作。 hello Azure Feature Pack for SSIS 提供 hello 遵循使用 HDInsight 的登錄區工作的元件。

* [Azure HDInsight Hive 工作][hivetask]

* [Azure 訂用帳戶連接管理員][connectionmanager]

深入了解 hello Azure Feature Pack for SSIS[這裡][ssispack]。

## <a id="nextsteps"></a>接續步驟

既然您已經學會 Hive 的是，以及如何使用 hello 下列 HDInsight 中的 Hadoop 連結 tooexplore Azure HDInsight 以其他方式 toowork toouse。

* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
