---
title: "對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯 | Microsoft Docs"
description: "使用 YARN UI、Spark UI 和 Spark 歷程記錄伺服器，追蹤和偵錯在 Azure HDInsight 中的 Spark 叢集上執行的作業"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯

在本文中，您將學習如何使用 YARN UI、Spark UI 和 Spark 歷程記錄伺服器，對 HDInsight 叢集上執行的 Spark 作業進行追蹤和偵錯。 在本文中，我們會使用 Spark 叢集中可用的 Notebook 啟動 Spark 作業， **機器學習服務︰使用 MLLib 對食物檢查資料進行預測分析**。 您可以使用下列步驟來追蹤您使用任何其他方法提交的應用程式，例如， **spark-submit**。

## <a name="prerequisites"></a>必要條件
您必須滿足以下條件：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
* 您應該開始執行 Notebook， **[機器學習服務︰使用 MLLib 對食物檢查資料進行預測分析](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**。 如需有關如何執行此 Notebook 的指示，請依照下列連結。  

## <a name="track-an-application-in-the-yarn-ui"></a>追蹤 YARN UI 中的應用程式
1. 啟動 YARN UI。 從叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [YARN]。
   
    ![啟動 YARN UI](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > 或者，您也可以從 Ambari UI 啟動 YARN UI。 若要啟動 Ambari UI，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [HDInsight 叢集儀表板]。 從 Ambari UI 中，依序按一下 [YARN]、[快速連結]、作用中的資源管理員，以及 [ResourceManager UI]。    
   > 
   > 
2. 因為您使用 Jupyter Notebook 啟動 Spark 作業，應用程式具有名稱 **remotesparkmagics** (這是從 Notebook 啟動之所有應用程式的名稱)。 針對應用程式名稱按一下應用程式識別碼，取得作業的詳細資訊。 這會啟動應用程式檢視。
   
    ![尋找 Spark 應用程式識別碼](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    對於從 Jupyter Notebook 啟動的應用程式，狀態一律是 [執行中]  ，直到您結束 Notebook。
3. 從應用程式檢視中，您可以進一步向下鑽研以找出與應用程式和記錄檔 (stdout/stderr) 相關聯的容器。 您也可以藉由按一下對應至 [追蹤 URL] 的連結，即可啟動 Spark UI，如下所示。 
   
    ![下載容器記錄檔](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a>追蹤 Spark UI 中的應用程式
在 Spark UI 中，您可以向下鑽研至您先前啟動的應用程式所繁衍的 Spark 作業。

1. 若要啟動 Spark UI，請從應用程式檢視中，針對 [追蹤 URL] 按一下連結，如上面的螢幕擷取畫面所示。 您可以看到應用程式啟動的所有 Spark 作業在 Jupyter Notebook 中執行。
   
    ![檢視 Spark 作業](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. 按一下 [執行程式]  索引標籤，查看每個執行程式的處理和儲存資訊。 您也可以按一下 [執行緒傾印]  連結，擷取呼叫堆疊。
   
    ![檢視 Spark 執行程式](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. 按一下 [階段]  索引標籤，查看與應用程式相關聯的階段。
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    每個階段可以有多個工作，您可以檢視其執行統計資料，如下所示。
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. 從階段詳細資料頁面上，您可以啟動 DAG 視覺效果。 展開頁面頂端的 [DAG 視覺效果]  連結，如下所示。
   
    ![檢視 Spark 階段 DAG 視覺效果](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG 或 Direct Aclyic Graph 代表應用程式中的不同階段。 每個圖形中的藍色方塊表示從應用程式叫用的 Spark 作業。
5. 您也可以從階段詳細資料頁面上，啟動應用程式時間軸檢視。 展開頁面頂端的 [事件時間軸]  連結，如下所示。
   
    ![檢視 Spark 階段事件時間軸](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    這會以時間軸的形式顯示 Spark 事件。 時間軸檢視有三個層級，跨作業、作業內以及階段內。 以上的映像擷取指定階段的時間軸檢視。
   
   > [!TIP]
   > 如果您選取 [啟用縮放功能] 核取方塊，您可以跨時間軸檢視左右捲動。
   > 
   > 
6. Spark UI 中的其他索引標籤也提供 Spark 執行個體的實用資訊。
   
   * [儲存體] 索引標籤 - 如果您的應用程式建立 RDD，您可以在 [儲存體] 索引標籤中找到相關資訊。
   * [環境]索引標籤 - 這個標籤提供關於您的 Spark 執行個體的實用資訊，例如 
     * Scala 版本
     * 與叢集相關聯的事件記錄檔目錄
     * 應用程式的執行程式核心數目
     * 等等

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a>使用 Spark 歷程記錄伺服器尋找已完成作業的相關資訊
完成作業後，作業的相關資訊會保存在 Spark 歷程記錄伺服器。

1. 若要啟動 Spark 歷程記錄伺服器，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [Spark 歷程記錄伺服器]。
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > 或者，您也可以從 Ambari UI 啟動 Spark 歷程記錄伺服器 UI。 若要啟動 Ambari UI，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [HDInsight 叢集儀表板]。 從 Ambari UI 中，依序按一下 [Spark]、[快速連結]和 [Spark 歷程記錄伺服器 UI]。
   > 
   > 
2. 您會看到列出所有已完成應用程式。 按一下應用程式識別碼，向下鑽研至應用程式以取得其他資訊。
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>另請參閱
*  [在 Azure HDInsight 中管理 Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>針對資料分析師

* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight 中使用 Spark 的 Application Insight 遙測資料分析](hdinsight-spark-analyze-application-insight-logs.md)
* [在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>針對 Spark 開發人員

* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)
* [使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


