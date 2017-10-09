---
title: "aaaAnalyze Application Insight 記錄與 Spark-Azure HDInsight |Microsoft 文件"
description: "了解如何 tooexport Application Insight 記錄 tooblob 存放裝置，，然後使用 HDInsight 上的 Spark 中分析 hello 記錄檔。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>使用 HDInsight 上的 Spark 分析 Application Insights 遙測記錄檔

深入了解如何 toouse 二手上 HDInsight tooanalyze Application Insight 遙測資料。

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) 是一項分析服務，可監視您的 Web 應用程式。 Application Insights 所產生的遙測資料可以是匯出的 tooAzure 儲存體。 HDInsight 一旦 hello 資料是在 Azure 儲存體之後, 才能使用的 tooanalyze 它。

## <a name="prerequisites"></a>必要條件

* 應用程式設定 toouse Application Insights。

* 熟悉以 Linux 為基礎的 HDInsight 叢集的建立程序。 如需詳細資訊，請參閱[在 HDInsight 中建立 Spark](hdinsight-apache-spark-jupyter-spark-sql.md)。

  > [!IMPORTANT]
  > 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* 網頁瀏覽器。

hello 下列資源用於開發和測試本文件中：

* Application Insights 遙測資料使用產生[Node.js web 應用程式設定 toouse Application Insights](../application-insights/app-insights-nodejs.md)。

* Linux 上的 Spark HDInsight 叢集版本 3.5 已使用的 tooanalyze hello 資料。

## <a name="architecture-and-planning"></a>架構與規劃

hello 下列圖表說明此範例中的 hello 服務架構：

