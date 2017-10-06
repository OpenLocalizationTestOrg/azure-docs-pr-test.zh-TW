---
title: "在 Azure HDInsight 叢集上的 Spark Jupyter 筆記本 aaaKernels |Microsoft 文件"
description: "深入了解適用於 Azure HDInsight 上的 Spark 叢集 Jupyter 筆記本的 hello PySpark、 PySpark3 和 Spark 核心。"
keywords: "spark 上的 jupyter notebook, jupyter spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Azure HDInsight 中 Spark 叢集上的 Jupyter Notebook 核心 

HDInsight Spark 叢集提供可用於與 hello Jupyter 筆記本 Spark 上測試您的應用程式的核心。 核心是一個可執行並解譯程式碼的程式。 hello 三個核心︰

- **PySpark** - 適用於以 Python2 撰寫的應用程式
- **PySpark3** - 適用於以 Python3 撰寫的應用程式
- **Spark** - 適用於以 Scala 撰寫的應用程式

在本文中，您將學習如何 toouse 這些核心和使用它們的 hello 優點。

## <a name="prerequisites"></a>必要條件

* HDInsight 中的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>在 Spark HDInsight 上建立 Jupyter Notebook

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，開啟您的叢集。  請參閱[清單和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)hello 的指示。 hello 叢集的新入口網站的刀鋒視窗中開啟。

