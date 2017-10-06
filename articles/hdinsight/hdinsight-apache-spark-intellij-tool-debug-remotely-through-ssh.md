---
title: "適用於 IntelliJ 的 Azure 工具組：透過 SSH 對 Spark 應用程式進行遠端偵錯 | Microsoft Docs"
description: "透過 SSH toouse HDInsight Tools 在 Azure Toolkit for IntelliJ toodebug 應用程式，在 HDInsight 上的遠端叢集的方式的逐步指引"
keywords: "遠端偵錯 intellij, 進行 intellij 遠端偵錯, ssh, intellij, hdinsight, 偵錯 intellij, 偵錯"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行偵錯

這篇文章提供有關逐步指引 toouse HDInsight Tools 在 Azure Toolkit IntelliJ toodebug 上的應用程式從遠端的 HDInsight 叢集。 toodebug 您的專案，您也可以檢視 hello[偵錯 HDInsight Spark 應用程式使用 Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)視訊。

**必要條件**

* **適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具**。 此工具是適用於 IntelliJ 之 Azure 工具組的一部分。 如需詳細資訊，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation)。
* **適用於 IntelliJ 的 Azure 工具組**。 HDInsight 叢集使用此工具組 toocreate Spark 應用程式。 如需詳細資訊，請依照下列中的 hello 指示[使用 Azure Toolkit for IntelliJ toocreate Spark 應用程式的 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin)。
* **HDInsight SSH 服務與使用者名稱和密碼管理**。 如需詳細資訊，請參閱[透過 SSH 連線 tooHDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)和[使用 SSH 通道 tooaccess Ambari web UI、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel)。 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>建立 Spark Scala 應用程式，並設定它以進行遠端偵錯

