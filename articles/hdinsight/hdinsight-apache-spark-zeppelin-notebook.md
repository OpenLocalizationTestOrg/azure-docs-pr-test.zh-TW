---
title: "在 Azure HDInsight 叢集化使用 Apache Spark aaaUse 運貨用飛艇筆記本 |Microsoft 文件"
description: "使用 Apache Spark toouse 運貨用飛艇筆記本 Azure HDInsight 上的叢集的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>在 Azure HDInsight 上搭配使用 Zeppelin Notebook 和 Apache Spark 叢集

HDInsight Spark 叢集包含運貨用飛艇筆記本，您可以使用 toorun Spark 作業。 在本文中，您學會如何 toouse hello 運貨用飛艇筆記本在 HDInsight 叢集上。

> [!NOTE]
> Zeppelin Notebook 僅適用於 HDInsight 3.5 上的 Spark 1.6.3 以及 HDInsight 3.6 上的 Spark 2.1.0。
>

**先決條件：**

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="launch-a-zeppelin-notebook"></a>啟動 Zeppelin Notebook
1. 從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下**運貨用飛艇筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。
   
   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello 運貨用飛艇筆記型電腦。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. 建立新的 Notebook。 從 hello 標頭窗格中，按一下 **筆記本**，然後按一下**建立新便箋**。
   
    ![建立新的 Zeppelin Notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "建立新的 Zeppelin Notebook")
   
    輸入 hello 筆記本的名稱，然後按一下**建立注意**。
