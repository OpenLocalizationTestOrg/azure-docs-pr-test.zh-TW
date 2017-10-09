---
title: "aaaUse 晚總 Spark toosubmit 作業 tooSpark 叢集 Azure HDInsight 上的 |Microsoft 文件"
description: "了解如何 toouse Apache Spark REST API toosubmit Spark 遠端作業 tooan Azure HDInsight 叢集。"
keywords: apache spark rest api, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>使用 Apache Spark REST API toosubmit 遠端作業 tooan HDInsight Spark 叢集

了解如何 toouse 晚總，hello Apache Spark REST API，也就是使用的 toosubmit 遠端作業 tooan Azure HDInsight Spark 叢集。 如需詳細文件，請參閱 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)。

您可以使用晚總 toorun 互動式 Spark 殼層或提交批次作業 toobe Spark 上執行。 這篇文章討論有關使用晚總 toosubmit 批次作業。 本文章中的 hello 程式碼片段使用 cURL toomake REST API 呼叫 toohello 晚總 Spark 端點。

**先決條件：**

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

* [cURL](http://curl.haxx.se/)。 本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 HDInsight Spark 叢集。

## <a name="submit-a-livy-spark-batch-job"></a>提交 Livy Spark 批次作業
提交批次作業之前，您必須上傳 hello hello 與 hello 叢集相關聯的叢集存放裝置上的應用程式 jar。 您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式、 toodo 如此。 沒有您可以使用 tooupload 資料的其他各種用戶端。 您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**範例**：

* 如果 hello jar 檔案是在 hello 叢集儲存體 (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* 如果您希望 toopass hello jar 檔名和 hello 做為輸入檔的一部分的類別名稱 (在此範例中，input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>取得有關晚總 Spark hello 叢集上執行的批次
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**範例**：

* 如果您想 tooretrieve hello 叢集上執行的所有 hello 晚總 Spark 批次：
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* 如果您想 tooretrieve 具有指定的批次識別碼的特定批次
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>將 Livy Spark 批次作業刪除
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**範例**：

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark 與高可用性
晚總 Spark hello 叢集上執行的工作提供高可用性。 以下是一些範例。

* 如果 hello 晚總服務從遠端送出作業之後關閉 tooa Spark 叢集，hello 作業會繼續 toorun hello 背景執行。 備份晚總時，它會還原 hello 工作和報表回 hello 狀態。
* Hdinsight Jupyter 筆記本會由晚總供電 hello 後端中。 如果筆記本執行 Spark 作業，而且 hello 晚總服務取得重新啟動，hello 筆記本會繼續 toorun hello 程式碼的儲存格。 

## <a name="show-me-an-example"></a>請舉例說明
本節中，我們可以查看範例 toouse 晚總 Spark toosubmit 批次工作、 監視 hello hello 作業進度，則請予以刪除。 hello 我們在此範例中使用的應用程式為的 hello hello 文件中開發的其中一個[HDInsight Spark 叢集上建立獨立 Scala 應用程式和 toorun](hdinsight-apache-spark-create-standalone-application.md)。 此處 hello 步驟假設：

* 您已經複製了 hello 應用程式 jar toohello 儲存體帳戶與 hello 叢集相關聯。
* 您有 CuRL hello 嘗試這些步驟的電腦上安裝。

執行下列步驟的 hello:

1. 讓我們先確認晚總 Spark hello 叢集上正在執行。 我們可以取得執行中的批次清單，加以確認。 如果您正在使用晚總 hello 第一次作業，hello 輸出應該會傳回零。
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    您應該取得輸出類似 toohello 下列程式碼片段：
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    請注意如何 hello hello 輸出中的最後一行顯示**總數： 0**，它會建議任何執行中批次。

2. 現在，我們要提交批次作業。 下列程式碼片段的 hello 使用輸入的檔 (input.txt) toopass hello jar 名稱與 hello 類別名稱做為參數。 如果您從 Windows 電腦執行下列步驟，使用的輸入的檔是 hello 建議的方法。
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    hello hello 檔案中的參數**input.txt**的定義方式如下：
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    您應該會看到下列程式碼片段的輸出類似 toohello:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    請注意如何 hello hello 輸出最後一行顯示**狀態： 啟動**。 此外也顯示 **id:0**。 在這裡， **0** hello 批次識別碼。

3. 您現在可以擷取使用 hello 批次識別碼。 這個特定批次 hello 狀態
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    您應該會看到下列程式碼片段的輸出類似 toohello:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    hello 輸出現在會顯示**狀態： 成功**，它會建議 hello 工作已順利完成。

4. 如果您想，您現在可以刪除 hello 批次。
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    您應該會看到下列程式碼片段的輸出類似 toohello:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    hello hello 輸出最後一行顯示該 hello 批次已成功刪除。 刪除工作，當它執行時，也會清除 hello 作業。 如果您刪除工作已完成、 成功或失敗，它會完全刪除 hello 作業資訊。

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>在 HDInsight 3.5 叢集上使用 Livy Spark

HDInsight 3.5 叢集，預設會停用使用本機檔案路徑 tooaccess 範例資料檔或 （每瓶）。 我們鼓勵您 toouse hello`wasb://`路徑而 tooaccess （每瓶） 範例資料檔案或從 hello 叢集。 如果您想 toouse 本機路徑，則必須跟著更新 hello Ambari 組態。 toodo 因此：

1. 請為 hello 叢集 toohello Ambari 入口網站。 hello Ambari Web UI 並用於您的 HDInsight 叢集在 https://**CLUSTERNAME**。 azurehdidnsight.net，CLUSTERNAME 所在 hello 叢集的名稱。

2. 在左瀏覽 hello，按一下**晚總**，然後按一下 **Configs**。

3. 在下**晚總預設**新增 hello 屬性名稱`livy.file.local-dir-whitelist`並設定它的值太**"/"**如果您希望 tooallow 完整存取 toofile 系統。 如果您想要 tooallow 存取只有 tooa 特定目錄，提供 hello 路徑 toothat 目錄做為 hello 值。

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>在 Azure 虛擬網路內提交叢集的 Livy 作業

如果您連接 tooan 從 Azure 虛擬網路內的 HDInsight Spark 叢集，您可以直接連接 tooLivy hello 叢集上。 在這種情況下，hello URL 晚總端點是`http://<IP address of hello headnode>:8998/batches`。 在這裡， **8998**是 hello 叢集前端節點執行所在晚總 hello 連接埠。 如需有關在非公用連接埠上存取服務的詳細資訊，請參閱 [HDInsight 上 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)。

## <a name="troubleshooting"></a>疑難排解

以下是在遠端工作提交 tooSpark 叢集使用晚總時可能會遇到一些問題。

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>不支援使用外部 jar 從 hello 額外的存放裝置

**問題：**晚總 Spark 作業參考外部 jar 從 hello 與 hello 叢集相關聯的額外的儲存體帳戶時，如果 hello 作業就會失敗。

**解決方式：**請確定您想要 toouse 可在 hello 與 hello HDInsight 叢集相關聯的預設儲存體中的 hello jar。





## <a name="next-step"></a>後續步驟

* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