2. 從 hello**快速連結**區段中，按一下**叢集儀表板**tooopen hello**叢集儀表板**刀鋒視窗。  如果您沒有看到**快速連結**，按一下 [**概觀**hello hello] 刀鋒視窗的左側功能表中。

    ![Spark 上的 Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Spark 上的 Jupyter Notebook") 

3. 按一下 [Jupyter Notebook]。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。
   
   > [!NOTE]
   > 您也可能會達到 hello Jupyter 筆記本，由下列 URL 在瀏覽器中開啟 hello 的 Spark 叢集上。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. 按一下**新增**，然後按一下 **Pyspark**， **PySpark3**，或**Spark** toocreate 筆記本。 使用 Scala 應用程式的 hello Spark 核心、 PySpark 核心 Python2 應用程式和 PySpark3 核心 Python3 應用程式。
   
    ![Spark 上的 Jupyter Notebook 核心](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Spark 上的 Jupyter Notebook 核心") 

4. 筆記本會開啟與您選取的 hello 核心。

## <a name="benefits-of-using-hello-kernels"></a>使用 hello 核心的優點

以下是使用 hello 新核心 Jupyter 筆記本 Spark HDInsight 叢集上的一些優點。

- **預設內容**。 與**PySpark**， **PySpark3**，或使用 hello **Spark**核心，您不需要 tooset hello Spark 或登錄區內容明確之前您開始使用您的應用程式。 這些依預設都可用。 這些內容包括：
   
   * **sc** - 代表 Spark 內容
   * **sqlContext** - 代表 Hive 內容

    因此，您不需要像 hello 遵循 tooset hello 內容 toorun 陳述式：

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    相反地，您可以直接使用 hello 預設應用程式中的內容。

- **Cell magic**。 hello PySpark 核心提供一些預先定義 「 我們"，這是特殊的命令，您可以呼叫與`%%`(例如， `%%MAGIC` <args>)。 hello magic 命令必須在程式碼的儲存格的 hello 第一個字以及允許多行的內容。 hello 非常重要，應該 hello hello 資料格中的第一個字。 將加入 hello magic，甚至是註解之前, 的任何項目會導致錯誤。     如需 magic 的詳細資訊，請參閱 [這裡](http://ipython.readthedocs.org/en/stable/interactive/magics.html)。
   
    hello 下表列出可透過 hello 核心 hello 不同我們。

   | Magic | 範例 | 說明 |
   | --- | --- | --- |
   | help |`%%help` |會產生所有 hello 可用我們使用範例和描述的資料表 |
   | info |`%%info` |Hello 目前晚總端點的輸出工作階段資訊 |
   | 設定 |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |設定 hello 參數建立工作階段。 hello force 旗標 (-f) 是強制性，如果已建立工作階段，以確保該 hello 工作階段卸除並重新建立。 如需有效參數的清單，請查看 [Livy 的 POST /sessions 要求本文](https://github.com/cloudera/livy#request-body) 。 參數必須為 JSON 字串中傳遞且必須在 hello 下一行之後 hello magic hello 範例資料行中所示。 |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |執行 Hive 查詢針對 hello sqlContext。 如果 hello`-o`參數傳遞，hello hello 查詢結果會持續保留在 hello %%做為本機的 Python 內容[熊](http://pandas.pydata.org/)資料框架。 |
   | local |`%%local`<br>`a=1` |接下來幾行中的所有 hello 程式碼以本機方式都執行。 程式碼必須是有效的 Python2 程式碼，即使不論您使用的 hello 核心。 因此，即使您選取**PySpark3**或**Spark**時建立 hello 筆記本中，如果您使用 hello 核心`%%local`magic 儲存格，該資料格必須只有有效 Python2 程式碼... |
   | logs |`%%logs` |輸出 hello hello 目前晚總工作階段記錄檔。 |
   | delete |`%%delete -f -s <session number>` |刪除特定的工作階段的 hello 目前晚總端點。 請注意，您無法刪除 hello 工作階段起始 hello 核心本身。 |
   | cleanup |`%%cleanup -f` |刪除 hello 目前晚總端點使用，包括此筆記本工作階段的所有 hello 工作階段。 hello force 旗標-f 是必要的。 |

   > [!NOTE]
   > 此外 toohello 我們加入 hello PySpark 核心，您也可以使用 hello[內建的 IPython 魔法](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics)，包括`%%sh`。 您可以使用 hello `%%sh` magic toorun 指令碼和 hello 叢集前端節點上的程式碼區塊。
   >
   >
2. **自動視覺化**。 hello **Pyspark**核心自動視覺化 hello 的 Hive 和 SQL 查詢的輸出。 有數種不同類型的視覺效果供您選擇，包括資料表、圓形圖、線條、區域、長條圖。

## <a name="parameters-supported-with-hello-sql-magic"></a>支援以 hello 參數 %%sql 識別常數
hello `%%sql` magic 支援不同的參數，您可以使用 toocontrol hello 種執行查詢時，您收到的輸出。 hello 下表列出 hello 輸出。

| 參數 | 範例 | 說明 |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |在 hello 中使用此參數 toopersist hello 查詢的結果 hello，%%本機 Python 內容，做為[熊](http://pandas.pydata.org/)資料框架。 hello hello 資料框架變數名稱是您指定的 hello 變數名稱。 |
| -q |`-q` |使用這個視覺效果關閉 tooturn hello 儲存格。 如果您不想 tooauto-視覺化 hello 儲存格內容，且只想 toocapture 其成為資料框架，然後使用`-q -o <VARIABLE>`。 如果您想 tooturn 關閉視覺效果，而不擷取 hello 結果 (例如，針對執行 SQL 查詢，例如`CREATE TABLE`陳述式)，使用`-q`但未指定`-o`引數。 |
| -m |`-m <METHOD>` |其中 **METHOD** 是 **take** 或 **sample** (預設值是 **take**)。 如果 hello 方法**採取**，hello 核心挑選 hello MAXROWS （稍後在此資料表中所述） 所指定的結果資料集的 hello 頂端的項目。 如果 hello 方法**範例**，hello 核心會隨機取樣，根據太 hello 資料集的項目`-r`參數，此資料表中的一節所說明。 |
| -r |`-r <FRACTION>` |這裡的 **FRACTION** 是介於 0.0 到 1.0 之間的浮點數。 如果 hello SQL 查詢的 hello 範例方法`sample`，然後 hello 核心會隨機取樣 hello 指定的部分設定為您的 hello 結果的 hello 項目。 例如，如果您以 hello 引數執行 SQL 查詢`-m sample -r 0.01`，則會隨機取樣的 hello 結果資料列的 1%。 |
| -n |`-n <MAXROWS>` |**MAXROWS** 是整數值。 hello 核心限制 hello 輸出資料列數目太**MAXROWS**。 如果**MAXROWS**是負數，例如**-1**，hello hello 結果集中的資料列數目沒有限制。 |

**範例：**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

hello 上面的陳述式沒有 hello 遵循：

* 從 **hivesampletable**選取所有記錄。
* 因為我們使用 -q，所以它會關閉自動視覺效果。
* 因為我們使用`-m sample -r 0.1 -n 500`其隨機取樣的 10%的 hello hello hivesampletable 中的資料列，並限制 hello hello 結果集 too500 資料列的大小。
* 最後，因為我們使用`-o query2`它也會將 hello 輸出儲存至呼叫的資料框架**query2**。

## <a name="considerations-while-using-hello-new-kernels"></a>使用 hello 新核心時的考量

您使用，無論核心離開 hello 筆記本執行會耗用 hello 叢集資源。  這些核心，都有預設 hello 內容，因為只要結束 hello 筆記本並不會終止 hello 內容，因此 hello 叢集資源會繼續 toobe 使用中。 最好的作法是 toouse hello**關閉而停止**選項從 hello 筆記本**檔案**使用 hello 筆記本，會清除 hello 內容完畢後再結束 hello 筆記本功能表。     

## <a name="show-me-some-examples"></a>請舉例說明

當您開啟 Jupyter 筆記本時，您會看到兩個資料夾可用 hello 根層級。

* hello **PySpark**資料夾有範例筆記本該使用 hello new **Python**核心。
* hello **Scala**資料夾有範例筆記本該使用 hello new **Spark**核心。

您可以開啟 hello **00-[讀取我第一次] 的 Spark Magic 核心功能**hello 的筆記本**PySpark**或**Spark**資料夾 toolearn 有關 hello 不同魔法可用。 您也可以使用如何 hello hello 兩個資料夾 toolearn 底下可用的其他範例筆記本 tooachieve Jupyter 筆記本使用 HDInsight Spark 叢集不同的案例。

## <a name="where-are-hello-notebooks-stored"></a>Hello 筆記本儲存在哪裡？

Jupyter 筆記本會儲存 toohello 下 hello 的 hello 叢集相關聯的儲存體帳戶**/HdiNotebooks**資料夾。  筆記本、 文字檔案，與您建立從 Jupyter 內的資料夾是可從 hello 儲存體帳戶存取。  例如，如果您使用 Jupyter toocreate 資料夾**myfolder**和筆記型電腦**myfolder/mynotebook.ipynb**，您可以存取位於該筆記本`/HdiNotebooks/myfolder/mynotebook.ipynb`hello 儲存體帳戶內。  hello 反向也是如此，也就是說，如果您上傳筆記本直接 tooyour 儲存體帳戶在`/HdiNotebooks/mynotebook1.ipynb`，也是可見的 Jupyter 筆記本 hello。  即使在刪除 hello 叢集之後，才，筆記本會保留在 hello 儲存體帳戶。

筆記本會儲存 toohello 儲存體帳戶的 hello 方法是與 HDFS 相容。 因此，如果您到 hello 叢集中，您可以使用 SSH 檔案管理命令 hello 下列程式碼片段所示：

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


萬一有存取 hello hello 叢集的儲存體帳戶的問題，請 hello 筆記本也會儲存在 hello 叢集前端節點上`/var/lib/jupyter`。

## <a name="supported-browser"></a>支援的瀏覽器

Google Chrome 上只支援 Spark HDInsight 叢集上的 Jupyter Notebook。

## <a name="feedback"></a>意見反應
hello 新核心中發展階段，並將成人經過一段時間。 這或許也意味著，API 可能會隨著這些核心的成熟而改變。 您在使用這些新核心時如有任何意見，我們都非常樂於知道。 這是在發展這些核心 hello 最後發行版本中很有用。 您可以讓您的註解/的意見反應在 hello**註解**在 hello 這篇文章底部的區段。

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
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
