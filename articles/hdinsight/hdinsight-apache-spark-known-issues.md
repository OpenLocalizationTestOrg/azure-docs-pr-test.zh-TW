---
title: "在 Azure HDInsight 叢集使用 Apache Spark aaaTroubleshoot 問題 |Microsoft 文件"
description: "了解問題相關的 tooApache Azure HDInsight Spark 叢集以及如何解決那些 toowork。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>HDInsight 上的 Apache Spark 叢集已知問題

這份文件會持續追蹤的所有 hello hello HDInsight Spark 公用預覽的已知問題。  

## <a name="livy-leaks-interactive-session"></a>Livy 會流失互動式工作階段
晚總重新啟動時 （從 Ambari 或因為 tooheadnode 0 虛擬機器重新開機） 與仍在執行的互動式工作階段，互動式工作階段會外洩。 因為這個緣故，新的工作可以陷入 hello 已接受狀態，因此無法啟動。

**緩和：**

使用下列程序 tooworkaround hello 問題 hello:

1. Ssh 到前端節點。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 執行下列命令 toofind hello 應用程式的 hello 透過晚總啟動 hello 互動式工作的識別碼。 
   
        yarn application –list
   
    hello 預設作業名稱會晚總 hello 工作已有名為沒有明確指定，如 hello 時入門晚總互動式工作階段啟動 Jupyter 筆記本晚總工作階段，hello 工作名稱的開頭將 remotesparkmagics_ *。 
3. 執行下列命令 tookill hello 這些作業。 
   
        yarn application –kill <Application ID>

新作業將會開始執行。 

## <a name="spark-history-server-not-started"></a>Spark 歷程記錄伺服器未啟動
叢集建立後，不會自動啟動 Spark 歷程記錄伺服器。  

**緩和：** 

手動從 Ambari 啟動 hello 歷程記錄的伺服器。

## <a name="permission-issue-in-spark-log-directory"></a>Spark 記錄檔目錄中的權限問題
當 hdiuser 提交 spark-submit 與作業時，就會發生錯誤 java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log （拒絕的權限） 和 hello 驅動程式記錄檔不會寫入。 

**緩和：**

1. 新增 hdiuser toohello Hadoop 群組。 
2. 在叢集建立之後，提供 /var/log/spark 的 777 權限。 
3. 更新使用 Ambari toobe 目錄 777 權限與 hello spark 記錄檔位置。  
4. 以 sudo 的身分執行 spark-submit。  

## <a name="spark-phoenix-connector-is-not-supported"></a>不支援 Spark-Phoenix 連接器

目前，hello Spark in Phoenix 連接器不支援與 HDInsight Spark 叢集。

**緩和：**

您必須改用 hello Spark HBase 連接器。 如需指示，請參閱[如何 toouse Spark HBase 連接器](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)。

## <a name="issues-related-toojupyter-notebooks"></a>與 tooJupyter 筆記本相關的問題
以下是一些已知的問題相關的 tooJupyter 筆記型電腦。

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notebook 在檔名中有非 ASCII 字元
可以用在 Spark HDInsight 叢集中的 Jupyter Notebook，檔名中不該有非 ASCII 字元。 如果您嘗試 tooupload 透過 hello Jupyter UI 的非 ASCII 檔案名稱的檔案時，會以無訊息模式失敗 （也就是 Jupyter 不會讓您上傳 hello 檔案，但它可能不會擲回看見的錯誤）。 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>載入大型 Notebook 時發生錯誤
載入大型 Notebook 時，您可能會看到錯誤訊息 **`Error loading notebook`** 。  

**緩和：**

如果您收到這個錯誤，並不表示您的資料已損毀或遺失。  您的筆記型電腦有仍在磁碟中`/var/lib/jupyter`，您可以 SSH hello 叢集 tooaccess 到它們。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

一旦您已經連接使用 SSH toohello 叢集，您可以從叢集 tooyour 本機電腦 （使用 SCP 或 WinSCP） 複製您筆記本當做備份 tooprevent hello 遺失的 hello 筆記本中的任何重要資料。 您接著可以 SSH 通道至您的叢集前端節點，在連接埠 8001 tooaccess Jupyter 而不需要透過 hello 閘道。  從該處，您可以清除筆記本的 hello 輸出，並重新儲存 toominimize hello 筆記本的大小。

tooprevent hello 未來，您必須遵循的一些最佳做法中發生此錯誤：

* 它是小型的重要 tookeep hello 筆記型電腦大小。 任何輸出會傳送回 tooJupyter 會持續保留在 hello 筆記本從 Spark 作業。  與 Jupyter 最佳作法是在執行的一般 tooavoid`.collect()`在大型 RDD 的或資料框架; 相反地，如果您想在 RDD 內容 toopeek，請考慮執行`.take()`或`.sample()`使您的輸出不會太大。
* 此外，當您儲存筆記本，清除所有輸出資料格 tooreduce hello 大小。

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Notebook 的初始啟動比預期耗時
在使用 Spark magic 的 Jupyter Notebook 中，第一個程式碼陳述式可能需耗時一分鐘以上才能執行完畢。  

**說明：**

這是因為執行 hello 第一個程式碼儲存格時。 在 hello 背景這會起始工作階段設定和 Spark、 SQL、 和 Hive 內容設定。 設定這些內容之後，hello 第一個陳述式執行時，這可讓 hello 陳述式所花費很長的時間 toocomplete hello 印象。

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>在建立 hello 工作階段的 Jupyter 筆記本逾時
用完資源 Spark 叢集時，hello Spark 和 Pyspark 核心 hello Jupyter 筆記本中的，將會嘗試 toocreate hello 工作階段逾時。 

**緩和措施：** 

1. 藉由下列方式，釋出 Spark 叢集中的一些資源：
   
   * 停止其他移 toohello 關閉和 Halt 功能表或按一下 [關閉 hello 筆記本總管] 中的 Spark 筆記型電腦。
   * 從 YARN 停止其他 Spark 應用程式。
2. 重新啟動您嘗試 toostart 向上 hello 筆記型電腦。 足夠的資源可供您 toocreate 立即的工作階段。

## <a name="see-also"></a>另請參閱
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
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

