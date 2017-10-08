---
title: "使用 Azure HDInsight 上的 Spark 中 Jupyter aaaUse 自訂 Maven 套件 |Microsoft 文件"
description: "上如何 tooconfigure Jupyter 筆記本適用於 HDInsight Spark 叢集 toouse 自訂的 Maven 封裝的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝
> [!div class="op_single_selector"]
> * [使用資料格魔術](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [使用指令碼動作](hdinsight-apache-spark-python-package-installation.md)
>
>

了解如何 tooconfigure Jupyter 筆記本 HDInsight toouse 外部、 Apache Spark 叢集中社群貢獻**maven**不封裝在 hello 叢集中包含的方塊外。 

您可以搜尋 hello [Maven 儲存機制](http://search.maven.org/)如 hello 的封裝所提供的完整清單。 您也可以從其他來源取得可用套件清單。 例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。

在本文中，您將學習如何 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)與 hello Jupyter 筆記本的封裝。



## <a name="prerequisites"></a>必要條件
您必須擁有 hello 下列：

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="use-external-packages-with-jupyter-notebooks"></a>搭配 Jupyter Notebook 使用外部套件
1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   
2. 從 hello Spark 叢集刀鋒視窗中，按一下 **快速連結**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

    > [!NOTE]
    > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. 建立新的 Notebook。 按一下 新增，然後按一下Spark。
   
    ![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")

4. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。
   
    ![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "提供 hello 筆記本的名稱")

5. 您將使用 hello `%%configure` magic tooconfigure hello 筆記本 toouse 外部的封裝。 在使用外部封裝的筆記型電腦，請確定呼叫 hello `%%configure` magic hello 第一個程式碼的資料格。 這可確保該 hello 核心設定的 toouse hello 套件 hello 工作階段開始之前。

    >[!IMPORTANT] 
    >如果您忘記 tooconfigure hello 核心 hello 第一個資料格，您可以使用 hello`%%configure`以 hello`-f`參數，但會重新啟動 hello 工作階段，並將遺失所有的進度。

    | HDInsight 版本 | 命令 |
    |-------------------|---------|
    |HDInsight 3.3 和 HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. 上述的 hello 片段預期 hello Maven 中央儲存機制中的外部封裝 hello maven 座標。 在此程式碼片段，`com.databricks:spark-csv_2.10:1.4.0`是 hello maven 座標**spark csv**封裝。 以下是您如何建立封裝的 hello 座標。
   
    a. 在 hello Maven 儲存機制中，找出 hello 封裝。 針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。
   
    b. 從 hello 儲存機制，蒐集 hello 值**GroupId**， **ArtifactId**，和**版本**。 請確定您所收集的 hello 值符合您的叢集。 在此情況下，我們使用的是 Scala 2.10 和 Spark 1.4.0 封裝，但您可能 hello 適當 Scala 或 Spark 版本需要 tooselect 不同版本，在您的叢集。 您可以找出 hello Scala 版本在叢集上執行`scala.util.Properties.versionString`或 Spark 送出 hello Spark Jupyter 核心上。 您可以找出 hello Spark 版本在叢集上執行`sc.version`Jupyter 筆記本上。
   
    ![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")
   
    c. 串連 hello 三個值，並以分號 (**:**)。
   
        com.databricks:spark-csv_2.10:1.4.0

7. 執行 hello 程式碼的儲存格以 hello`%%configure`識別常數。 這會設定 hello 基礎晚總工作階段 toouse hello 您提供的封裝。 在儲存格中 hello 後續 hello 筆記本，您現在可以使用 hello 封裝，如下所示。
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. 然後，您可以執行 hello 程式碼片段，類似如下所示，tooview hello hello 資料框架的資料建立 hello 上一個步驟中。
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能

* [在 HDInsight Linux 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部 Python 套件](hdinsight-apache-spark-python-package-installation.md)
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

