---
title: "aaaAnalyze Spark-Azure 中的 Python 程式庫的網站記錄檔 |Microsoft 文件"
description: "筆記本會示範如何 tooanalyze 記錄 Azure HDInsight 上的 Spark 中使用自訂的程式庫的資料。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>使用自訂 Python 程式庫搭配 HDInsight 上的 Spark 叢集來分析網站記錄

筆記本會示範如何 tooanalyze 記錄 HDInsight 上的 Spark 中使用自訂的程式庫的資料。 我們使用 hello 自訂文件庫是 Python 程式庫呼叫**iislogparser.py**。

> [!TIP]
> 本教學課程也適用於您在 HDInsight 中所建立 Spark (Linux) 叢集上的 Jupyter Notebook。 hello 筆記本體驗可讓您從本身的 hello 筆記本執行 hello Python 程式碼片段。 tooperform hello 教學課程中的筆記本內建立 Spark 叢集，請啟動 Jupyter 筆記本 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 hello 筆記本**分析記錄檔與使用自訂 library.ipynb Spark**下 hello **PySpark**資料夾。
>
>

**先決條件：**

您必須擁有 hello 下列：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="save-raw-data-as-an-rdd"></a>將原始資料儲存為 RDD
在本節中，我們使用 hello [Jupyter](https://jupyter.org)筆記本 HDInsight toorun 工作處理未經處理的範例資料，並將它儲存為 Hive 資料表中的 Apache Spark 叢集相關聯。 上的.csv 檔案 (hvac.csv) 使用預設的所有叢集 hello 範例資料。

一旦您的資料會儲存為 Hive 資料表，在 hello 下一節我們將連接使用 BI 工具，例如 Power BI 和 Tableau toohello Hive 資料表。

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   
2. 從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. 建立新的 Notebook。 按一下 新增，然後按一下PySpark。

    ![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")
4. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。

    ![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "提供 hello 筆記本的名稱")
5. 因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。 您可以啟動匯入此案例所需的 hello 型別。 貼上下列程式碼片段中的空白儲存格，hello，然後按下**SHIFT + ENTER**。

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. 建立 hello 叢集上使用 hello 範例記錄檔資料已提供 RDD。 您可以存取 hello 與 hello 叢集相關聯的預設儲存體帳戶中的 hello 資料**\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**。

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. 範例記錄檔設定 tooverify 該 hello 前一步驟已順利完成的擷取。

        logs.take(5)

    您應該會看到類似 toohello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>使用自訂 Python 程式庫來分析記錄資料
1. 上述 hello 輸出前, 幾行 hello 包含 hello 標頭資訊和每個其餘的列符合該標頭中所述的 hello 結構描述。 剖析這類記錄檔可能是複雜的作業。 因此，我們使用自訂 Python 程式庫 (**iislogparser.py**)，它可大幅簡化這類記錄檔的剖析。 依預設，此程式庫會包含在位於以下位置的 HDInsight 上的 Spark 叢集中： **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**。

    不過，此程式庫不在 hello`PYTHONPATH`因此我們使用類似的匯入陳述式不能使用它`import iislogparser`。 toouse 此程式庫，我們必須將它散發 tooall hello 背景工作節點。 執行下列程式碼片段的 hello。

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`提供函式`parse_log_line`傳回`None`記錄列標頭資料列，並且傳回 hello 的執行個體如果`LogLine`遇到記錄列類別。 使用 hello`LogLine`類別 tooextract 只 hello hello RDD 中的記錄程式行：

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. 擷取 hello 步驟已順利完成的擷取的記錄行 tooverify 數。

       logLines.take(2)

   hello 輸出應類似 toohello 下列：

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. hello`LogLine`類別，又具有一些有用的方法，例如`is_error()`，它會傳回記錄項目是否有錯誤程式碼。 使用錯誤此 toocompute hello 數目 hello 擷取記錄行，並再記錄所有 hello 錯誤 tooa 不同的檔案。

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   您應該會看到類似 hello 下列輸出：

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. 您也可以使用**Matplotlib** tooconstruct 的 hello 資料視覺效果。 例如，如果您想 tooisolate hello 造成長時間執行的要求，您可以採取 hello 大部分時間 tooserve 平均 toofind hello 檔案。
   hello 以下程式碼片段會擷取 hello 前 25 資源所花費大部分時間 tooserve 要求。

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   您應該會看到類似 hello 下列輸出：

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. 您也可以呈現 hello 表單區域的這項資訊。 第一個步驟 toocreate 繪圖，讓我們先建立暫存資料表**AverageTime**。 如果在任何特定時間沒有任何不尋常的延遲尖峰時間 toosee 記錄 hello 資料表群組 hello。

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. 然後，您可以執行下列 SQL 查詢 tooget hello hello 的所有記錄中 hello **AverageTime**資料表。

       %%sql -o averagetime
       SELECT * FROM AverageTime

   hello `%%sql` magic 後面`-o averagetime`可確保 hello 查詢的 hello 輸出保存在本機上 hello Jupyter 伺服器 （通常 hello 叢集的前端節點 hello 叢集）。 hello 輸出會保存為[熊](http://pandas.pydata.org/)資料框架 hello 與指定名稱**averagetime**。

   您應該會看到類似 hello 下列輸出：

   ![SQL 查詢輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 查詢輸出")

   如需有關 hello `%%sql` magic，請參閱[hello 的支援參數 %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。
7. 您現在可以使用 Matplotlib、 文件庫使用的資料，toocreate 繪圖 tooconstruct 視覺效果。 因為必須從本機 hello 建立 hello 圖保存**averagetime**資料框架，hello 程式碼片段必須以 hello 開頭`%%local`識別常數。 這可確保 hello 程式碼在本機執行 hello Jupyter 伺服器上。

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   您應該會看到類似 hello 下列輸出：

   ![Matplotlib 輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 輸出")
8. 當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。 這將會關機並關閉 hello 筆記本。

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
