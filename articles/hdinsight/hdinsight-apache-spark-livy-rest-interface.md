---
title: "使用 Livy Spark 將作業提交至 Azure HDInsight 上的 Spark 叢集 | Microsoft Docs"
description: "了解如何使用 Apache Spark REST API 從遠端將 Spark 作業提交至 Azure HDInsight 叢集。"
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="76200-104">使用 Apache Spark REST API 將遠端作業提交至 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="76200-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="76200-105">了解如何使用可將遠端作業提交至 Azure HDInsight Spark 叢集的 Livy (也就是 Apache Spark REST API)。</span><span class="sxs-lookup"><span data-stu-id="76200-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="76200-106">如需詳細文件，請參閱 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)。</span><span class="sxs-lookup"><span data-stu-id="76200-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="76200-107">您可以使用 Livy 執行互動式 Spark 殼層，或提交要在 Spark 上執行的批次作業。</span><span class="sxs-lookup"><span data-stu-id="76200-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="76200-108">本文將討論如何使用 Livy 提交批次作業。</span><span class="sxs-lookup"><span data-stu-id="76200-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="76200-109">本文中的程式碼片段會使用 cURL 向 Livy Spark 端點發出 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="76200-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="76200-110">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="76200-110">**Prerequisites:**</span></span>

