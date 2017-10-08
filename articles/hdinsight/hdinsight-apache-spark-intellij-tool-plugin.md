---
title: "適用於 IntelliJ 的 Azure 工具組：建立適用於 HDInsight 叢集的 Spark 應用程式 | Microsoft Docs"
description: "使用 hello Azure Toolkit IntelliJ toodevelop Spark 應用程式撰寫的 Scala，並將它們送出 tooan HDInsight Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>使用 Azure Toolkit 的 HDInsight 叢集的 IntelliJ toocreate Spark 應用程式

Hello Azure Toolkit 用於 Scala，以撰寫的 IntelliJ 外掛程式 toodevelop Spark 應用程式，然後將它們送出 tooan HDInsight Spark 叢集，直接從 hello IntelliJ 整合式的開發環境 (IDE)。 您可以使用一些方式外掛程式 hello:

* 在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。
* 存取您的 Azure HDInsight Spark 叢集資源。
* 在本機開發並執行 Scala Spark 應用程式。

toocreate 您專案中，檢視 hello[建立 Spark 應用程式以 hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)視訊。

> [!IMPORTANT]
> 您可以使用這個外掛程式 toocreate 並送出應用程式僅適用於 linux 的 HDInsight Spark 叢集。
> 

## <a name="prerequisites"></a>必要條件

