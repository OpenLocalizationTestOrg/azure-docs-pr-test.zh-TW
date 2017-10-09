---
title: "在 Azure HDInsight 叢集化 Apache Spark aaaManage 資源 |Microsoft 文件"
description: "了解 toouse 管理 Azure HDInsight 上的 Spark 叢集，以提升效能的資源。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>在 Azure HDInsight 上管理 Apache Spark 叢集的資源 

在本文中，您將學習 tooaccess hello 介面，例如 Ambari UI、 YARN UI 和 hello Spark 記錄伺服器與您的 Spark 叢集的相關聯。 您也將了解如何 tootune hello 叢集設定以獲得最佳效能。

**先決條件：**

您必須擁有 hello 下列：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>我要如何啟動 hello Ambari Web UI？
1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。
2. 從 hello Spark 叢集刀鋒視窗中，按一下 **儀表板**。 出現提示時，輸入 hello Spark 叢集 hello 系統管理員認證。

    ![啟動 Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "啟動 Resource Manager")
3. 這應該啟動 hello Ambari Web UI 中，如下所示。

    ![Ambari Web UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>我要如何啟動 hello Spark 記錄伺服器？
1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。
2. 從 hello 叢集刀鋒視窗中，在**快速連結**，按一下 **叢集儀表板**。 在 hello**叢集儀表板**刀鋒視窗中，按一下  **Spark 記錄伺服器**。

    ![Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark 歷程記錄伺服器")

    出現提示時，輸入 hello Spark 叢集 hello 系統管理員認證。

## <a name="how-do-i-launch-hello-yarn-ui"></a>我要如何啟動 hello Yarn UI？
您可以使用 hello YARN UI toomonitor 應用程式目前正在 hello Spark 叢集上執行。

1. 從 hello 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **YARN**。

    ![啟動 YARN UI](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > 或者，您也可以啟動 hello YARN UI 從 hello Ambari UI。 按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。 從 hello Ambari UI 中，按一下  **YARN**，按一下 **快速連結**hello 作用中的資源管理員，然後按**ResourceManager UI**。
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>什麼是 hello 最佳群集組態 toorun Spark 應用程式？
用於根據應用程式需求的 Spark 組態 hello 三個參數都是`spark.executor.instances`， `spark.executor.cores`，和`spark.executor.memory`。 執行程式是針對 Spark 應用程式啟動的程序。 它在 hello 背景工作節點上執行，而且是負責 toocarry hello hello 應用程式的工作。 執行程式和每個叢集的 hello executor 大小的 hello 預設數目是根據 hello 數目背景工作節點和 hello 背景工作節點大小計算。 這些儲存在`spark-defaults.conf`hello 叢集前端節點上。

hello 三個組態參數可以設定在 hello 叢集層級 （適用於 hello 叢集執行的所有應用程式），或每個個別應用程式也可以指定。

### <a name="change-hello-parameters-using-ambari-ui"></a>變更使用 Ambari UI hello 參數
1. 從 hello Ambari UI 按一下**Spark**，按一下**Configs**，然後展開**自訂 spark 預設**。

    ![使用 Ambari UI 設定參數](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. hello 預設值為 hello 叢集上同時執行的良好 toohave 4 Spark 應用程式。 您可以變更這些值從 hello 使用者介面，如下所示。

    ![使用 Ambari UI 設定參數](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. 按一下**儲存**toosave hello 組態變更。 在 hello hello 頁面頂端，系統會提示您所有 hello 的 toorestart 受影響的服務。 按一下 [重新啟動] 。

    ![重新啟動服務](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>變更 hello 參數 Jupyter 筆記本中執行的應用程式
Hello Jupyter 筆記本中執行的應用程式，您可以使用 hello `%%configure` magic toomake hello 組態變更。 在理想情況下，您必須進行這類變更在 hello 開頭 hello 應用程式，才能執行您的第一個程式碼儲存格。 這可確保該 hello 組態會套用的 toohello 晚總工作階段中，取得建立時。 如果您想在稍後階段 hello 應用程式中的 toochange hello 組態，您必須使用 hello`-f`參數。 不過，這麼做會所有進度 hello 中應用程式將會遺失。

hello 以下程式碼片段顯示如何 toochange hello Jupyter 中執行的應用程式的組態。

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

組態參數必須為 JSON 字串中傳遞且必須在 hello 下一行之後 hello magic hello 範例資料行中所示。

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>應用程式使用提交變更 hello 參數 spark-submit 對
下列命令是如何 toochange hello 使用提交的批次應用程式的組態參數的範例`spark-submit`。

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>使用 cURL 提交應用程式的變更 hello 參數
下列命令是如何 toochange hello 使用 cURL 提交的批次應用程式的組態參數的範例。

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>如何在 Spark Thrift 伺服器變更這些參數？
Spark Thrift 伺服器提供 JDBC/ODBC 存取 tooa Spark 叢集，而且是使用的 tooservice Spark SQL 查詢。 Power BI、Tableau 等工具 ODBC 通訊協定 toocommunicate 搭配 Spark Thrift 伺服器 tooexecute Spark SQL 查詢使用做為 Spark 應用程式。 Spark 叢集，以建立時，兩個 hello Spark Thrift 伺服器會啟動，每個前端節點上的其中一個執行個體。 每個 Spark Thrift 伺服器會顯示以 hello YARN UI 中的 Spark 應用程式。

Spark Thrift 伺服器使用二手動態執行程式配置，因此 hello`spark.executor.instances`未使用。 相反地，Spark Thrift 伺服器會使用`spark.dynamicAllocation.minExecutors`和`spark.dynamicAllocation.maxExecutors`toospecify hello 執行程式計數。 hello 組態參數`spark.executor.cores`和`spark.executor.memory`是使用 toomodify hello 執行程式的大小。 您可以變更這些參數，如下所示。

* 展開 hello**進階 spark-thrift-sparkconf**類別 tooupdate hello 參數`spark.dynamicAllocation.minExecutors`， `spark.dynamicAllocation.maxExecutors`，和`spark.executor.memory`。

    ![設定 Spark Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* 展開 hello**自訂 spark thrift sparkconf**分類 tooupdate hello 參數`spark.executor.cores`。

    ![設定 Spark Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>如何變更 hello 驅動程式記憶體的 hello Spark Thrift 伺服器？
Spark Thrift 伺服器驅動程式的記憶體是已設定的 too25 %hello 前端節點的 RAM 大小，提供 hello 前端節點的 hello 總 RAM 大小大於 14 GB。 您可以使用 hello Ambari UI toochange hello 驅動程式的記憶體組態，如下所示。

* 從 hello Ambari UI 按一下**Spark**，按一下**Configs**，依序展開**進階 spark env**，然後提供 hello 值**spark_thrift_cmd_opts**.

    ![設定 Spark Thrift 伺服器 RAM](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>我沒有搭配使用 BI 和 Spark 叢集。 如何備份佔用 hello 資源？
因為我們使用 Spark 動態配置，hello thrift 伺服器所耗用的資源是 hello hello 兩個應用程式主機的資源。 tooreclaim 這些資源，您必須先停止 hello Thrift 伺服器 hello 叢集上執行的服務。

1. 從 hello Ambari UI hello 左窗格中，按一下  **Spark**。
2. 在 hello 下一步 頁面上，按一下**Spark Thrift 伺服器**。

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. 您應該會看到 hello 兩個 headnodes 哪些 hello Spark Thrift 伺服器正在執行。 按一下其中一個 hello headnodes。

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. hello 下一個頁面會列出在該叢集前端節點上執行的所有 hello 服務。 從 hello 清單中，按一下 hello 下拉式按鈕下一步 tooSpark Thrift 伺服器，然後按一下**停止**。

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. 上重複這些步驟 hello 以及其他前端節點。

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>我的 Jupyter Notebook 並未如預期般執行。 如何重新啟動 hello 服務？
啟動 hello Ambari Web UI，如上所示。 從 hello 左側瀏覽窗格中，按一下  **Jupyter**，按一下 **服務動作**，然後按一下**重新啟動所有**。 這會啟動 hello Jupyter 服務上所有的 hello headnodes。

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>如何知道我是否用盡資源？
啟動 hello Yarn UI，如上所示。 在叢集度量資料表之上囉 」 畫面中，檢查值**記憶體使用**和**記憶體總計**資料行。 如果 hello 2 值非常接近，可能不會有足夠資源 toostart hello 下一個應用程式。 hello 同樣適用 toohello **VCores 用**和**VCores 總計**資料行。 此外，在 hello 主要檢視中，如果沒有應用程式仍會維持在**接受**狀態並不會轉換成**執行**也**失敗**狀態時，這也可能表示它沒有取得足夠的資源 toostart。

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>如何終止執行的應用程式 toofree 資源？
1. 在 hello Yarn UI 從 hello 左面板中，按一下 **執行**。 從 hello 清單中執行的應用程式，判斷 hello 應用程式 toobe 遭到刪除，然後按一下 hello**識別碼**。

    ![終止 App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "終止 App1")

2. 按一下**終止應用程式**hello 頂端的右上角，然後按一下 **確定**。

    ![終止 App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "終止 App2")

## <a name="see-also"></a>另請參閱
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

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