![圖中顯示資料流動從 Application Insights tooblob 儲存體，則正在處理的 HDInsight 上的 Spark](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Azure 儲存體

Application Insights 可以設定的 toocontinuously 匯出遙測資訊 tooblobs。 HDInsight 然後可以讀取的資料儲存在 hello blob。 不過，有一些您必須遵守的需求︰

* **位置**： 如果 hello 儲存體帳戶與 HDInsight 是在不同的位置，但是可能會增加延遲。 因為輸出費用套用的 toodata 區域之間移動，它也會增加成本。

    > [!WARNING]
    > 不支援在與 HDInsight 不同的位置使用儲存體帳戶。

* **blob 類型**：HDInsight 僅支援區塊 blob。 Application Insights 預設 toousing 區塊 blob，因此應該根據預設，使用 HDInsight 工作。

如需加入額外的儲存體 tooan 現有 HDInsight 叢集的資訊，請參閱 hello[新增額外的儲存體帳戶](hdinsight-hadoop-add-storage.md)文件。

### <a name="data-schema"></a>資料結構描述

Application Insights 提供[匯出資料模型](../application-insights/app-insights-export-data-model.md)匯出 tooblobs hello 遙測資料格式的資訊。 本文件中的 hello 步驟使用 Spark SQL toowork hello 資料。 Spark SQL 可以自動產生記錄的 Application Insights hello JSON 資料結構的結構描述。

## <a name="export-telemetry-data"></a>匯出遙測資料

中的 hello 步驟[設定連續匯出](../application-insights/app-insights-export-telemetry.md)tooconfigure 您 Application Insights tooexport 遙測資訊 tooan Azure 儲存體 blob。

## <a name="configure-hdinsight-tooaccess-hello-data"></a>設定 HDInsight tooaccess hello 資料

如果您要建立的 HDInsight 叢集，請在叢集建立期間新增 hello 儲存體帳戶。

tooadd hello Azure 儲存體帳戶 tooan 現有的叢集，請使用中 hello hello 資訊[新增額外的儲存體帳戶](hdinsight-hadoop-add-storage.md)文件。

## <a name="analyze-hello-data-pyspark"></a>分析 hello 資料： PySpark

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集上的 Spark。 從 hello**快速連結**區段中，選取**叢集儀表板**，然後選取**Jupyter 筆記本**從 hello 叢集 Dashboard__ 刀鋒視窗。

    ![hello 叢集儀表板](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. 在 hello 右上角的 hello Jupyter 頁面、 選取**新增**，然後**PySpark**。 隨即開啟新的瀏覽器索引標籤，其中包含以 Python 為基礎的 Jupyter Notebook。

3. Hello 第一個欄位中 (稱為**儲存格**) hello 頁面上，輸入下列文字的 hello:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    此程式碼會設定 Spark toorecursively 存取 hello 目錄結構 hello 輸入資料。 Application Insights 遙測是記錄的 tooa 目錄結構類似 toohello `/{telemetry type}/YYYY-MM-DD/{##}/`。

4. 使用**SHIFT + ENTER** toorun hello 程式碼。 上的 hello 資料格，左方的 hello '\*' hello 這個資料格中的程式碼正在執行 hello 方括號 tooindicate 之間會出現。 在完成，hello '\*' tooa 數目和底下 hello 資料格會顯示下列文字類似 toohello 輸出變更：

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Hello 底下建立新的儲存格第一次一個。 輸入下列文字放 hello 新儲存格的 hello。 取代`CONTAINER`和`STORAGEACCOUNT`hello Azure 儲存體帳戶名稱與包含 Application Insights 資料的 blob 容器名稱。

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    使用**SHIFT + ENTER** tooexecute 這個儲存格。 您會看到下列文字結果類似 toohello:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    傳回的 hello wasb 路徑是 hello hello Application Insights 遙測資料位置。 變更 hello `hdfs dfs -ls` hello 儲存格 toouse hello wasb 路徑傳回中的行，然後使用**SHIFT + ENTER**再次 toorun hello 儲存格。 這次 hello 結果應該會顯示 hello 目錄，其中包含遙測資料。

   > [!NOTE]
   > 本節中的步驟 hello hello 其餘部分，hello`wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests`目錄使用。 您的目錄結構可能不同。

6. 在 hello 下一個資料格中，輸入下列程式碼的 hello： 取代`WASB_PATH`hello hello 先前步驟中的路徑。

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    此程式碼會建立資料框架 hello 連續匯出程序所匯出的 hello JSON 檔案中。 使用**SHIFT + ENTER** toorun 這個儲存格。
7. 在 hello 下一個資料格中，輸入並執行下列建立 hello JSON 檔案的 Spark tooview hello 結構描述的 hello:

   ```python
   jsonData.printSchema()
   ```

    每種類型的遙測 hello 結構描述不相同。 hello 下列範例是產生的 web 要求的 hello 結構描述 (資料儲存在 hello`Requests`子目錄):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. 使用 hello 遵循 tooregister hello 資料框架的暫存資料表，並針對 hello 資料執行查詢：

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    此查詢會傳回其中 context.location.city 不是 null hello 前 20 筆記錄的 hello 縣 （市） 資訊。

   > [!NOTE]
   > hello 內容結構會出現在所有記錄的 Application Insights 的遙測資料。 hello 縣 （市） 項目可能不會填入您記錄中。 使用 hello 結構描述 tooidentify 其他項目，您可以查詢可能包含記錄資料。

    此查詢傳回的資訊類似 toohello 下列文字：

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>分析 hello 資料： Scala

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集上的 Spark。 從 hello**快速連結**區段中，選取**叢集儀表板**，然後選取**Jupyter 筆記本**從 hello 叢集 Dashboard__ 刀鋒視窗。

    ![hello 叢集儀表板](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. 在 hello 右上角的 hello Jupyter 頁面、 選取**新增**，然後**Scala**。 新的瀏覽器索引標籤隨即出現，其中包含以 Scala 為基礎的 Jupyter Notebook。
3. Hello 第一個欄位中 (稱為**儲存格**) hello 頁面上，輸入下列文字的 hello:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    此程式碼會設定 Spark toorecursively 存取 hello 目錄結構 hello 輸入資料。 Application Insights 遙測記錄 tooa 目錄結構類似太`/{telemetry type}/YYYY-MM-DD/{##}/`。

4. 使用**SHIFT + ENTER** toorun hello 程式碼。 上的 hello 資料格，左方的 hello '\*' hello 這個資料格中的程式碼正在執行 hello 方括號 tooindicate 之間會出現。 在完成，hello '\*' tooa 數目和底下 hello 資料格會顯示下列文字類似 toohello 輸出變更：

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Hello 底下建立新的儲存格第一次一個。 輸入下列文字放 hello 新儲存格的 hello。 取代`CONTAINER`和`STORAGEACCOUNT`使用 hello Azure 儲存體帳戶名稱和 blob 容器名稱，其中包含 Application Insights 記錄。

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    使用**SHIFT + ENTER** tooexecute 這個儲存格。 您會看到下列文字結果類似 toohello:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    傳回的 hello wasb 路徑是 hello hello Application Insights 遙測資料位置。 變更 hello `hdfs dfs -ls` hello 儲存格 toouse hello wasb 路徑傳回中的行，然後使用**SHIFT + ENTER**再次 toorun hello 儲存格。 這次 hello 結果應該會顯示 hello 目錄，其中包含遙測資料。

   > [!NOTE]
   > 本節中的步驟 hello hello 其餘部分，hello`wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests`目錄使用。 這個目錄可能不存在，除非您的遙測資料是用於 Web 應用程式。

6. 在 hello 下一個資料格中，輸入下列程式碼的 hello： 取代`WASB\_PATH`hello hello 先前步驟中的路徑。

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    此程式碼會建立資料框架 hello 連續匯出程序所匯出的 hello JSON 檔案中。 使用**SHIFT + ENTER** toorun 這個儲存格。

7. 在 hello 下一個資料格中，輸入並執行下列建立 hello JSON 檔案的 Spark tooview hello 結構描述的 hello:

   ```scala
   jsonData.printSchema
   ```

    每種類型的遙測 hello 結構描述不相同。 hello 下列範例是產生的 web 要求的 hello 結構描述 (資料儲存在 hello`Requests`子目錄):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. 使用 hello 遵循 tooregister hello 資料框架的暫存資料表，並針對 hello 資料執行查詢：

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    此查詢會傳回其中 context.location.city 不是 null hello 前 20 筆記錄的 hello 縣 （市） 資訊。

   > [!NOTE]
   > hello 內容結構會出現在所有記錄的 Application Insights 的遙測資料。 hello 縣 （市） 項目可能不會填入您記錄中。 使用 hello 結構描述 tooidentify 其他項目，您可以查詢可能包含記錄資料。
   >
   >

    此查詢傳回的資訊類似 toohello 下列文字：

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>後續步驟

如需使用 Spark toowork 資料與服務在 Azure 中的範例，請參閱下列文件的 hello:

* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

在建立及執行 Spark 應用程式的資訊，請參閱下列文件的 hello:

* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行工作](hdinsight-apache-spark-livy-rest-interface.md)
