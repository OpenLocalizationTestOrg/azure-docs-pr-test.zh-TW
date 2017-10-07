---
title: "aaaAzure Toolkit for Eclipse-HDInsight Spark 建立 Scala 應用程式 |Microsoft 文件"
description: "使用 HDInsight Tools 在 Azure Toolkit Scala 以撰寫的 Eclipse toodevelop Spark 應用程式並將它們送出 tooan HDInsight Spark 叢集，直接從 hello Eclipse IDE。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>使用 Azure Toolkit 的 HDInsight 叢集的 Eclipse toocreate Spark 應用程式

在 Azure Toolkit for Eclipse toodevelop 使用 HDInsight Tools 二手 Scala 中撰寫的應用程式，並將它們送出 tooan Azure HDInsight Spark 叢集，直接從 Eclipse IDE hello。 您可以使用 hello HDInsight Tools 外掛程式幾個不同的方式：

* toodevelop 並提交 HDInsight Spark 叢集上的 Scala Spark 應用程式
* tooaccess Azure HDInsight Spark 叢集資源
* toodevelop 和執行本機 Scala Spark 應用程式

> [!IMPORTANT]
> 此工具可以使用的 toocreate 和送出應用程式僅適用於 linux 的 HDInsight Spark 叢集。
> 
> 

