---
title: "aaaAzure IntelliJ-在 HDInsight Spark 上遠端偵錯應用程式的工具組 |Microsoft 文件"
description: "深入了解如何在 Azure Toolkit 使用 HDInsight Tools for IntelliJ tooremotely 偵錯應用程式透過 vpn HDInsight Spark 叢集上執行。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>使用 Azure Toolkit IntelliJ toodebug 上的應用程式從遠端透過 VPN HDInsight Spark

我們建議偵錯 spark applicaltion 從遠端透過 ssh 的 hello 的方法。 如需指示，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。

本文章提供如何 toouse hello IntelliJ toosubmit HDInsight Spark 叢集上的 Spark 作業在 Azure Toolkit HDInsight Tools，然後遠端偵錯它從您桌面的電腦上的逐步指引。 toodo 因此，您必須執行下列高階步驟 hello:

1. 建立站對站或點對站 Azure 虛擬網路。 本文件中的 hello 步驟假設您使用站對站網路。
2. 建立屬於 hello-網站 Azure 虛擬網路的 Azure HDInsight Spark 叢集。
3. 確認 hello hello 叢集前端節點與您的桌面之間的連線。
4. 在 IntelliJ IDEA 中建立 Scala 應用程式，並設定它以進行遠端偵錯。
5. 執行和偵錯 hello 應用程式。

