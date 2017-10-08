---
title: "Azure HDInsight 上執行作業的 aaaDebug Apache Spark |Microsoft 文件"
description: "使用 YARN UI、 Spark UI 和 Spark 記錄伺服器 tootrack 和偵錯工作在 Azure HDInsight Spark 叢集上執行"
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯

在本文中，您將學習如何 tootrack 和偵錯二手使用 hello YARN UI Spark UI 的 HDInsight 叢集上執行的作業以及 hello Spark 歷程記錄的伺服器。 這個發行項，我們將會啟動 Spark 工作 hello Spark 叢集後，使用可用的筆記本**機器學習： 針對使用 MLLib 食物檢查資料的預測分析**。 您可以使用下列 tootrack 您送出使用任何其他方法，例如，應用程式的 hello 步驟**spark-submit 對**。

## <a name="prerequisites"></a>必要條件
您必須擁有 hello 下列：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
* 您應該開始執行 hello 筆記本**[機器學習： 針對使用 MLLib 食物檢查資料的預測分析](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**。 如需有關指示 toorun 筆記本，後續 hello 連結。  

## <a name="track-an-application-in-hello-yarn-ui"></a>追蹤 hello YARN UI 中的應用程式
1. 啟動 hello YARN UI。 從 hello 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **YARN**。
   
    ![啟動 YARN UI](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > 或者，您也可以啟動 hello YARN UI 從 hello Ambari UI。 按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。 從 hello Ambari UI 中，按一下  **YARN**，按一下 **快速連結**hello 作用中的資源管理員，然後按**ResourceManager UI**。    
   > 
   > 
2. Hello 應用程式，您一開始使用 Jupyter 筆記本 hello Spark 作業，因為已 hello 名稱**remotesparkmagics** （這是 hello hello 筆記本從啟動的所有應用程式的名稱）。 按一下 針對 hello 應用程式名稱 tooget hello 應用程式識別碼 hello 工作的詳細資訊。 這會啟動 hello 應用程式檢視。
   
    ![尋找 Spark 應用程式識別碼](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    從 hello Jupyter 筆記本啟動這類應用程式，對於 hello 狀態一律是**執行**等到您結束 hello 筆記型電腦。
3. 從 hello 應用程式檢視中，您可以向下鑽研進一步 toofind 出 hello 與 hello 應用程式和 hello 記錄檔 (stdout/stderr) 相關聯的容器。 您也可以按一下連結對應 toohello hello 啟動 hello Spark UI**追蹤 URL**，如下所示。 
   
    ![下載容器記錄檔](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>追蹤 hello Spark UI 中的應用程式
在 hello Spark UI，您可以向下鑽研由您先前已啟動的 hello 應用程式產生的 hello Spark 作業。

1. toolaunch hello Spark UI hello 應用程式檢視中，按一下 針對 hello hello 連結**追蹤 URL**hello 螢幕擷取畫面上方所示。 您可以查看所有 hello hello Jupyter 筆記本中執行的應用程式所啟動的 hello Spark 工作。
   
    ![檢視 Spark 作業](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. 按一下 hello**執行程式**索引標籤上的每一個執行程式的 toosee 處理和儲存體資訊。 您也可以擷取 hello 呼叫堆疊上 hello 即可**執行緒傾印**連結。
   
    ![檢視 Spark 執行程式](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. 按一下 hello**階段**hello 應用程式相關聯的 toosee hello 階段索引標籤上。
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    每個階段可以有多個工作，您可以檢視其執行統計資料，如下所示。
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Hello 階段詳細資料頁面中，您可以啟動 DAG 視覺效果。 展開 hello **DAG 視覺效果**連結 hello 頁面頂端的 hello，如下所示。
   
    ![檢視 Spark 階段 DAG 視覺效果](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG 或直接 Aclyic 圖形代表 hello hello 應用程式中的不同階段。 Hello 圖形中每一個藍色方塊表示從 hello 應用程式叫用的 Spark 作業。
5. Hello 階段詳細資料頁面中，您也可以啟動 hello 應用程式時間軸檢視。 展開 hello**事件時間軸**連結 hello 頁面頂端的 hello，如下所示。
   
    ![檢視 Spark 階段事件時間軸](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    這在 hello 以時刻表的形式顯示 hello Spark 事件。 hello 時間表檢視可在三個層級，在工作階段內和作業範圍內。 上述的 hello 映像擷取特定階段 hello 時間表檢視。
   
   > [!TIP]
   > 如果您選取 hello**啟用縮放**核取方塊，您可以左右橫向捲動 hello 時間表檢視。
   > 
   > 
6. Hello Spark UI 中的其他索引標籤會提供實用資訊以及 hello Spark 執行個體。
   
   * 儲存體索引標籤-如果您的應用程式建立 RDDs，您可以找到 hello 儲存體索引標籤中的相關資訊。
   * 環境索引標籤-此索引標籤提供了許多有用的資訊關於您的 Spark 執行個體，例如 hello 
     * Scala 版本
     * 與 hello 叢集相關聯的事件記錄檔目錄
     * Hello 應用程式的執行程式核心數目
     * 等等

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>尋找使用 hello Spark 記錄伺服器已完成工作的相關資訊
完成工作之後，hello hello 工作的資訊會保存在 hello Spark 歷程記錄的伺服器。

1. toolaunch hello Spark 記錄伺服器上，從 hello 叢集刀鋒視窗中，按一下**叢集儀表板**，然後按一下 **Spark 記錄伺服器**。
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > 或者，您也可以啟動 hello Spark 記錄 Server UI 從 hello Ambari UI。 按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。 從 hello Ambari UI 中，按一下  **Spark**，按一下 **快速連結**，然後按一下 **Spark 記錄 Server UI**。
   > 
   > 
2. 您會看到所有列出的 hello 完成應用程式。 如需詳細資訊的應用程式，向下一直按應用程式識別碼 toodrill。
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>另請參閱
*  [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>針對資料分析師

* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight 中使用 Spark 的 Application Insight 遙測資料分析](hdinsight-spark-analyze-application-insight-logs.md)
* [在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>針對 Spark 開發人員

* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