3. 此外，請確定 hello 筆記本標頭會顯示已連線的狀態。 它是由綠點 hello 右上角中表示。
   
    ![Zeppelin Notebook 狀態](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 狀態")
4. 將範例資料載入暫存資料表。 當您建立 HDInsight，hello 範例資料檔中的 Spark 叢集**hvac.csv**，是儲存體帳戶相關聯的複製的 toohello **\HdiSamples\SensorSampleData\hvac**。
   
    在 hello 空白段落所建立的預設 hello 新筆記本中，貼上下列程式碼片段的 hello。
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    按**SHIFT + ENTER**或按一下 hello**播放**hello 段落 toorun hello 程式碼片段的按鈕。 hello 右上角的 hello 段落的 hello 狀態應該從好時，暫止、 正在執行 tooFINISHED 進度。 在 hello hello 底部顯示 hello 輸出相同的 paragraph。 hello 螢幕擷取畫面看起來像下列 hello:
   
    ![從未經處理資料建立暫存資料表](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "從未經處理資料建立暫存資料表")
   
    您也可以提供標題 tooeach 段落。 從 hello 右上角，按一下 hello**設定**圖示，然後再按一下**顯示標題**。
5. 您現在可以執行 Spark SQL 陳述式上 hello **hvac**資料表。 貼上下列查詢在新的段落中的 hello。 hello 查詢會擷取 hello 建置識別碼和 hello hello 目標與實際溫度的每個建置在特定日期之間的差異。 按下 **SHIFT + ENTER**。
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    hello **%sql** hello 開頭的陳述式會告知 hello 筆記本 toouse hello 晚總 Scala 直譯器。
   
    hello 下列螢幕擷取畫面顯示 hello 輸出。
   
    ![執行使用 hello 筆記本的 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "執行使用 hello 筆記本的 Spark SQL 陳述式")
   
     按一下 hello 顯示選項 （反白顯示在矩形） tooswitch hello 不同表示之間相同的輸出。 按一下**設定**toochoose 哪些 consitutes hello 索引鍵和 hello 輸出中的值。 hello 使用上面的螢幕擷取**buildingID**作為 hello 索引鍵和 hello 平均**temp_diff** hello 值。
6. 您也可以執行在 hello 查詢中使用變數的 Spark SQL 陳述式。 hello 下一步的程式碼片段說明如何 toodefine 變數， **Temp**，要與 tooquery hello hello 可能值的查詢中。 當您第一次執行 hello 查詢時，下拉式清單會自動填入 hello hello 變數您指定的值。
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    將此程式碼片段貼到新的段落中，然後按下 **SHIFT + ENTER**。 hello 下列螢幕擷取畫面顯示 hello 輸出。
   
    ![執行使用 hello 筆記本的 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "執行使用 hello 筆記本的 Spark SQL 陳述式")
   
    對於後續的查詢，您可以從 hello 下拉式清單中選取新的值，然後再次執行 hello 查詢。 按一下**設定**toochoose 哪些 consitutes hello 索引鍵和 hello 輸出中的值。 hello 使用上面的螢幕擷取**buildingID** hello 索引鍵，hello 平均**temp_diff** hello 值和**targettemp**為 hello 群組。
7. 重新啟動 hello 晚總直譯器 tooexit hello 應用程式。 toodo，開啟即可 hello 登入使用者名稱，從 hello 右上角的 解譯器設定，然後按一下**直譯器**。
   
    ![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")
8. 捲動 tooLivy 直譯器設定，然後按一下**重新啟動**。
   
    ![重新啟動 hello 晚總 intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 運貨用飛艇 intepreter 重新啟動")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>如何使用與 hello 筆記本的外部封裝？
您可以設定 hello 運貨用飛艇筆記本 HDInsight (Linux) toouse 外部、 社群貢獻的套件不包含--現成的 hello 叢集中的 Apache Spark 叢集中。 您可以搜尋 hello [Maven 儲存機制](http://search.maven.org/)如 hello 的封裝所提供的完整清單。 您也可以從其他來源取得可用套件清單。 例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。

在本文中，您會看到如何 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)與 hello Jupyter 筆記本的封裝。

1. 開啟解譯器設定。 從 hello 右上角，按一下 hello 登入使用者名稱，然後按一下**直譯器**。
   
    ![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")
2. 捲動 tooLivy 直譯器設定，然後按一下**編輯**。
   
    ![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "變更解譯器設定")
3. 加入新機碼，呼叫**livy.spark.jars.packages**並設定其值格式 hello `group:id:version`。 因此，如果您想要 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)封裝時，您必須設定 hello hello 機碼值太`com.databricks:spark-csv_2.10:1.4.0`。
   
    ![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "變更解譯器設定")
   
    按一下**儲存**然後重新啟動 hello 晚總直譯器。
4. **提示**： 如果您想的 toounderstand tooarrive hello hello 機碼值在這裡的上方輸入的方式如何。
   
    a. 在 hello Maven 儲存機制中，找出 hello 封裝。 針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。
   
    b. 從 hello 儲存機制，蒐集 hello 值**GroupId**， **ArtifactId**，和**版本**。
   
    ![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")
   
    c. 串連 hello 三個值，並以分號 (**:**)。
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>在哪裡？ hello 運貨用飛艇筆記本儲存
hello 運貨用飛艇筆記本會儲存 toohello 叢集 headnodes。 因此，如果您刪除 hello 叢集時，會一併刪除 hello 筆記型電腦。 如果您想 toopreserve 您筆記本供稍後使用其他叢集上，您必須將它們匯出您完成執行後，hello 作業。 tooexport 筆記本中，按一下 hello**匯出**圖示 hello 圖所示。

![下載筆記本](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "下載 hello 筆記本")

這可以節省 hello 筆記本作為下載位置在 JSON 檔案。

## <a name="livy-session-management"></a>Livy 工作階段管理
當您執行第一個程式碼段落 hello 運貨用飛艇筆記本中時，HDInsight Spark 叢集中建立新的晚總工作階段。 此工作階段可供您後續建立的所有 Zeppelin Notebook 共用。 如果某些原因 hello 晚總工作階段已終止 （叢集重新開機等），您將無法從 hello 運貨用飛艇筆記本能夠 toorun 作業。

在這種情況下，您必須執行下列步驟，才能開始執行作業從運貨用飛艇筆記本 hello。 

1. 重新啟動 hello 從 hello 運貨用飛艇筆記本晚總直譯器。 toodo，開啟即可 hello 登入使用者名稱，從 hello 右上角的 解譯器設定，然後按一下**直譯器**。
   
    ![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")
2. 捲動 tooLivy 直譯器設定，然後按一下**重新啟動**。
   
    ![重新啟動 hello 晚總 intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 運貨用飛艇 intepreter 重新啟動")
3. 從現有的 Zeppelin Notebook 執行程式碼單元。 這會建立新的工作階段晚總 hello HDInsight 叢集。

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
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
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







