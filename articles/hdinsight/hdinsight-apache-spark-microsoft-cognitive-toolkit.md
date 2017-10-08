---
title: "深入了解 aaaMicrosoft 認知的工具組使用 Azure HDInsight Spark |Microsoft 文件"
description: "了解如何定型 Microsoft 認知 Toolkit 深入學習模型可以是使用 Azure HDInsight Spark 叢集中的 hello Spark Python 應用程式開發介面的 tooa 套用資料集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>使用 Microsoft 辨識工具組深入了解模型與 Azure HDInsight Spark 叢集

在本文中，您下列步驟 hello。

1. Azure HDInsight Spark 叢集上執行自訂指令碼 tooinstall Microsoft 認知工具組。

2. 如何上傳 Jupyter 筆記本 toohello Spark 叢集 toosee tooapply 定型 Microsoft 認知 Toolkit 深入了解使用 hello Azure Blob 儲存體帳戶中的模型 toofiles [Spark Python 應用程式開發介面 (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。 請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。

* **Azure HDInsight Spark 叢集**。 針對本文，建立 Spark 2.0 叢集。 如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="how-does-this-solution-flow"></a>此解決方案的流程為何？

此解決方案可分為本文章與您上傳作為本教學課程一部分的 Jupyter Notebook。 在本文中，您將完成 hello 下列步驟：

* HDInsight Spark 叢集上 tooinstall Microsoft 認知工具組，並將 Python 封裝執行的指令碼動作。
* 上傳 hello Jupyter 筆記本執行 hello 方案 toohello HDInsight Spark 叢集。

hello 下列其餘涵蓋了步驟 hello Jupyter 筆記本中。

- 將範例映像載入 Spark 復原分散式資料集或 RDD
   - 載入模組並定義預設值
   - 下載 hello hello Spark 叢集，在本機的資料集
   - 轉換 RDD hello 資料集
- 使用定型的認知 Toolkit 模型的分數 hello 映像
   - 下載 hello 定型認知 Toolkit 模型 toohello Spark 叢集
   - 定義背景工作節點使用的函式 toobe
   - 在背景工作角色節點的分數 hello 映像
   - 評估模型的精確度


## <a name="install-microsoft-cognitive-toolkit"></a>安裝 Microsoft 辨識工具組

您可以使用指令碼動作在 Spark 叢集上安裝 Microsoft 辨識工具組。 指令碼動作會在無法使用預設的 hello 叢集上使用自訂指令碼 tooinstall 元件。 使用 HDInsight.NET SDK，或使用 Azure PowerShell，您可以使用 hello hello Azure 入口網站中，從自訂指令碼。 您也可以為叢集建立或 hello 叢集已啟動並執行後的一部分使用 hello 指令碼 tooinstall hello 工具組。 

在本文中，我們會使用 hello 入口 tooinstall hello 工具組，建立 hello 叢集之後。 針對其他方式 toorun hello 自訂指令碼，請參閱[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)。

### <a name="using-hello-azure-portal"></a>使用 hello Azure 入口網站

如需有關如何 toouse hello Azure 入口網站 toorun 指令碼動作的指示，請參閱[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)。 請確定您提供下列輸入 tooinstall Microsoft 認知 Toolkit hello。

* 提供 hello 指令碼動作名稱的值。

* 對於 **Bash 指令碼 URI**，輸入 `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`。

* 請確定您執行 hello 指令碼只在 hello head 和背景工作節點並清除所有 hello 其他核取方塊。

* 按一下 [建立] 。

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>上傳 hello Jupyter 筆記本 tooAzure HDInsight Spark 叢集

toouse hello Microsoft 認知 Toolkit 與 hello Azure HDInsight Spark 叢集，您必須先載入 hello Jupyter 筆記本**CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark 叢集。 這個 Notebook 可在 GitHub 上取得，網址是：[https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。

1. 複製 hello GitHub 儲存機制[https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。 指示 tooclone，請參閱[複製的儲存機制](https://help.github.com/articles/cloning-a-repository/)。

2. 從 hello Azure 入口網站，開啟 已佈建，按一下的 hello Spark 叢集分頁**叢集儀表板**，然後按一下 **Jupyter 筆記本**。

    您也可以藉由選取 toohello URL 啟動 hello Jupyter 筆記本`https://<clustername>.azurehdinsight.net/jupyter/`。 取代\<clustername > hello 名稱，為您的 HDInsight 叢集。

3. 從 hello Jupyter 筆記本中，按一下 **上傳**在 hello 右上角，然後瀏覽您再製 hello GitHub 儲存機制的 toohello 位置。

    ![上傳 Jupyter 筆記本 tooAzure HDInsight Spark 叢集](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "上傳 Jupyter 筆記本 tooAzure HDInsight Spark 叢集")

4. 再次按一下 [上傳]。

5. Hello 筆記本已上傳之後，按一下 hello 筆記本的 hello 名稱，並遵照 tooload hello 資料集和執行 hello 教學課程的方式上本身 hello 筆記本中的 hello 指示。

## <a name="see-also"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight 中使用 Spark 的 Application Insight 遙測資料分析](hdinsight-spark-analyze-application-insight-logs.md)

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

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
