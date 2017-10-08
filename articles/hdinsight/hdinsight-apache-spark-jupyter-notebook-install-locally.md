---
title: "在本機 aaaInstall Jupyter （& s) 連接 tooan Azure HDInsight Spark 叢集 |Microsoft 文件"
description: "深入了解如何在電腦上本機 tooinstall Jupyter 筆記本並將它連接 Azure HDInsight 上的 tooan Apache Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>在您的電腦上安裝 Jupyter 筆記本，並連接 tooApache HDInsight 上的 Spark

在這篇文章您了解如何以 hello tooinstall Jupyter 筆記本自訂 PySpark （適用於 Python) 並 （適用於 Scala) Spark 核心與二手的優勢，並連接 hello 筆記本 tooan HDInsight 叢集。 可以是本機電腦上的理由 tooinstall Jupyter 數，而且可以有以及一些挑戰。 如需此詳細資訊，請參閱 hello 節[為什麼我應該安裝 Jupyter 我的電腦上](#why-should-i-install-jupyter-on-my-computer)hello 本文結尾處。

您的電腦上安裝 Jupyter 與 hello Spark magic 是三個主要步驟。

* 安裝 Jupyter Notebook
* 安裝 hello PySpark 和 Spark 核心以 hello Spark 識別常數
* 設定在 HDInsight 上的 Spark magic tooaccess Spark 叢集

Hello 自訂核心和 hello Spark magic 供 Jupyter notebook 與 HDInsight 叢集相關的詳細資訊，請參閱[透過 Apache Spark Linux Jupyter 筆記本的可用的核心叢集 HDInsight 上](hdinsight-apache-spark-jupyter-notebook-kernels.md)。

## <a name="prerequisites"></a>必要條件
此處所列的 hello 必要條件不安裝 Jupyter。 這些是連接 hello Jupyter 筆記本 tooan HDInsight 叢集 hello 筆記本安裝之後。

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="install-jupyter-notebook-on-your-computer"></a>在電腦上安裝 Jupyter Notebook

您必須先安裝 Python，才能安裝 Jupyter Notebook。 Python 和 Jupyter 可用一部分 hello [Anaconda 發佈](https://www.continuum.io/downloads)。 當您安裝 Anaconda 時，會安裝某個 Python 發行版本。 Anaconda 安裝之後，您可以加入 hello Jupyter 安裝執行適當的命令。

1. 下載 hello [Anaconda installer](https://www.continuum.io/downloads)平台和 hello 執行安裝程式。 在執行 hello 安裝精靈，請務必選取 hello 選項 tooadd Anaconda tooyour PATH 變數。
2. 執行下列命令 tooinstall Jupyter hello。

        conda install jupyter

    如需有關安裝 Jupyter 的詳細資訊，請參閱[使用 Anaconda 來安裝 Jupyter](http://jupyter.readthedocs.io/en/latest/install.html) \(英文\)。

## <a name="install-hello-kernels-and-spark-magic"></a>安裝 hello 核心和 Spark 識別常數

如需有關如何在 tooinstall hello Spark magic、 hello PySpark 和 Spark 核心，請遵循 hello hello 安裝指示指示[sparkmagic 文件](https://github.com/jupyter-incubator/sparkmagic#installation)GitHub 上。 hello hello Spark magic 文件中的第一個步驟會要求您 tooinstall Spark 識別常數。 取代下列命令，視您要連接到 hello HDInsight 叢集的 hello 版本而定的 hello hello 連結中的第一個步驟。 完成之後，遵循 hello 剩餘 hello Spark magic 文件中的步驟。 如果您想 tooinstall hello 不同核心，您必須執行步驟 3 中 hello Spark magic 安裝指示 > 一節。

* 若為叢集 3.4 版，請執行 `pip install sparkmagic==0.2.3` 來安裝 sparkmagic 0.2.3

* 若為叢集 3.5 版和 3.6 版，請執行 `pip install sparkmagic==0.11.2` 來安裝 sparkmagic 0.11.2

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>設定 Spark magic tooconnect tooHDInsight Spark 叢集

本節中，您會設定安裝舊版 tooconnect tooan 的 Apache Spark 叢集，您必須已經建立 Azure HDInsight 中的 hello Spark 識別常數。

1. hello Jupyter 組態資訊通常會儲存在 hello 使用者主目錄中。 toolocate 主目錄任何作業系統平台上，遵循的型別 hello 命令。

    啟動 hello Python 殼層。 在命令視窗中，輸入 hello 下列：

        python

    在 hello Python 殼層中，輸入下列命令 toofind 出 hello 主目錄的 hello。

        import os
        print(os.path.expanduser('~'))

2. 瀏覽 toohello 主目錄，並建立一個稱為資料夾**.sparkmagic**如果不存在。
3. Hello 資料夾內建立檔案，稱為**config.json**並新增下列 JSON 片段內文中的 hello。

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. 以適當的值替代 **{USERNAME}**、**{CLUSTERDNSNAME}** 和 **{BASE64ENCODEDPASSWORD}**。 您可以使用多種公用程式在您偏好的程式設計語言或線上 toogenerate base64 編碼的密碼做為實際的密碼。

5. 設定在 hello 右活動訊號設定`config.json`。 您應該在相同層級為 hello hello 加入這些設定`kernel_python_credentials`和`kernel_scala_credentials`片段您加入稍早。 如需如何及在何處 tooadd hello 活動訊號設定範例，請參閱此[範例 config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)。

    * 若為 `sparkmagic 0.2.3` (叢集 3.4 版)，請加入︰

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * 若為 `sparkmagic 0.11.2` (叢集 3.5 版和 3.6 版)，請加入︰

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >活動訊號會傳送工作階段不會遺漏 tooensure。 當電腦進入 toosleep 或已關閉時，不會傳送 hello 活動訊號時，導致 hello 工作階段正在清除。 對於叢集 v3.4，如果您想 toodisable 這種行為，您可以設定 hello 晚總 config`livy.server.interactive.heartbeat.timeout`太`0`從 hello Ambari UI。 針對叢集 v3.5，如果您未設定上述 hello 3.5 組態 hello 工作階段會刪除。

6. 啟動 Jupyter。 使用 hello hello 命令提示字元中的下列命令。

        jupyter notebook

7. 請確認您可以連接使用 hello Jupyter 筆記本和，您可以使用可用的 hello Spark magic hello 核心 toohello 叢集。 執行下列步驟的 hello。

    a. 建立新的 Notebook。 從 hello 右上角，按一下 **新增**。 您應該會看見 hello 預設核心**Python2**和 hello 的安裝時，兩個新核心**PySpark**和**Spark**。 按一下 [PySpark] 。

    ![Jupyter Notebook 中的核心](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter Notebook 中的核心")

    b. 執行下列程式碼片段的 hello。

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    如果成功，您可以擷取 hello 輸出，則會測試連接 toohello HDInsight 叢集。

    >[!TIP]
    >如果您想 tooupdate hello 筆記本設定 tooconnect tooa 不同的叢集時，更新 hello config.json hello 組新的值，如上面的步驟 3 中所示。

## <a name="why-should-i-install-jupyter-on-my-computer"></a>為什麼我應該在我的電腦上安裝 Jupyter？
可以有許多原因，您可能想在電腦上的 tooinstall Jupyter 並且然後將它連接 tooa Spark HDInsight 上的叢集。

* 即使 Jupyter 筆記本已可用 hello Azure HDInsight Spark 叢集上，在電腦上安裝 Jupyter 提供 hello 選項 toocreate 本機您的筆記型電腦、 執行的叢集，對測試應用程式，然後上傳 hello筆記本 toohello 叢集。 tooupload hello 筆記本 toohello 叢集中，您可以上傳它們使用 hello Jupyter 筆記本執行或 hello 叢集，或將它們 hello 與 hello 叢集相關聯的儲存體帳戶中儲存 toohello /HdiNotebooks 資料夾。 如需有關筆記本 hello 叢集上的儲存方式的詳細資訊，請參閱[Jupyter 筆記本儲存](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)？
* 在本機，hello 筆記本提供您可以連接 toodifferent Spark 叢集，根據您應用程式的需求。
* 您可以使用 GitHub tooimplement 原始檔控制系統，並且有 hello 筆記本的版本控制。 您也可以共同作業環境，其中多個使用者可使用 hello 相同筆記型電腦。
* 您甚至不需要啟用叢集，即可在本機使用 Notebook。 您只需要叢集 tootest 針對您筆記本，不 toomanually 管理您的筆記型電腦或開發環境。
* 它可能會更容易 tooconfigure 本機開發環境比 tooconfigure hello Jupyter 安裝 hello 叢集上的。  您可以利用本機安裝但未設定一或多個遠端叢集的所有 hello 軟體。

> [!WARNING]
> 多個使用者可以使用 Jupyter 安裝在本機電腦上，執行 hello 相同筆記型電腦上相同的 Spark 叢集在 hello hello 相同的時間。 在這種情況下，會建立多個 Livy 工作階段。 如果您遇到問題，而且想 toodebug，它將會是複雜的工作 tootrack 晚總工作階段所屬 toowhich 使用者。
>
>

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
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