* <span data-ttu-id="76200-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="76200-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="76200-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="76200-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="76200-113">[cURL](http://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="76200-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="76200-114">本文使用 cURL 示範如何對 HDInsight Spark 叢集進行 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="76200-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="76200-115">提交 Livy Spark 批次作業</span><span class="sxs-lookup"><span data-stu-id="76200-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="76200-116">在提交批次作業之前，您必須將應用程式 jar 上傳至與叢集相關聯的叢集儲存體。</span><span class="sxs-lookup"><span data-stu-id="76200-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="76200-117">您可以使用命令列公用程式 [**AzCopy**](../storage/common/storage-use-azcopy.md) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="76200-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="76200-118">此外也有各種用戶端可用來上傳資料。</span><span class="sxs-lookup"><span data-stu-id="76200-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="76200-119">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="76200-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="76200-120">**範例**：</span><span class="sxs-lookup"><span data-stu-id="76200-120">**Examples**:</span></span>

* <span data-ttu-id="76200-121">如果 jar 檔案位於叢集儲存體 (WASB) 上</span><span class="sxs-lookup"><span data-stu-id="76200-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="76200-122">如果您需要在輸入檔案 (在此範例中為 input.txt) 中傳遞 jar 檔案名稱和類別名稱</span><span class="sxs-lookup"><span data-stu-id="76200-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="76200-123">取得在叢集上執行之 Livy Spark 批次的相關資訊</span><span class="sxs-lookup"><span data-stu-id="76200-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="76200-124">**範例**：</span><span class="sxs-lookup"><span data-stu-id="76200-124">**Examples**:</span></span>

* <span data-ttu-id="76200-125">如果您想要擷取在叢集上執行的所有 Livy Spark 批次：</span><span class="sxs-lookup"><span data-stu-id="76200-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="76200-126">如果您想要擷取具有指定批次識別碼的特定批次</span><span class="sxs-lookup"><span data-stu-id="76200-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="76200-127">將 Livy Spark 批次作業刪除</span><span class="sxs-lookup"><span data-stu-id="76200-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="76200-128">**範例**：</span><span class="sxs-lookup"><span data-stu-id="76200-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="76200-129">Livy Spark 與高可用性</span><span class="sxs-lookup"><span data-stu-id="76200-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="76200-130">Livy 可為在叢集上執行的 Spark 作業提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="76200-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="76200-131">以下是一些範例。</span><span class="sxs-lookup"><span data-stu-id="76200-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="76200-132">如果在您從遠端將作業提交給 Spark 叢集之後，Livy 服務當機，作業將會繼續在背景執行。</span><span class="sxs-lookup"><span data-stu-id="76200-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="76200-133">當 Livy 恢復運作時，它會還原作業的狀態並回報。</span><span class="sxs-lookup"><span data-stu-id="76200-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="76200-134">適用於 HDInsight 的 Jupyter Notebook 是由 Livy 在後端提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="76200-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="76200-135">如果在 Notebook 執行 Spark 作業時，Livy 服務重新啟動，Notebook 就會繼續執行程式碼單元。</span><span class="sxs-lookup"><span data-stu-id="76200-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="76200-136">請舉例說明</span><span class="sxs-lookup"><span data-stu-id="76200-136">Show me an example</span></span>
<span data-ttu-id="76200-137">在本節中，我們將透過範例了解如何使用 Livy Spark 來提交批次作業、監視作業的進度，然後加以刪除。</span><span class="sxs-lookup"><span data-stu-id="76200-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="76200-138">我們在此範例中使用的應用程式，就是 [建立獨立 Scala 應用程式，並在 HDInsight Spark 叢集上執行](hdinsight-apache-spark-create-standalone-application.md)一文中所開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="76200-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="76200-139">這裡的步驟假設：</span><span class="sxs-lookup"><span data-stu-id="76200-139">The steps here assume that:</span></span>

* <span data-ttu-id="76200-140">您已將應用程式 jar 複製到與叢集相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="76200-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="76200-141">您已將 CuRL 安裝在要嘗試這些步驟的電腦上。</span><span class="sxs-lookup"><span data-stu-id="76200-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="76200-142">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="76200-142">Perform the following steps:</span></span>

1. <span data-ttu-id="76200-143">我們先確認 Livy Spark 正在叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="76200-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="76200-144">我們可以取得執行中的批次清單，加以確認。</span><span class="sxs-lookup"><span data-stu-id="76200-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="76200-145">如果您是第一次使用 Livy 執行作業，輸出應會傳回零。</span><span class="sxs-lookup"><span data-stu-id="76200-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="76200-146">您應該會看到如下列程式碼片段的輸出：</span><span class="sxs-lookup"><span data-stu-id="76200-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="76200-147">請留意到輸出的最後一行顯示為 **total:0**，這表示沒有執行中的批次。</span><span class="sxs-lookup"><span data-stu-id="76200-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="76200-148">現在，我們要提交批次作業。</span><span class="sxs-lookup"><span data-stu-id="76200-148">Let us now submit a batch job.</span></span> <span data-ttu-id="76200-149">下列程式碼片段會使用輸入檔案 (input.txt) 傳遞 jar 名稱和類別名稱來作為參數。</span><span class="sxs-lookup"><span data-stu-id="76200-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="76200-150">如果您要從 Windows 電腦執行這些步驟，建議您採用輸出檔案這個方法。</span><span class="sxs-lookup"><span data-stu-id="76200-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="76200-151">檔案 **input.txt** 中的參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="76200-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="76200-152">您應該會看到如下列程式碼片段的輸出：</span><span class="sxs-lookup"><span data-stu-id="76200-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="76200-153">請留意到輸出的最後一行顯示為 **state:starting**。</span><span class="sxs-lookup"><span data-stu-id="76200-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="76200-154">此外也顯示 **id:0**。</span><span class="sxs-lookup"><span data-stu-id="76200-154">It also says, **id:0**.</span></span> <span data-ttu-id="76200-155">在這裡，批次識別碼是 **0**。</span><span class="sxs-lookup"><span data-stu-id="76200-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="76200-156">現在，您可以使用批次識別碼來擷取此批次的狀態。</span><span class="sxs-lookup"><span data-stu-id="76200-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="76200-157">您應該會看到如下列程式碼片段的輸出：</span><span class="sxs-lookup"><span data-stu-id="76200-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="76200-158">輸出此時顯示 **state:success**，這表示作業已順利完成。</span><span class="sxs-lookup"><span data-stu-id="76200-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="76200-159">現在，您可以視需要刪除批次。</span><span class="sxs-lookup"><span data-stu-id="76200-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="76200-160">您應該會看到如下列程式碼片段的輸出：</span><span class="sxs-lookup"><span data-stu-id="76200-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="76200-161">輸出的最後一行顯示批次已成功刪除。</span><span class="sxs-lookup"><span data-stu-id="76200-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="76200-162">當作業執行時將它刪除，也會清除作業。</span><span class="sxs-lookup"><span data-stu-id="76200-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="76200-163">如果您刪除已完成的作業，無論成功與否，這將會完全刪除作業資訊。</span><span class="sxs-lookup"><span data-stu-id="76200-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="76200-164">在 HDInsight 3.5 叢集上使用 Livy Spark</span><span class="sxs-lookup"><span data-stu-id="76200-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="76200-165">根據預設，HDInsight 3.5 叢集會停用使用本機檔案路徑，以存取範本資料檔案或 jar。</span><span class="sxs-lookup"><span data-stu-id="76200-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="76200-166">建議您使用 `wasb://` 路徑，而不是從叢集存取 jar 或範本資料檔案。</span><span class="sxs-lookup"><span data-stu-id="76200-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="76200-167">如果您確定要使用本機路徑，您就必須同時更新 Ambari 組態。</span><span class="sxs-lookup"><span data-stu-id="76200-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="76200-168">若要這樣做：</span><span class="sxs-lookup"><span data-stu-id="76200-168">To do so:</span></span>

1. <span data-ttu-id="76200-169">移至叢集的 Ambari 入口網站。</span><span class="sxs-lookup"><span data-stu-id="76200-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="76200-170">Ambari Web UI 位在您的 HDInsight 叢集的 https://**CLUSTERNAME**.azurehdidnsight.net，其中 CLUSTERNAME 是您的叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="76200-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="76200-171">在左側導覽中，按一下 [Livy]，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="76200-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="76200-172">在 [livy-default] 底下新增屬性名稱 `livy.file.local-dir-whitelist`，如果您想要允許存取整個檔案系統，可將其值設為 **"/"**。</span><span class="sxs-lookup"><span data-stu-id="76200-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="76200-173">如果您只想要允許存取特定目錄，請將值設為該目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="76200-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="76200-174">在 Azure 虛擬網路內提交叢集的 Livy 作業</span><span class="sxs-lookup"><span data-stu-id="76200-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="76200-175">如果您是從 Azure 虛擬網路內連線到 HDInsight Spark 叢集，可以直接連線到叢集上的 Livy。</span><span class="sxs-lookup"><span data-stu-id="76200-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="76200-176">在此案例中，Livy 端點的 URL 是 `http://<IP address of the headnode>:8998/batches`。</span><span class="sxs-lookup"><span data-stu-id="76200-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="76200-177">在這裡，**8998** 是 Livy 在叢集前端節點上執行的連接埠。</span><span class="sxs-lookup"><span data-stu-id="76200-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="76200-178">如需有關在非公用連接埠上存取服務的詳細資訊，請參閱 [HDInsight 上 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="76200-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="76200-179">疑難排解</span><span class="sxs-lookup"><span data-stu-id="76200-179">Troubleshooting</span></span>

<span data-ttu-id="76200-180">以下是一些使用 Livy 進行對 Spark 叢集的遠端作業提交時可能遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="76200-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="76200-181">不支援從其他儲存體使用外部 jar</span><span class="sxs-lookup"><span data-stu-id="76200-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="76200-182">**問題︰**如果您的 Livy Spark 作業是參考與叢集相關聯的其他儲存體帳戶之外部 jar，則作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="76200-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="76200-183">**解決方式︰**請確定您想要使用的 jar 位於與 HDInsight 叢集相關聯的預設儲存體中。</span><span class="sxs-lookup"><span data-stu-id="76200-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="76200-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76200-184">Next step</span></span>

* [<span data-ttu-id="76200-185">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="76200-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="76200-186">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="76200-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

