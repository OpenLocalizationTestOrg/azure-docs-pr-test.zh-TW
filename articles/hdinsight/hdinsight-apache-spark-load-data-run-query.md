---
title: "aaaRun Azure HDInsight Spark 叢集上的互動式查詢 |Microsoft 文件"
description: "如何 toocreate Apache Spark 叢集在 HDInsight 上的 HDInsight Spark 快速入門。"
keywords: "spark 快速入門, 互動式 spark, 互動式查詢, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>在 HDInsight Spark 叢集上執行互動式查詢

在本文中，您可以使用 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢的 Spark 叢集。 Jupyter 筆記本是擴充 hello 主控台為基礎的互動體驗 toohello Web 瀏覽器型應用程式。 如需詳細資訊，請參閱[hello Jupyter 筆記本](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html)。

此教學課程中，您可以使用 hello **PySpark** hello Jupyter 筆記本 toorun 互動式 Spark SQL 查詢中的核心。 HDInsight 叢集上的 Jupyter Notebook 也支援其他兩個核心：**PySpark3** 和 **Spark**。 如需有關 hello 核心和使用的 hello 優點**PySpark**，請參閱[在 HDInsight 中的使用 Jupyter 筆記本核心使用 Apache Spark 叢集](hdinsight-apache-spark-jupyter-notebook-kernels.md)。

## <a name="prerequisites"></a>必要條件

* **Azure HDInsight Spark 叢集**。 如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>建立 Jupyter 筆記本 toorun 互動式查詢

toorun 查詢，我們會使用預設 hello 與 hello 叢集相關聯的儲存體中可用的範例資料。 不過，您必須先將該資料載入到 Spark 作為資料框架。 一旦您擁有 hello 資料框架，您可以使用來 hello Jupyter 筆記本執行查詢。 在本節中，您要查看如何：

* 註冊範例資料集作為 Spark 資料框架。
* Hello 資料框架上執行查詢。

1. 開啟 hello [Azure 入口網站](https://portal.azure.com/)。 如果您選擇 toopin hello 叢集 toohello 儀表板，按一下 hello 叢集磚的 hello 儀表板 toolaunch hello 叢集刀鋒視窗。

    如果您沒有不固定 hello 叢集 toohello 儀表板，從 hello 左窗格中，按一下**HDInsight 叢集**，然後按一下您所建立的 hello 叢集。

3. 從 快速連結，按一下 叢集儀表板，然後按一下Jupyter Notebook。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   ![開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")

   > [!NOTE]
   > 您也可以透過下列 URL 在瀏覽器中開啟 hello 叢集存取 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. 建立 Notebook。 按一下 新增，然後按一下PySpark。

   ![建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")

   建立新的記事本，並開啟 hello 名稱 Untitled(Untitled.pynb)。

4. 按一下頂端 hello hello 筆記本名稱，然後輸入易記的名稱，如果您想。

    ![提供查詢的名稱 hello Jupter 筆記本 toorun 互動式 Spark 從](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "提供 hello Jupter 筆記本 toorun 互動式 Spark 中查詢的名稱")

5. 貼上 hello 下列空的資料格中的程式碼，然後按下**SHIFT + ENTER** toorun hello 程式碼。 hello 程式碼會匯入這個案例所需的 hello 類型：

        from pyspark.sql.types import *

    因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容會自動建立，當您執行 hello 第一個程式碼儲存格。

    ![互動式 Spark SQL 查詢的狀態](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "互動式 Spark SQL 查詢的狀態")

    每次您在 Jupyter 執行互動式的查詢，您的 web 瀏覽器視窗標題顯示**（忙碌）**狀態以及 hello 筆記本標題。 另請參閱實心圓的下一個 toohello **PySpark** hello 右上角中的文字。 Hello 作業完成之後，它會變更 tooa 空心圓圈。

6. Hello 資料載入的 Spark 叢集之前，可讓我們看它的快照集。 hello 在本教學課程使用範例資料可做為 CSV 檔案 HDInsight Spark 叢集，在所有**\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**。 hello 資料擷取建築物 hello 溫度的變化。 以下是 hello hello 資料前的幾個資料列。

    ![互動式 Spark SQL 查詢的資料快照集](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "互動式 Spark SQL 查詢的資料快照集")

6. 建立資料框架和暫存資料表 (**hvac**) 藉由執行下列程式碼的 hello。 此教學課程中，我們不要建立 hello 的所有資料行 hello 暫存資料表中做為比較的 toohello hello 未經處理的 CSV 資料中的資料行。 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Hello 資料表建立之後，執行互動式查詢 hello 資料上使用下列程式碼的 hello。

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   因為您使用 PySpark 核心，您現在可以直接執行互動式的 SQL 查詢 hello 暫存資料表上**hvac**您建立使用 hello`%%sql`識別常數。 如需有關 hello`%%sql`魔法和其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。

   根據預設，會顯示 hello 遵循表格式輸出。

     ![互動式 Spark 查詢結果的資料表輸出](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "互動式 Spark 查詢結果的資料表輸出")

    您也可以查看其他視覺效果中的 hello 結果。 例如，區域圖相同的輸出會如下 hello 示 hello。

    ![互動式 Spark 查詢結果的區域圖表](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "互動式 Spark 查詢結果的區域圖表")

9. 您完成執行後，hello 應用程式，請關閉 hello 筆記本 toorelease hello 叢集資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。

## <a name="next-step"></a>後續步驟

在這個發行項您學到如何 toorun 使用 Jupyter 筆記本的 Spark 中的互動式查詢。 前進 toohello 如何您的 Spark 中註冊的 hello 資料可以提取下一個發行項 toosee 到 Power BI 等 Tableau BI 分析工具。 

> [!div class="nextstepaction"]
>[使用資料視覺效果工具搭配 Azure HDInsight 的 Spark BI](hdinsight-apache-spark-use-bi-tools.md)




