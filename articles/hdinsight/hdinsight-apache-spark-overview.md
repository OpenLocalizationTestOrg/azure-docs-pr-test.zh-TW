---
title: "Azure HDInsight 上的 aaaIntroduction tooSpark |Microsoft 文件"
description: "本文章提供簡介 tooSpark，您可以在此使用 HDInsight 上的 Spark 叢集的 HDInsight 和 hello 不同的案例。"
keywords: "什麼是 apache spark，spark 叢集，簡介 toospark hdinsight 上的 spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>HDInsight 上的簡介 tooSpark

這篇文章提供您在 HDInsight 上簡介 tooSpark。 <a href="http://spark.apache.org/" target="_blank">Apache Spark</a>開放原始碼的平行處理架構，可支援記憶體中處理 tooboost hello 巨量資料分析的應用程式效能。 HDInsight 上的 Spark 叢集也能與 Azure 儲存體 (WASB) 以及 Azure Data Lake Store 相容，因此您可以輕鬆地透過 Spark 叢集處理儲存在 Azure 中的現有資料。

當您在 HDInsight 上建立 Spark 叢集時，就是建立了已安裝及設定 Spark 的 Azure 計算資源。 只需要約 toocreate Spark 叢集 HDInsight 中的十分鐘。 處理 hello 資料 toobe 會儲存在 Azure 儲存體或 Azure 資料湖存放區。 請參閱[搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。

**在 HDInsight 叢集化 toocreate Spark**，請參閱[快速入門： 建立 HDInsight 上的 Spark 叢集，並執行互動式查詢使用 Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md)。


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>什麼是 Apache Spark on Azure HDInsight？
HDInsight 上的 Spark 叢集可提供完全受管理的 Spark 服務。 在 HDInsight 上建立 Spark 叢集的優點如下所列。

| 功能 | 說明 |
| --- | --- |
| 容易建立 Spark 叢集 |以分鐘為單位使用 hello Azure 入口網站、 Azure PowerShell 或 hello HDInsight.NET SDK，您可以在 HDInsight 上建立新的 Spark 叢集。 請參閱 [開始使用 HDInsight 中的 Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md) |
| 容易使用 |HDInsight 上的 Spark 叢集包含 Jupyter 和 Zeppelin Notebook。 您可以使用它們來進行互動式的資料處理和視覺化。|
| REST API |在 HDInsight Spark 叢集包含[晚總](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)，REST API 為基礎的 Spark 作業伺服器 tooremotely 提交和監視工作。 |
| 支援 Azure Data Lake Store | HDInsight 上的 Spark 叢集，可以設定的 toouse Azure Data Lake Store 的其他存放裝置，以及主要儲存體 （僅限與 HDInsight 3.5 叢集）。 如需有關 Data Lake Store 的詳細資訊，請參閱 [Azure Data Lake Store 概觀](../data-lake-store/data-lake-store-overview.md)。 |
| Azure 服務整合 |HDInsight 上的 Spark 叢集隨附連接器 tooAzure 事件中心。 客戶可以建置串流應用程式使用 hello 事件中樞，此外太[Kafka](http://kafka.apache.org/)，既有的 Spark 一部分。 |
| 支援 R 伺服器 | 您可以設定 R 伺服器 HDInsight Spark 叢集 toorun 分散式 R 計算具有 hello 速度承諾的 Spark 叢集上。 如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。 |
| 第三方 IDE 整合 | HDInsight 提供 Ide IntelliJ 概念和 Eclipse，您可以使用 toocreate 並送出應用程式 tooan HDInsight Spark 叢集等外掛程式。 如需詳細資訊，請參閱[使用 Azure Toolkit for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md)和[使用 Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)。|
| 並行查詢 |HDInsight 中的 Spark 叢集支援並行查詢。 這可讓多個查詢從一位使用者或多個查詢從不同的使用者和應用程式 tooshare hello 相同的叢集資源。 |
| SSD 快取 |您可以任選其一 toocache 資料在記憶體中或在 Ssd 附加 toohello 叢集節點。 在記憶體中快取提供 hello 最佳查詢效能，但可能很昂貴。快取中的 Ssd 會提供改善查詢效能不 hello 需要 toocreate 必要的 toofit hello 整個資料集在記憶體中大小的叢集中的一個絕佳的選項。 |
| BI 工具整合 |HDInsight 上的 Spark 叢集會為 BI 工具 (例如 [Power BI](http://www.powerbi.com/) 和 [Tableau](http://www.tableau.com/products/desktop)) 提供資料分析所需的連接器。 |
| 預先載入的 Anaconda 程式庫 |HDInsight 上的 Spark 叢集附有預先安裝的 Anaconda 程式庫。 [Anaconda](http://docs.continuum.io/anaconda/)關閉 too200 程式庫提供機器學習服務、 資料分析、 視覺效果等等。 |
| 延展性 |雖然您可以指定叢集中的節點數目 hello 建立期間，您可能想 toogrow 或壓縮 hello 叢集 toomatch 工作負載。 所有的 HDInsight 叢集可讓您的節點 toochange hello 數目 hello 叢集中。 此外，Spark 叢集可以卸除，且不會遺失資料的因為所有的 hello 資料會儲存在 Azure 儲存體或資料湖存放區。 |
| 全天候支援 |HDInsight 上的 Spark 叢集附有企業級的全天候支援和保證正常運作時間達 99.9% 的 SLA。 |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>HDInsight 上的 Spark hello 的使用案例有哪些？
在 HDInsight Spark 叢集啟用 hello 下列重要案例。

### <a name="interactive-data-analysis-and-bi"></a>互動式資料分析和 BI
[觀看教學課程](hdinsight-apache-spark-use-bi-tools.md)

HDInsight 中的 Apache Spark 會將資料儲存在 Azure 儲存體或 Azure Data Lake Store 中。 商務專家和金鑰決策者可以分析及透過該資料建立報表和使用 Microsoft Power BI toobuild 互動式報表從 hello 分析資料。 分析師可以開始從叢集存放區中的非結構化/半結構化資料定義使用筆記型電腦，hello 資料的結構描述，然後建立使用 Microsoft Power BI 的資料模型。 HDInsight 中的 Spark 叢集也支援 Tableau 等多個第三方 BI 工具，因此能成為資料分析師、商務專家及重要決策者的理想平台。

### <a name="spark-machine-learning"></a>Spark 機器學習服務
[看看教學課程：利用 HVAC 資料來預測建築物的溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[看看教學課程：預測食物檢查結果](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark 隨附 [MLlib](http://spark.apache.org/mllib/)，這是以 Spark 為基礎的機器學習程式庫，您可以從 HDInsight 中的 Spark 叢集使用。 HDInsight 上的 Spark 叢集也包含 Anaconda，這是提供各種機器學習套件的 Python 散發。 搭配內建的 Jupyter 和 Zeppelin Notebook 支援，您將擁有最先進的機器學習應用程式建立環境。

### <a name="spark-streaming-and-real-time-data-analysis"></a>Spark 串流和即時資料分析
[觀看教學課程](hdinsight-apache-spark-eventhub-streaming.md)

HDInsight 上的 Spark 叢集提供豐富的支援供您建置即時分析解決方案。 雖然 Spark 已有連接器 tooingest 資料，從許多來源，例如 Kafka、 Flume、 Twitter、 ZeroMQ 或 TCP 通訊端，在 HDInsight Spark 會加入第一級支援擷取資料從 Azure 事件中樞。 事件中心是在 Azure 上 hello 最常使用的佇列服務。 擁有立即可用的事件中樞支援，讓 HDInsight 中的 Spark 叢集成為建置即時分析管線的理想平台。

## <a name="next-steps"></a>Spark 叢集包含哪些元件？
在 HDInsight Spark 叢集包含下列元件所提供的預設 hello 叢集 hello。

* [Spark Core](https://spark.apache.org/docs/1.5.1/)。 包括 Spark Core、Spark SQL、Spark 串流 API、GraphX 及 MLlib。
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter Notebook](https://jupyter.org)
* [Zeppelin Notebook](http://zeppelin-project.org/)

HDInsight 上的 Spark 叢集也提供[ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229)HDInsight 中的 BI 工具，例如 Microsoft Power BI 和 Tableau 的連線能力 tooSpark 叢集。

## <a name="where-do-i-start"></a>我該從哪裡開始？
請從在 HDInsight 上建立 Spark 叢集開始。 請參閱[快速入門：在 HDInsight Linux 上建立 Spark 叢集並利用 Jupyter 執行互動式查詢](hdinsight-apache-spark-jupyter-spark-sql.md)。 

## <a name="next-steps"></a>後續步驟
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
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
* [Azure HDInsight 中 Apache Spark 的已知問題](hdinsight-apache-spark-known-issues.md)。
