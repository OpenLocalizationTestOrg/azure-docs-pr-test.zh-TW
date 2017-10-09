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
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="19446-104">使用 Apache Spark REST API toosubmit 遠端作業 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="19446-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="19446-105">了解如何 toouse 晚總，hello Apache Spark REST API，也就是使用的 toosubmit 遠端作業 tooan Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="19446-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="19446-106">如需詳細文件，請參閱 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)。</span><span class="sxs-lookup"><span data-stu-id="19446-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="19446-107">您可以使用晚總 toorun 互動式 Spark 殼層或提交批次作業 toobe Spark 上執行。</span><span class="sxs-lookup"><span data-stu-id="19446-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="19446-108">這篇文章討論有關使用晚總 toosubmit 批次作業。</span><span class="sxs-lookup"><span data-stu-id="19446-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="19446-109">本文章中的 hello 程式碼片段使用 cURL toomake REST API 呼叫 toohello 晚總 Spark 端點。</span><span class="sxs-lookup"><span data-stu-id="19446-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="19446-110">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="19446-110">**Prerequisites:**</span></span>

* <span data-ttu-id="19446-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="19446-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="19446-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="19446-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="19446-113">[cURL](http://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="19446-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="19446-114">本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="19446-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="19446-115">提交 Livy Spark 批次作業</span><span class="sxs-lookup"><span data-stu-id="19446-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="19446-116">提交批次作業之前，您必須上傳 hello hello 與 hello 叢集相關聯的叢集存放裝置上的應用程式 jar。</span><span class="sxs-lookup"><span data-stu-id="19446-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="19446-117">您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式、 toodo 如此。</span><span class="sxs-lookup"><span data-stu-id="19446-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="19446-118">沒有您可以使用 tooupload 資料的其他各種用戶端。</span><span class="sxs-lookup"><span data-stu-id="19446-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="19446-119">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="19446-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="19446-120">**範例**：</span><span class="sxs-lookup"><span data-stu-id="19446-120">**Examples**:</span></span>

* <span data-ttu-id="19446-121">如果 hello jar 檔案是在 hello 叢集儲存體 (WASB)</span><span class="sxs-lookup"><span data-stu-id="19446-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="19446-122">如果您希望 toopass hello jar 檔名和 hello 做為輸入檔的一部分的類別名稱 (在此範例中，input.txt)</span><span class="sxs-lookup"><span data-stu-id="19446-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="19446-123">取得有關晚總 Spark hello 叢集上執行的批次</span><span class="sxs-lookup"><span data-stu-id="19446-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="19446-124">**範例**：</span><span class="sxs-lookup"><span data-stu-id="19446-124">**Examples**:</span></span>

* <span data-ttu-id="19446-125">如果您想 tooretrieve hello 叢集上執行的所有 hello 晚總 Spark 批次：</span><span class="sxs-lookup"><span data-stu-id="19446-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="19446-126">如果您想 tooretrieve 具有指定的批次識別碼的特定批次</span><span class="sxs-lookup"><span data-stu-id="19446-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="19446-127">將 Livy Spark 批次作業刪除</span><span class="sxs-lookup"><span data-stu-id="19446-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="19446-128">**範例**：</span><span class="sxs-lookup"><span data-stu-id="19446-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="19446-129">Livy Spark 與高可用性</span><span class="sxs-lookup"><span data-stu-id="19446-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="19446-130">晚總 Spark hello 叢集上執行的工作提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="19446-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="19446-131">以下是一些範例。</span><span class="sxs-lookup"><span data-stu-id="19446-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="19446-132">如果 hello 晚總服務從遠端送出作業之後關閉 tooa Spark 叢集，hello 作業會繼續 toorun hello 背景執行。</span><span class="sxs-lookup"><span data-stu-id="19446-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="19446-133">備份晚總時，它會還原 hello 工作和報表回 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="19446-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="19446-134">Hdinsight Jupyter 筆記本會由晚總供電 hello 後端中。</span><span class="sxs-lookup"><span data-stu-id="19446-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="19446-135">如果筆記本執行 Spark 作業，而且 hello 晚總服務取得重新啟動，hello 筆記本會繼續 toorun hello 程式碼的儲存格。</span><span class="sxs-lookup"><span data-stu-id="19446-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="19446-136">請舉例說明</span><span class="sxs-lookup"><span data-stu-id="19446-136">Show me an example</span></span>
<span data-ttu-id="19446-137">本節中，我們可以查看範例 toouse 晚總 Spark toosubmit 批次工作、 監視 hello hello 作業進度，則請予以刪除。</span><span class="sxs-lookup"><span data-stu-id="19446-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="19446-138">hello 我們在此範例中使用的應用程式為的 hello hello 文件中開發的其中一個[HDInsight Spark 叢集上建立獨立 Scala 應用程式和 toorun](hdinsight-apache-spark-create-standalone-application.md)。</span><span class="sxs-lookup"><span data-stu-id="19446-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="19446-139">此處 hello 步驟假設：</span><span class="sxs-lookup"><span data-stu-id="19446-139">hello steps here assume that:</span></span>

* <span data-ttu-id="19446-140">您已經複製了 hello 應用程式 jar toohello 儲存體帳戶與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="19446-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="19446-141">您有 CuRL hello 嘗試這些步驟的電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="19446-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="19446-142">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="19446-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="19446-143">讓我們先確認晚總 Spark hello 叢集上正在執行。</span><span class="sxs-lookup"><span data-stu-id="19446-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="19446-144">我們可以取得執行中的批次清單，加以確認。</span><span class="sxs-lookup"><span data-stu-id="19446-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="19446-145">如果您正在使用晚總 hello 第一次作業，hello 輸出應該會傳回零。</span><span class="sxs-lookup"><span data-stu-id="19446-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="19446-146">您應該取得輸出類似 toohello 下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="19446-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="19446-147">請注意如何 hello hello 輸出中的最後一行顯示**總數： 0**，它會建議任何執行中批次。</span><span class="sxs-lookup"><span data-stu-id="19446-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="19446-148">現在，我們要提交批次作業。</span><span class="sxs-lookup"><span data-stu-id="19446-148">Let us now submit a batch job.</span></span> <span data-ttu-id="19446-149">下列程式碼片段的 hello 使用輸入的檔 (input.txt) toopass hello jar 名稱與 hello 類別名稱做為參數。</span><span class="sxs-lookup"><span data-stu-id="19446-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="19446-150">如果您從 Windows 電腦執行下列步驟，使用的輸入的檔是 hello 建議的方法。</span><span class="sxs-lookup"><span data-stu-id="19446-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="19446-151">hello hello 檔案中的參數**input.txt**的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="19446-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="19446-152">您應該會看到下列程式碼片段的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="19446-152">You should see an output similar toohello  following snippet:</span></span>
   
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
   
    <span data-ttu-id="19446-153">請注意如何 hello hello 輸出最後一行顯示**狀態： 啟動**。</span><span class="sxs-lookup"><span data-stu-id="19446-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="19446-154">此外也顯示 **id:0**。</span><span class="sxs-lookup"><span data-stu-id="19446-154">It also says, **id:0**.</span></span> <span data-ttu-id="19446-155">在這裡， **0** hello 批次識別碼。</span><span class="sxs-lookup"><span data-stu-id="19446-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="19446-156">您現在可以擷取使用 hello 批次識別碼。 這個特定批次 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="19446-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="19446-157">您應該會看到下列程式碼片段的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="19446-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="19446-158">hello 輸出現在會顯示**狀態： 成功**，它會建議 hello 工作已順利完成。</span><span class="sxs-lookup"><span data-stu-id="19446-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="19446-159">如果您想，您現在可以刪除 hello 批次。</span><span class="sxs-lookup"><span data-stu-id="19446-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="19446-160">您應該會看到下列程式碼片段的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="19446-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="19446-161">hello hello 輸出最後一行顯示該 hello 批次已成功刪除。</span><span class="sxs-lookup"><span data-stu-id="19446-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="19446-162">刪除工作，當它執行時，也會清除 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="19446-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="19446-163">如果您刪除工作已完成、 成功或失敗，它會完全刪除 hello 作業資訊。</span><span class="sxs-lookup"><span data-stu-id="19446-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="19446-164">在 HDInsight 3.5 叢集上使用 Livy Spark</span><span class="sxs-lookup"><span data-stu-id="19446-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="19446-165">HDInsight 3.5 叢集，預設會停用使用本機檔案路徑 tooaccess 範例資料檔或 （每瓶）。</span><span class="sxs-lookup"><span data-stu-id="19446-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="19446-166">我們鼓勵您 toouse hello`wasb://`路徑而 tooaccess （每瓶） 範例資料檔案或從 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="19446-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="19446-167">如果您想 toouse 本機路徑，則必須跟著更新 hello Ambari 組態。</span><span class="sxs-lookup"><span data-stu-id="19446-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="19446-168">toodo 因此：</span><span class="sxs-lookup"><span data-stu-id="19446-168">toodo so:</span></span>

1. <span data-ttu-id="19446-169">請為 hello 叢集 toohello Ambari 入口網站。</span><span class="sxs-lookup"><span data-stu-id="19446-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="19446-170">hello Ambari Web UI 並用於您的 HDInsight 叢集在 https://**CLUSTERNAME**。 azurehdidnsight.net，CLUSTERNAME 所在 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="19446-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="19446-171">在左瀏覽 hello，按一下**晚總**，然後按一下 **Configs**。</span><span class="sxs-lookup"><span data-stu-id="19446-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="19446-172">在下**晚總預設**新增 hello 屬性名稱`livy.file.local-dir-whitelist`並設定它的值太**"/"**如果您希望 tooallow 完整存取 toofile 系統。</span><span class="sxs-lookup"><span data-stu-id="19446-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="19446-173">如果您想要 tooallow 存取只有 tooa 特定目錄，提供 hello 路徑 toothat 目錄做為 hello 值。</span><span class="sxs-lookup"><span data-stu-id="19446-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="19446-174">在 Azure 虛擬網路內提交叢集的 Livy 作業</span><span class="sxs-lookup"><span data-stu-id="19446-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="19446-175">如果您連接 tooan 從 Azure 虛擬網路內的 HDInsight Spark 叢集，您可以直接連接 tooLivy hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="19446-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="19446-176">在這種情況下，hello URL 晚總端點是`http://<IP address of hello headnode>:8998/batches`。</span><span class="sxs-lookup"><span data-stu-id="19446-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="19446-177">在這裡， **8998**是 hello 叢集前端節點執行所在晚總 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="19446-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="19446-178">如需有關在非公用連接埠上存取服務的詳細資訊，請參閱 [HDInsight 上 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="19446-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="19446-179">疑難排解</span><span class="sxs-lookup"><span data-stu-id="19446-179">Troubleshooting</span></span>

<span data-ttu-id="19446-180">以下是在遠端工作提交 tooSpark 叢集使用晚總時可能會遇到一些問題。</span><span class="sxs-lookup"><span data-stu-id="19446-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="19446-181">不支援使用外部 jar 從 hello 額外的存放裝置</span><span class="sxs-lookup"><span data-stu-id="19446-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="19446-182">**問題：**晚總 Spark 作業參考外部 jar 從 hello 與 hello 叢集相關聯的額外的儲存體帳戶時，如果 hello 作業就會失敗。</span><span class="sxs-lookup"><span data-stu-id="19446-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="19446-183">**解決方式：**請確定您想要 toouse 可在 hello 與 hello HDInsight 叢集相關聯的預設儲存體中的 hello jar。</span><span class="sxs-lookup"><span data-stu-id="19446-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="19446-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19446-184">Next step</span></span>

* [<span data-ttu-id="19446-185">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="19446-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="19446-186">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="19446-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