## <a name="prerequisites"></a>必要條件

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
* Oracle Java Development Kit 第 8 版，以用於 hello Eclipse IDE 執行階段。 您可以從 hello [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
* Eclipse IDE。 本文使用的是 Eclipse Neon。 您可以將它安裝從 hello [Eclipse 網站](https://www.eclipse.org/downloads/)。   
* Spark SDK。 您可以從 [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409) 下載。


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>在 Azure Toolkit 安裝 HDInsight Tools Eclipse 和 Scala 外掛程式
### <a name="install-hdinsight-tools"></a>安裝 HDInsight 工具
適用於 Eclipse 的 HDInsight 工具是適用於 Eclipse 的 Azure 工具組的一部分。 如需安裝指示，請參閱[安裝適用於 Eclipse 的 Azure 工具組](../azure-toolkit-for-eclipse-installation.md)。
### <a name="install-scala-plugin"></a>安裝 Scala 外掛程式
當您開啟 hello Intellij 時，hello HDInsight Tools 自動偵測是否或不安裝 Scala 外掛程式。 按一下**確定**toocontinue 然後遵循 hello 指示 tooinstall 由 hello Eclipse Marketplace。

 ![自動安裝 Scala 外掛程式](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>登入 tooyour Azure 訂用帳戶
1. 啟動 hello Eclipse IDE，並開啟 Azure 總管。 在 hello**視窗**功能表上，按一下 **顯示檢視**，然後按一下**其他**。 在開啟的 hello 對話方塊中，依序展開**Azure**，按一下**Azure 總管**，然後按一下**確定**。

    ![顯示檢視對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. 以滑鼠右鍵按一下 hello **Azure**節點，然後再按一下**登入**。
3. 在 hello **Azure 登入**對話方塊方塊中，選擇 hello 驗證方法中，按一下**登入**，並輸入您的 Azure 認證。
   
    ![[Azure 登入] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. 您已登入之後，hello**選取的訂用帳戶**對話方塊方塊中列出所有 hello 與 hello 認證相關聯的 Azure 訂用帳戶。 按一下**選取**tooclose hello 對話方塊。

    ![[選取訂用帳戶] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. 在 hello **Azure 總管**索引標籤上，依序展開**HDInsight** toosee hello HDInsight Spark 叢集，您的訂用帳戶底下。
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. 您可以進一步展開叢集名稱節點 toosee hello （例如，儲存體帳戶） 相關聯的資源與 hello 叢集。
   
    ![展開叢集名稱 toosee 資源](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>設定 HDInsight Spark 叢集的 Spark Scala 專案

1. 在 hello Eclipse IDE 工作區中，按一下 **檔案**，按一下**新增**，然後按一下**專案**。 
2. 在 hello 新專案精靈 中，展開**HDInsight**，選取**HDInsight (Scala) 上的 Spark**，然後按一下**下一步**。

    ![選取 HDInsight (Scala) 專案上的 Spark hello](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. hello Scala 專案建立精靈自動偵測是否或不安裝 Scala 外掛程式。 按一下**確定**toocontinue 下載 hello Scala 外掛程式，然後遵循 hello 指示 toorestart Eclipse。

    ![Scala 檢查](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. 在 hello**新 HDInsight Scala 專案**對話方塊中，提供 hello 下列值，然後再按一下**下一步**:
   * 輸入 hello 專案的名稱。
   * 在 hello **JRE**區域中，請確定**使用執行環境 JRE**設定得**JavaSE 1.7**或更新版本。
   * 請確定 Spark SDK 下載 hello SDK 組 toohello 位置。 hello 連結 toohello 下載中包含位置 hello[必要條件](#prerequisites)稍早在本文章。 您也可以從 hello 下載 hello SDK 包含 hello 對話方塊中的連結。

    ![[新增 HDInsight Scala 專案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  在 hello 下一步 對話方塊中，按一下 hello**文件庫**索引標籤上，並保留 hello 的預設值，然後按一下**完成**。 
   
    ![[程式庫] 索引標籤](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>建立 HDInsight Spark 叢集的 Scala 應用程式

1. 在 hello Eclipse IDE 中，從 封裝總管 中，展開您稍早建立的 hello 專案，以滑鼠右鍵按一下**src**，點太**新增**，然後按一下**其他**。
2. 在 hello**選取精靈**對話方塊方塊中，展開  **Scala 精靈**，按一下  **Scala 物件**，然後按一下**下一步**。
   
    ![選取精靈對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. 在 hello**開新檔案**對話方塊中，輸入 hello 物件的名稱，然後按一下**完成**。
   
    ![[建立新檔案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. 貼上下列程式碼 hello 文字編輯器中的 hello:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. HDInsight Spark 叢集上執行 hello 應用程式：
   
   1. 封裝總管 中，從 hello 專案名稱，以滑鼠右鍵按一下，然後選取**提交 Spark 應用程式 tooHDInsight**。        
   2. 在 hello **Spark 提交**對話方塊中，提供 hello 下列值，然後再按一下**送出**:
      
      * 如**叢集名稱**，選取 hello 想 toorun HDInsight Spark 叢集應用程式。
      * Hello Eclipse 的專案，從選取的成品，或選取從硬碟機。 hello 預設值取決於您以滑鼠右鍵按一下封裝總管 中的 hello 項目。
      * 在 hello**主要類別名稱**dropdownlist，精靈會顯示從選定專案的所有物件名稱的提交。 選取或輸入一個您要 toorun。 如果您從硬碟選取構件，您必須自行輸入主要類別名稱。 
      * 因為在此範例中的 hello 應用程式程式碼不需要任何命令列引數或參考 （每瓶） 或檔案，您可以保留 hello 剩餘的空文字方塊。
        
       ![[提交 Spark] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. hello **Spark 提交** 索引標籤應該開始顯示 hello 進度。 您可以在 hello hello 紅色按鈕，即可停止 hello 應用程式**Spark 提交**視窗。 您也可以檢視 hello hello 地球圖示 （hello 映像中的 hello 藍色方塊以表示），即可執行此特定應用程式的記錄檔。
      
       ![[提交 Spark] 視窗](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具來存取和管理 HDInsight Spark 叢集
您可以使用 HDInsight 工具，包括存取 hello 工作輸出執行各種作業。

### <a name="access-hello-job-view"></a>存取 hello 工作檢視
1. 在 Azure 總管] 中，依序展開**HDInsight**，依序展開 [hello Spark 叢集名稱，然後按一下**作業**。 

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. 按一下 hello**作業**節點。 hello HDInsight Tools 自動偵測是否或不安裝 hello E (fx) clipse 外掛程式。 按一下**確定**toocontinue 與後續 hello 指示 tooinstall hello Eclipse Marketplace 並重新啟動 Eclipse。

    ![安裝 E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. 開啟 hello 工作檢視從 hello**作業**節點。 Hello 右窗格中，hello **Spark 工作檢視**索引標籤會顯示 hello 叢集所執行的所有 hello 應用程式。 按一下 hello hello 要 toosee 更多詳細資料的應用程式名稱。

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. 如果您將滑鼠停留在 hello 作業圖形，它會顯示基本執行的作業資訊。 按一下即可在 hello 作業圖形顯示 hello 階段圖形和每項工作產生的資訊。

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. 常用的記錄檔，包括驅動程式 Stderr、 驅動程式 Stdout 和目錄資訊會列在 hello**記錄** 索引標籤。

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. 您也可以按一下 hello 視窗頂端的 hello hello 各自的超連結，開啟 hello Spark 記錄 UI 和 hello YARN UI （hello 應用程式層級）。

### <a name="access-hello-storage-container-for-hello-cluster"></a>Hello 叢集存取 hello 儲存體容器
1. 在 Azure 總管] 中，展開 [hello **HDInsight**根節點 toosee HDInsight Spark 叢集可用的清單。
2. 展開 hello 叢集名稱 toosee hello 儲存體帳戶與 hello hello 叢集的預設儲存體容器。
   
    ![儲存體帳戶和預設儲存體容器](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. 按一下 hello 與 hello 叢集相關聯的儲存體容器名稱。 Hello 右窗格中，按兩下 hello **HVACOut**資料夾。 開啟其中一個 hello**一部分-**檔案 toosee hello hello 應用程式輸出。

### <a name="access-hello-spark-history-server"></a>存取 hello Spark 記錄伺服器
1. 在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。 當提示您時，請輸入 hello 叢集 hello 系統管理員認證。 您必須指定這些佈建 hello 叢集時。
2. Hello Spark 記錄伺服器儀表板 中，您可以使用 hello 應用程式名稱 toolook hello 剛剛完成執行的應用程式。 在上述程式碼的 hello，您必須設定 hello 應用程式名稱使用`val conf = new SparkConf().setAppName("MyClusterApp")`。 因此，Spark 應用程式名稱為 **MyClusterApp**。

### <a name="start-hello-ambari-portal"></a>啟動 hello Ambari 入口網站
1. 在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。 
2. 當提示您時，請輸入 hello 叢集 hello 系統管理員認證。 您必須指定這些佈建 hello 叢集時。

### <a name="manage-azure-subscriptions"></a>管理 Azure 訂用帳戶
根據預設，在 Azure Toolkit for Eclipse HDInsight 工具會列出所有您 Azure 訂用帳戶的 hello Spark 叢集。 如有必要，您可以指定要 tooaccess hello 叢集 hello 訂用帳戶。 

1. 在 Azure 總管 中，以滑鼠右鍵按一下 hello **Azure**根節點，然後**管理訂用帳戶**。 
2. 在 [hello] 對話方塊中，清除 hello hello 訂用帳戶，您不想 tooaccess，，然後按一下核取方塊**關閉**。 您也可以按一下**登出**如果想要從您的 Azure 訂用帳戶的 toosign。

## <a name="run-a-spark-scala-application-locally"></a>在本機執行 Spark Scala 應用程式
您可以使用 HDInsight Tools 在 Azure Toolkit Eclipse toorun Spark Scala 應用程式在本機工作站上。 一般而言，這些應用程式不需要存取 toocluster 資源，例如儲存體容器，而且您可以執行，並在本機測試它們。

### <a name="prerequisite"></a>必要條件
雖然您在 Windows 電腦上執行 hello 本機 Spark Scala 應用程式，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)。 發生這個例外狀況是因為 Windows 中遺失 **WinUtils.exe**。 

tooresolve 這個錯誤，您必須[下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置**C:\WinUtils\bin**。 然後，您必須加入 hello 環境變數**HADOOP_HOME**並設定 hello hello 變數值太**C\WinUtils**。

### <a name="run-a-local-spark-scala-application"></a>執行本機 Spark Scala 應用程式
1. 啟動 Eclipse，然後建立專案。 在 hello**新專案**對話方塊中，請 hello 下列選項，然後再按一下**下一步**。
   
   * Hello 左窗格中，選取**HDInsight**。
   * Hello 右窗格中，選取**HDInsight 本機執行範例 (Scala) 上的 Spark**。

    ![New Project dialog box](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. tooprovide hello 專案詳細資料，遵循步驟 3 到 6 從 hello 前一節[設定 Spark Scala 專案 HDInsight Spark 叢集](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster)。
3. hello 範本加入程式碼範例 (**LogQuery**) 下 hello **src**您可以在本機執行您的電腦的資料夾。
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. 以滑鼠右鍵按一下 hello **LogQuery**應用程式中，點太**執行身分**，然後按一下 **1 個 Scala 應用程式**。 您會看到如下輸出中 hello**主控台**hello 底部的索引標籤：
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>常見問題集
應用程式 tooAzure 資料湖存放區，toosubmit 選擇**互動式**hello Azure 登入程序期間的模式。 如果您選取 [自動] 模式，可能會發生錯誤。

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

現在，我們已解決了。 您可以使用任何登入方法選擇 Azure 資料湖叢集 toosubmit 您的應用程式。

## <a name="feedback-and-known-issues"></a>意見反應和已知問題
目前，不支援直接檢視 Spark 輸出。

如果您有任何建議或意見反應，或使用此工具時，遇到任何問題，您可用 toosend 我們在電子郵件hdivstool@microsoft.com。

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>建立和執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [使用 Azure Toolkit for IntelliJ toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