## <a name="prerequisites"></a>必要條件
* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
* Oracle Java Development Kit。 您可以從 [這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)加以安裝。
* IntelliJ IDEA。 本文章使用 2017.1 版。 您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。
* 適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具。 HDInsight 工具 IntelliJ 可用 hello Azure Toolkit for IntelliJ 的一部分。 如需有關如何 tooinstall hello Azure Toolkit 的指示，請參閱[安裝 hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。
* 從 IntelliJ IDEA 登入您的 Azure 訂用帳戶。 請依照下列指示 hello[這裡](hdinsight-apache-spark-intellij-tool-plugin.md)。
* 在執行遠端偵錯在 Windows 電腦上的 Spark Scala 應用程式時，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) ，就會發生因為 tooa 遺漏 WinUtils.exe Windows 上的。 您必須解決此錯誤 toowork，[從這裡下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置**C:\WinUtils\bin**。 然後，您必須加入環境變數**HADOOP_HOME**並設定 hello hello 變數值太**C\WinUtils**。

## <a name="step-1-create-an-azure-virtual-network"></a>步驟 1：建立 Azure 虛擬網路
請依照下方連結 toocreate Azure 虛擬網路的 hello hello 指示，然後確認 hello hello 桌面和 Azure 虛擬網路之間的連線。

* [使用 Azure 入口網站建立具有站對站 VPN 連線的 VNet](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [使用 PowerShell 建立具有站對站 VPN 連線的 VNet](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [設定點對站連線 tooa 虛擬網路使用 PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>步驟 2：建立 HDInsight Spark 叢集
您也應該屬於 hello 您建立 Azure 虛擬網路的 Azure HDInsight 上建立的 Apache Spark 叢集。 使用可用的 hello 資訊[HDInsight 中的 建立 linux 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 選擇性組態的一部分，選取 hello hello 先前步驟中所建立的 Azure 虛擬網路。

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>步驟 3： 確認 hello hello 叢集前端節點與您的桌面之間的連線
1. 收到 hello 的 hello 叢集前端節點的 IP 位址。 開啟 hello 叢集 Ambari UI。 從 hello 叢集刀鋒視窗中，按一下 **儀表板**。

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. 從 hello Ambari UI 從 hello 右上角，按一下 **主機**。

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. 您應該會看到前端節點、背景工作角色節點和 zookeeper 節點的清單。 hello headnodes 擁有 hello **hn*** 前置詞。 按一下 hello 第一個前端節點。

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. 在 hello 開啟時，從 hello 的 hello 頁面底端**摘要**方塊中，複製 hello IP 位址的 hello 叢集前端節點和 hello 主機名稱。

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. 包含 hello IP 位址和 hello 主機名稱的 hello 叢集前端節點 toohello**主機**hello 您想 toorun 和進行遠端偵錯 hello Spark 工作的電腦上的檔案。 這可讓您 toocommunicate 與 hello 叢集前端節點使用 hello IP 位址與 hello 主機名稱。

   1. 以提高的權限開啟 [記事本]。 Hello 檔案 功能表中按一下**開啟**，然後瀏覽 toohello hello hosts 檔案位置。 在 Windows 電腦上，是 `C:\Windows\System32\Drivers\etc\hosts`。
   2. 新增下列 toohello hello**主機**檔案。

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. 從 hello 連接 toohello hello HDInsight 叢集所使用的 Azure 虛擬網路的電腦，請確認您可以 ping hello IP 位址，以及 hello 主機名稱使用這兩個 hello headnodes。
7. SSH 到 hello 叢集前端節點使用 hello 指示[使用 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)。 Hello 叢集前端節點，從 ping hello hello 桌面的電腦 IP 位址。 您應該測試連線 tooboth hello IP 位址指派 toohello 電腦，另一個用於 hello 網路連線，且 hello 其他 hello Azure 虛擬網路的 hello 電腦已連線到。
8. 重複 hello 以及其他前端節點 hello 步驟。

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>步驟 4： 建立使用 Azure Toolkit 中的 hello HDInsight Tools for IntelliJ Spark Scala 應用程式，並將其設定為遠端偵錯
1. 啟動 IntelliJ IDEA，並建立新的專案。 在 hello 新專案 對話方塊進行 hello 下列選項，然後按一下**下一步**。

    ![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * 從 hello 左窗格中，選取**HDInsight**。
   * 從 hello 右窗格中，選取**HDInsight (Scala) 上的 Spark**。
   * 按一下 [下一步] 。
2. 在 hello 下一步 視窗中，提供 hello 下列專案的詳細資料，然後再按一下**完成**。  
   - 提供專案名稱和專案位置。
   - 針對 [Project SDK] \(專案 SDK\)，Spark 2.x 叢集請使用 Java 1.8，Spark 1.x 叢集請使用 Java 1.7。
   - 針對 [Spark Version] \(Spark 版本\)，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。 如果 hello spark 叢集的版本低 2.0，請選擇二手 1.x。 否則，您應該選取 Spark2.x。 此範例使用 Spark2.0.2(Scala 2.11.8)。
       ![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. hello Spark 專案會自動為您建立成品。 toosee hello 成品，請遵循下列步驟。

   1. 從 hello**檔案**功能表上，按一下 **專案結構**。
   2. 在 hello**專案結構**對話方塊中，按一下**成品**toosee hello 預設成品所建立。
   ![建立 JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      您也可以建立您自己的成品 bly 按一下 hello  **+** 圖示、 在 hello 圖中反白顯示。

4. 加入程式庫 tooyour 專案。 tooadd 文件庫，在 hello 專案樹狀目錄中的 hello 專案名稱上按一下滑鼠右鍵，然後按一下**開啟模組設定**。 在 hello**專案結構**對話方塊中的，從 hello 左窗格中，按一下**文件庫**，按一下 hello （+） 符號，然後按一下**從 Maven**。

    ![新增程式庫](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    在 hello**從 Maven 儲存機制下載的程式庫**對話方塊方塊中，搜尋並新增下列程式庫的 hello。

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. 複製`yarn-site.xml`和`core-site.xml`hello 從叢集前端節點，並將它 toohello 專案。 使用下列命令 toocopy hello 檔案 hello。 您可以使用[Cygwin](https://cygwin.com/install.html) toorun hello 下列`scp`命令從 hello 叢集 headnodes toocopy hello 檔案。

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    因為我們已加入 hello 叢集前端節點 IP 位址和主機名稱 fo hello hosts 檔案 hello 桌面上，我們可以使用 hello **scp** hello 下列方式中的命令。

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    新增這些檔案 tooyour 專案並將其複製下 hello **/src**資料夾中您專案的樹狀目錄，例如`<your project directory>\src`。
6. 更新 hello `core-site.xml` toomake hello 下列變更。

   1. `core-site.xml`包含加密的 hello hello 叢集相關聯的金鑰 toohello 儲存體帳戶。 在 hello`core-site.xml`您加入 toohello 專案中，取代 hello 加密金鑰與 hello hello 預設儲存體帳戶相關聯的實際儲存體金鑰。 請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. 移除下列項目從 hello hello `core-site.xml`。

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. 儲存 hello 檔案。
7. 加入您的應用程式的 hello 主要類別。 從 hello**專案總管**，以滑鼠右鍵按一下**src**，點太**新增**，然後按一下 **Scala 類別**。

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. 在 hello**建立類別的新 Scala**對話方塊方塊中，提供名稱，如**種類**選取**物件**，然後按一下 **[確定]**。

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. 在 hello`MyClusterAppMain.scala`檔案中，貼上下列程式碼的 hello。 此程式碼會建立 hello Spark 內容，並啟動`executeJob`方法從 hello`SparkSample`物件。

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. 重複步驟 8 和 9 tooadd 呼叫新的 Scala 物件上方`SparkSample`。 toothis 類別新增下列程式碼的 hello。 此程式碼，讀取 hello hello HVAC.csv （可在所有的 HDInsight Spark 叢集上）、 擷取 hello hello hello CSV 中的第七個資料行中只有一個數字的資料列和 hello 會將輸出寫入太**/HVACOut**下 hello 預設hello 叢集的儲存體容器。

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. 重複步驟 8 和 9 以上 tooadd 新的類別稱為 「 `RemoteClusterDebugging`。 這個類別會實作用於偵錯應用程式的 hello Spark 測試架構。 新增下列程式碼 toohello hello`RemoteClusterDebugging`類別。

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     幾個重要事項 toonote 這裡：

   * 如`.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`，請確定 hello Spark 組件 JAR hello 叢集存放裝置 hello 指定路徑上，您可以使用。
   * 如`setJars`，指定將會建立 hello 成品 jar hello 位置。 通常是 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`。
12. 在 hello`RemoteClusterDebugging`類別，以滑鼠右鍵按一下 hello`test`關鍵字，然後選取**建立 RemoteClusterDebugging 組態**。

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. 在 [hello] 對話方塊中，請在提供 hello 組態的名稱，然後選取 hello**測試種類**為**測試名稱**。 對於所有其他值保留預設值，按一下 套用，然後按一下確定。

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. 您現在應該會看到**遠端執行**組態 hello 功能表列中的下拉式清單中。

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>步驟 5： 偵錯模式執行 hello 應用程式
1. 在 IntelliJ 概念專案中，開啟`SparkSample.scala`並建立中斷點 下一步 too'val rdd1'。 在建立中斷點 hello 快顯功能表中選取**列在函式 executeJob**。

    ![新增中斷點](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. 按一下 hello**偵錯執行**按鈕的下一個 toohello**遠端執行**組態下拉式清單 toostart 執行 hello 應用程式。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. 當執行 hello 程式到達 hello 中斷點時，您應該會看到**偵錯工具**hello 下方窗格中的索引標籤。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. 按一下 hello (**+**) 圖示 tooadd 監看式 hello 圖所示。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    此處，因為 hello 應用程式中斷之前 hello 變數`rdd1`使用所建立，我們可以看到什麼是 hello hello 變數中的第一次 5 個資料列此監看式`rdd`。 按 **ENTER**鍵。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    上述的 hello 映像中看到的內容是在執行階段，您可以查詢資料與偵錯的 terrabytes 如何您的應用程式進行時。 例如，在 hello hello 圖所示的輸出，您可以看到該 hello hello 輸出的第一個資料列是標頭。 有鑑於此，您可以修改您應用程式程式碼 tooskip hello 標頭資料列有必要。
5. 您現在可以按一下 hello**繼續程式**圖示 tooproceed 與執行應用程式。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. 如果順利完成 hello 應用程式，您應該會看到類似 hello 下列輸出。

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>示範
* 建立 Scala 專案 (影片)：[建立 Spark Scala 應用程式](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) \(Create Spark Scala Applications\)
* 遠端偵錯 （影片）：[使用 Azure Toolkit for IntelliJ toodebug Spark 應用程式，從遠端在 HDInsight 叢集上](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [在 Azure Toolkit HDInsight Tools 用於 IntelliJ toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