1. 啟動 IntelliJ IDEA，然後建立專案。 在 hello**新專案**對話方塊方塊中，執行下列 hello:

   a. 選取 [HDInsight]。 

   b. 根據您的喜好設定選取 Java 或 Scala 範本。 選取下列選項的 hello:

      - **Spark on HDInsight (Scala) \(HDInsight 上的 Spark (Scala)\)**

      - **Spark on HDInsight (Java) \(HDInsight 上的 Spark (Java)\)**

      - Spark on HDInsight Cluster Run Sample (Scala) \(HDInsight 叢集上的 Spark 執行範例 (Scala)\)

      此範例會使用 [Spark on HDInsight Cluster Run Sample (Scala)] \(HDInsight 叢集上的 Spark 執行範例 (Scala)) 範本。

   c. 在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:

      - **Maven**，以支援 Scala 專案建立精靈

      -  **SBT**、 管理 hello 相依性和建置 hello Scala 專案 

      ![建立偵錯專案](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. 選取 [下一步] 。     
 
3. Hello 中下一步**新專案**視窗中，請勿遵循 hello:

   ![選取 hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. 輸入專案名稱和專案位置。

   b. 在 hello**專案 SDK**下拉式清單中，選取**Java 1.8**的**二手 2.x**叢集，或選取**Java 1.7**的**Spark 1。x**叢集。

   c. 在 hello **Spark 版本**下拉式清單中，hello Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。 如果 hello spark 叢集版本早於 2.0，請選取**二手 1.x**。 否則，請選取 **Spark 2.x**。 此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。

   d. 選取 [完成]。

4. 選取**src** > **主要** > **scala** tooopen hello 專案中的程式碼。 這個範例會使用 hello **SparkCore_wasbloTest**指令碼。

5. tooaccess hello**編輯組態**功能表中，選取 hello hello 右上角的圖示。 從這個功能表中，您可以建立或編輯 hello 組態進行遠端偵錯。

   ![編輯設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. 在 [hello**執行/偵錯組態**] 對話方塊中，選取 hello 加號 (**+**)。 然後選取 hello**提交 Spark 作業**選項。

   ![新增設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. 輸入 [Name] \(名稱\)、**[Spark cluster] \(Spark 叢集\)** 和 [Main class name] \(主要類別名稱\)。 然後選取 [Advanced configuration] \(進階設定\)。 

   ![[Run/Debug Configurations] \(執行/偵錯設定\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. 在 hello **Spark 提交進階設定**對話方塊中，選取**啟用 Spark 遠端偵錯**。 輸入 hello SSH 使用者名稱，然後輸入密碼，或使用私用金鑰檔。 toosave hello 設定，請選取**確定**。

   ![[Enable Spark remote debug] \(啟用 Spark 遠端偵錯\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. hello 組態現在是以您所提供的 hello 名稱儲存。 tooview hello 設定詳細資料，選取 hello 組態名稱。 選取 toomake 變更**編輯組態**。 

10. Hello 組態設定完成之後，您可以針對 hello 遠端叢集執行 hello 專案或執行遠端偵錯。

## <a name="learn-how-tooperform-remote-debugging"></a>深入了解如何 tooperform 遠端偵錯
### <a name="scenario-1-perform-remote-run"></a>案例 1：執行遠端執行

在本節中，我們會示範如何 toodebug 驅動程式和執行程式。

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. 設定中斷點，然後再選取 hello**偵錯**圖示。

   ![選取 hello 偵錯圖示](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. 當執行 hello 程式達到 hello 重大點時，您會看到**驅動程式** 索引標籤和兩個**Executor** hello 中的索引標籤**偵錯工具**窗格。 選取 hello**繼續程式**執行 hello 程式碼，然後到達 hello 下一個中斷點，並著重於 hello 對應的圖示 toocontinue **Executor**  索引標籤。您可以檢閱 hello hello 對應的執行記錄**主控台** 索引標籤。

   ![[Debug] \(偵錯\) 索引標籤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>案例 2：執行遠端偵錯和錯誤修正
在本節中，我們會示範如何使用的 toodynamically 更新 hello 變數值 hello IntelliJ 偵錯功能對簡單的修正。 在下列程式碼範例的 hello，因為 hello 目標檔案已存在，會擲回例外狀況。
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>tooperform 遠端偵錯和 bug 修正
1. 設定兩個中斷點，然後再選取 hello**偵錯**圖示 toostart hello 遠端偵錯處理序。

2. hello 程式碼會停止在 hello 第一次中斷時間點，而且 hello 參數和變數的資訊會顯示 hello**變數**窗格。 

3. 選取 hello**繼續程式**圖示 toocontinue。 hello 程式碼會在 hello 第二個點停止。 如預期般，會攔截到 hello 例外狀況。

  ![擲回錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. 選取 hello**繼續程式**圖示一次。 hello **HDInsight Spark 提交**視窗會顯示 「 工作執行失敗 」 錯誤。

  ![提交錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. 選取 使用 hello IntelliJ 偵錯功能的 toodynamically 更新 hello 變數值**偵錯**一次。 hello**變數**窗格會顯示一次。 

6. 以滑鼠右鍵按一下 hello 目標上 hello**偵錯**索引標籤，然後選取**設定值**。 接下來，輸入新的值為 hello 變數。 然後選取**Enter** toosave hello 值。 

  ![設定值](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. 選取 hello**繼續程式**圖示 toocontinue toorun hello 程式。 此時，不會攔截到任何例外狀況。 您可以看到該 hello 專案成功執行不含任何例外狀況。

  ![偵錯而未發生例外狀況](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>接續步驟
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>示範
* 建立 Scala 專案 (影片)：[Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (建立 Spark Scala 應用程式)
* 遠端偵錯 （影片）：[使用 Azure Toolkit for IntelliJ toodebug Spark 應用程式，從遠端在 HDInsight 叢集上](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [機器學習的 Spark： 使用 HDInsight tooanalyze 建置溫度使用 HVAC 資料中的 Spark](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight toobuild 即時串流應用程式中的 Spark Streaming： 使用 Spark](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [使用 Azure Toolkit 的 HDInsight 叢集的 IntelliJ toocreate Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [適用於在 hello HDInsight Spark 叢集中的 Jupyter 筆記本的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