- HDInsight Linux 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
- Oracle Java Development Kit。 您可以將它安裝從 hello [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
- IntelliJ IDEA。 本文章使用 2017.1 版。 您可以將它安裝從 hello [JetBrains 網站](https://www.jetbrains.com/idea/download/)。

## <a name="install-azure-toolkit-for-intellij"></a>安裝適用於 IntelliJ 的 Azure 工具組
如需安裝指示，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](../azure-toolkit-for-intellij-installation.md)。

## <a name="sign-in-tooyour-azure-subscription"></a>登入 tooyour Azure 訂用帳戶

1. 啟動 hello IntelliJ IDE，並開啟 Azure 總管。 在 hello**檢視**功能表上，選取**工具視窗**，然後選取**Azure 總管**。
       
   ![hello Azure 總管連結](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. 以滑鼠右鍵按一下 hello **Azure**節點，然後再選取**登入**。

3. 在 hello **Azure 登入**對話方塊中，選取**登入**，然後輸入您的 Azure 認證。

    ![hello Azure 登入 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. 您已登入之後，hello**選取的訂用帳戶**對話方塊方塊中列出所有 hello Azure 訂用帳戶相關聯 hello 認證。 選取 hello**選取** 按鈕。

    ![hello 選取多個訂閱對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. 在 hello **Azure 總管**索引標籤上，依序展開**HDInsight** tooview hello HDInsight Spark 叢集，您的訂用帳戶中。
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello （例如，儲存體帳戶） 相關聯的資源與 hello 叢集，您可以進一步展開叢集名稱節點。
   
    ![展開的叢集名稱節點](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>在 HDInsight Spark 叢集上執行 Spark Scala 應用程式

1. 啟動 IntelliJ IDEA，然後建立專案。 在 hello**新專案**對話方塊方塊中，執行下列 hello: 

   a. 選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。

   b. 在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:

      * **Maven**，以支援 Scala 專案建立精靈
      * **SBT**、 管理 hello 相依性和建置 hello Scala 專案

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. 選取 [下一步] 。

3. hello Scala 專案建立精靈會自動偵測您的電腦已安裝的 hello Scala 外掛程式。 選取 [安裝]。

   ![Scala 外掛程式檢查](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. toodownload hello Scala 外掛程式，請選取**確定**。 請遵循 hello 指示 toorestart IntelliJ。 

   ![hello Scala 外掛程式安裝對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. 在 hello**新的專案**視窗中，執行下列 hello:  

    ![選取 hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. 輸入專案名稱和位置。

   b. 在 hello**專案 SDK**下拉式清單中，選取**Java 1.8** hello Spark 2.x 叢集，或選取**Java 1.7** hello Spark 1.x 叢集。

   c. 在 hello **Spark 版本**下拉式清單中，Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。 如果 hello Spark 叢集版本早於 2.0，請選取**二手 1.x**。 否則，請選取 [Spark2.x]。 此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。

6. 選取 [完成]。

7. hello Spark 專案會自動為您建立成品。 tooview hello 成品，請勿遵循 hello:

   a. 在 hello**檔案**功能表上，選取**專案結構**。

   b. 在 hello**專案結構**對話方塊中，選取**成品**tooview hello 預設成品所建立。 您也可以藉由選取加號 hello 建立您自己的成品 (**+**)。

      ![在 [hello] 對話方塊中的成品資訊](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. 執行 hello 下列新增您的應用程式的原始程式碼：

   a. 在 [專案總管] 中，以滑鼠右鍵按一下**src**，點太**新增**，然後選取**Scala 類別**。
      
      ![從 [專案總管] 中建立 Scala 類別的命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. 在 hello**建立類別的新 Scala**對話方塊方塊中，提供的名稱，選取**物件**在 hello**種類**方塊，並選取**[確定]**。
      
      ![建立新的 Scala 類別對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. 在 hello **MyClusterApp.scala**檔案中，貼上下列程式碼的 hello。 hello 程式碼，讀取 hello HVAC.csv （可在所有的 HDInsight Spark 叢集上），擷取 hello 資料列只有一個數字 hello 第七個資料行都在 hello CSV 檔案中，並將 hello 輸出太**/HVACOut**下 hello 預設hello 叢集的儲存體容器。

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. 藉由 hello 下列 HDInsight Spark 叢集執行 hello 應用程式：

   a. 在 專案總管 hello 專案名稱，以滑鼠右鍵按一下，然後選取**提交 Spark 應用程式 tooHDInsight**。
      
      ![hello 提交 Spark 應用程式 tooHDInsight 命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. 您會提示的 tooenter 您 Azure 訂用帳戶的認證。 在 hello **Spark 提交**對話方塊中，提供下列值的 hello，然後選取**送出**。
      
      * 如**二手叢集 (僅 Linux)**，選取 hello 想 toorun HDInsight Spark 叢集應用程式。

      * Hello IntelliJ 專案，從選取的成品，或選取從 hello 硬碟機。

      * 在 hello**主要類別名稱**方塊中，選取 hello 省略符號 (**...**) 應用程式程式碼中，選取 hello 主要類別，然後選取**確定**。

        ![hello 選取主要類別對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * 因為在此範例中的 hello 應用程式程式碼不需要命令列引數或參考 （每瓶） 或檔案，您可以保留 hello 剩餘空白的方塊。 提供所有 hello 資訊之後，hello 對話方塊看起來應該像 hello 下列映像。
        
        ![hello Spark 提交對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. hello **Spark 提交**在 hello hello 視窗底部的索引標籤應該開始顯示 hello 進度。 您也可以停止 hello 應用程式藉由選取 hello 紅色按鈕在 hello **Spark 提交**視窗。
      
      ![hello Spark 提交視窗](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn 如何 tooaccess hello 作業輸出，請參閱 hello 」 存取和管理 HDInsight Spark 叢集，請使用 Azure Toolkit for IntelliJ"本文中稍後的章節。

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>在 HDInsight Spark 叢集上執行或偵錯 Spark Scala 應用程式
我們也建議送出 hello Spark 應用程式 toohello 叢集的另一種。 您可以藉由設定 hello 參數在 hello**執行/偵錯組態**IDE。 如需詳細資訊，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>使用適用於 IntelliJ 的 Azure 工具組來存取和管理 HDInsight Spark 叢集
您可以使用適用於 IntelliJ 的 Azure 工具組來執行各種作業。

### <a name="access-hello-job-view"></a>存取 hello 工作檢視
1. 在 Azure 總管] 中，依序展開**HDInsight**，依序展開 [hello Spark 叢集名稱，然後選取**作業**。  

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Hello 右窗格中，hello **Spark 工作檢視**索引標籤會顯示 hello 叢集所執行的所有 hello 應用程式。 選取 hello hello 要 toosee 更多詳細資料的應用程式名稱。

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay 基本執行作業資訊暫留在 hello 作業圖形。 tooview hello 階段圖形和資訊所產生的每個工作，請選取 hello 作業圖形的節點。

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview 常用的記錄檔，例如*驅動程式 Stderr*，*驅動程式 Stdout*，和*目錄資訊*，選取 hello**記錄** 索引標籤。

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. 您也可以選取 hello hello 視窗上方的連結，檢視 hello Spark 記錄 UI 和 hello YARN UI （hello 應用程式層級）。

### <a name="access-hello-spark-history-server"></a>存取 hello Spark 記錄伺服器
1. 在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。 

2. 當提示您時，請輸入 hello 叢集系統管理員認證，您可以指定當您設定 hello 叢集。

3. Hello Spark 記錄伺服器儀表板上，您可以使用 hello 應用程式名稱 toolook hello 剛剛完成執行的應用程式。 在上述程式碼的 hello，您必須設定 hello 應用程式名稱使用`val conf = new SparkConf().setAppName("MyClusterApp")`。 因此，Spark 應用程式名稱為 **MyClusterApp**。

### <a name="start-hello-ambari-portal"></a>啟動 hello Ambari 入口網站
1. 在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。 

2. 當提示您時，請輸入 hello 叢集 hello 系統管理員認證。 您可以指定這些認證 hello 叢集安裝程序期間。

### <a name="manage-azure-subscriptions"></a>管理 Azure 訂用帳戶
根據預設，Azure Toolkit for IntelliJ 會列出所有您 Azure 訂用帳戶的 hello Spark 叢集。 如有必要，您可以指定您想 tooaccess hello 訂用帳戶。 

1. 在 Azure 總管 中，以滑鼠右鍵按一下 hello **Azure**根節點，然後再選取**管理訂用帳戶**。 

2. 在 [hello] 對話方塊中，清除 hello 核取方塊下一步 toohello 訂用帳戶，您不想 tooaccess，，然後選取**關閉**。 您也可以選取**登出**如果想要從您的 Azure 訂用帳戶的 toosign。

## <a name="run-a-spark-scala-application-locally"></a>在本機執行 Spark Scala 應用程式
您的工作站上，您可以在本機使用 Azure Toolkit IntelliJ toorun Spark Scala 應用程式。 hello 應用程式通常不需要存取 toocluster 資源，例如儲存體容器，您可以執行和測試它們，在本機。

### <a name="prerequisite"></a>必要條件
雖然您在 Windows 電腦上執行 hello 本機 Spark Scala 應用程式，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)。 因為 WinUtils.exe 遺漏 Windows 上，就會發生 hello 例外狀況。 

tooresolve 這個錯誤，[下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置，如**C:\WinUtils\bin**。 接著，新增 hello 環境變數**HADOOP_HOME**，並設定 hello hello 變數值太**C\WinUtils**。

### <a name="run-a-local-spark-scala-application"></a>執行本機 Spark Scala 應用程式
1. 啟動 IntelliJ IDEA 並建立專案。 

2. 在 hello**新專案**對話方塊方塊中，執行下列 hello:
   
    a. 選取 [HDInsight] > [HDInsight 上的 Spark 本機執行範例 (Scala)]。

    b. 在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:

      * **Maven**，以支援 Scala 專案建立精靈
      * **SBT**、 管理 hello 相依性和建置 hello Scala 專案

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. 選取 [下一步] 。
 
4. 在 hello 下一步 視窗中，請勿 hello 遵循：
   
    a. 輸入專案名稱和位置。

    b. 在 hello**專案 SDK**下拉式清單中，選取晚於 1.7 版的 Java 版本。

    c. 在 hello **Spark 版本**下拉式清單中，您想 toouse Scala 選取 hello 版本： Scala Spark 2.0 或 Scala 2.11.x Spark 1.6 的 2.10.x。

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. 選取 [完成]。

6. hello 範本加入程式碼範例 (**LogQuery**) 下 hello **src**您可以在本機執行您的電腦的資料夾。
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. 以滑鼠右鍵按一下 hello **LogQuery**應用程式，然後再選取**執行 'LogQuery'**。 在 [hello**執行**] 索引標籤底部 hello，您會看到類似 hello 下列輸出：
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>轉換現有 IntelliJ 概念應用程式 toouse Azure Toolkit for IntelliJ
您可以將轉換 hello 現有 Spark Scala 建立應用程式 IntelliJ 概念 toobe 中與 Azure Toolkit for IntelliJ。 然後，您可以使用 hello 外掛程式 toosubmit hello 應用程式 tooan HDInsight Spark 叢集。

1. 針對現有的 Spark Scala 應用程式建立透過 IntelliJ 概念，開啟 hello 相關聯的.iml 檔案。

2. 在 hello 根層級是**模組**hello 如下的項目：
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   編輯 hello 元素 tooadd`UniqueKey="HDInsightTool"`因此的 hello**模組**項目看起來類似下列 hello:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. 儲存 hello 的變更。 您的應用程式現在應該可與適用於 IntelliJ 的 Azure 工具組相容。 您可以測試它，以滑鼠右鍵按一下 [專案總管] 中的 hello 專案名稱。 hello 快顯功能表現在具有 hello 選項**提交 Spark 應用程式 tooHDInsight**。

## <a name="troubleshooting"></a>疑難排解

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>本機執行的錯誤：「請使用較大的堆積大小」
中的 Spark 1.6，如果您在本機執行，使用 32 位元 Java SDK 可能會遇到下列錯誤 hello:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

因為不是大型的 Spark toorun hello 堆積的大小，則會發生這些錯誤。 Spark 需要至少 471 MB (如需詳細資訊，請參閱 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081))。一個簡單的解決方案是 toouse 64 位元 Java SDK。 您也可以藉由新增下列選項的 hello 變更 IntelliJ hello JVM 設定：

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![加入選項 toohello 方塊 IntelliJ 中的 「 VM 選項 」](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>常見問題集
應用程式 tooAzure 資料湖存放區，toosubmit 選擇**互動式**hello Azure 登入程序期間的模式。 如果您選取 [自動] 模式，可能會發生錯誤。

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

現在，我們已解決了。 您可以使用任何登入方法選擇 Azure 資料湖叢集 toosubmit 您的應用程式。

## <a name="feedback-and-known-issues"></a>意見反應和已知問題
目前，不支援直接檢視 Spark 輸出。

如果您有任何建議或意見反應，或使用此外掛程式時遇到任何問題，請將電子郵件傳送到 hdivstool@microsoft.com。

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

### <a name="creating-and-running-applications"></a>建立和執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

