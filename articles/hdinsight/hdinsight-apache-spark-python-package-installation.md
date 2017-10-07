---
title: "aaaScript 動作-安裝 Python 封裝，使用 Azure HDInsight 上 Jupyter |Microsoft 文件"
description: "上如何 toouse 指令碼動作 tooconfigure Jupyter 筆記本適用於 HDInsight Spark 叢集 toouse 外部 python 封裝的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>使用 Apache Spark 叢集，在 HDInsight 上 Jupyter 筆記本的指令碼動作 tooinstall 外部 Python 封裝
> [!div class="op_single_selector"]
> * [使用資料格魔術](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [使用指令碼動作](hdinsight-apache-spark-python-package-installation.md)
>
>

了解如何 toouse 指令碼動作 tooconfigure Apache Spark 叢集上 HDInsight (Linux) toouse 外部、 社群貢獻**python**不封裝在 hello 叢集中包含的方塊外。

> [!NOTE]
> 您也可以藉由設定 Jupyter 筆記本`%%configure`magic toouse 外部的封裝。 如需指示，請參閱[在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)。
> 
> 

您可以搜尋 hello[封裝索引](https://pypi.python.org/pypi)如 hello 的封裝所提供的完整清單。 您也可以從其他來源取得可用套件清單。 例如，您可以安裝經由 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 或 [conda-forge](https://conda-forge.github.io/feedstocks.html) 提供的套件。

在本文中，您將學習如何 tooinstall hello [TensorFlow](https://www.tensorflow.org/)封裝您的叢集上使用指令碼 Actoin 並使用透過 hello Jupyter 筆記本。

## <a name="prerequisites"></a>必要條件
您必須擁有 hello 下列：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

   > [!NOTE]
   > 如果您在 HDInsight Linux 上還沒有 Spark 叢集，您可以在叢集建立期間執行指令碼動作。 瀏覽 hello 文件上[toouse 自訂如何編寫指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)。
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>搭配 Jupyter Notebook 使用外部套件

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   

2. 從 hello Spark 叢集刀鋒視窗中，按一下 **指令碼動作**下**使用量**。 執行安裝 TensorFlow hello 前端節點和 hello 背景工作角色節點中的 hello 自訂動作。 您可以從參考 hello bash 指令碼： https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh 造訪 hello 文件上的[toouse 自訂如何編寫指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)。

   > [!NOTE]
   > 有兩個 python 安裝 hello 叢集中。 Spark 會使用 hello Anaconda 的 python 安裝位於`/usr/bin/anaconda/bin`。 在您的自訂動作中，透過 `/usr/bin/anaconda/bin/pip` 和 `/usr/bin/anaconda/bin/conda` 來參考該安裝。
   > 
   > 

3. 開啟 PySpark Jupyter Notebook

    ![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")

4. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。

    ![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "提供 hello 筆記本的名稱")

5. 現在，您將 `import tensorflow` 並執行 hello world 範例。 

    程式碼 toocopy:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    hello 結果看起來像這樣：
    
    ![TensorFlow 程式碼執行](./media/hdinsight-apache-spark-python-package-installation/execution.png "執行 TensorFlow 程式碼")



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
* [在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
