---
title: "使用 Hadoop 資料流活動轉換資料 - Azure | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 中的 Hadoop 資料流活動，以在隨選/您自己的 HDInsight 叢集上執行 Hadoop 資料流程式來轉換資料。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="b7371-103">使用 Azure Data Factory 中的 Hadoop 資料流活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="b7371-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b7371-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b7371-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b7371-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b7371-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="b7371-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b7371-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b7371-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="b7371-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b7371-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="b7371-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b7371-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="b7371-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b7371-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b7371-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="b7371-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b7371-114">您可以使用 HDInsightStreamingActivity 活動從 Azure Data Factory 管線叫用 Hadoop 串流工作。</span><span class="sxs-lookup"><span data-stu-id="b7371-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="b7371-115">下列 JSON 片段會示範在管線 JSON 檔案中使用 HDInsightStreamingActivity 的語法。</span><span class="sxs-lookup"><span data-stu-id="b7371-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="b7371-116">Data Factory [管線](data-factory-create-pipelines.md)中的 HDInsight 串流活動會在[您自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨選](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)的 Windows/Linux 架構 HDInsight 叢集上執行 Hadoop 串流程式。</span><span class="sxs-lookup"><span data-stu-id="b7371-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b7371-117">本文是根據 [資料轉換活動](data-factory-data-transformation-activities.md) 一文，它呈現資料轉換和支援的轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="b7371-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="b7371-118">如果您是 Azure Data Factory 的新手，請在閱讀本文章之前閱讀 [Azure Data Factory 簡介](data-factory-introduction.md)，以及研習教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="b7371-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="b7371-119">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="b7371-119">JSON sample</span></span>
<span data-ttu-id="b7371-120">HDInsight 叢集會使用範例程式 (wc.exe 和 cat.exe) 和資料 (將 davinci.txt) 自動填入。</span><span class="sxs-lookup"><span data-stu-id="b7371-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b7371-121">根據預設，HDInsight 叢集所使用的容器名稱是叢集本身的名稱。</span><span class="sxs-lookup"><span data-stu-id="b7371-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="b7371-122">例如，如果您的叢集名稱是 myhdicluster，相關聯的 Blob 容器名稱為 myhdicluster。</span><span class="sxs-lookup"><span data-stu-id="b7371-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="b7371-123">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="b7371-123">Note the following points:</span></span>

1. <span data-ttu-id="b7371-124">將連結服務的名稱設定為 **linkedServiceName** ，該服務指向您的 HDInsight 叢集，串流 mapreduce 作業會在該叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="b7371-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="b7371-125">將活動的類型設為 **HDInsightStreaming**。</span><span class="sxs-lookup"><span data-stu-id="b7371-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="b7371-126">針對 **mapper** 屬性，指定對應程式可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="b7371-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="b7371-127">在範例中，cat.exe 是對應程式可執行檔。</span><span class="sxs-lookup"><span data-stu-id="b7371-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="b7371-128">針對 **reducer** 屬性，指定減壓器可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="b7371-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="b7371-129">在範例中，cat.exe 是減壓器可執行檔。</span><span class="sxs-lookup"><span data-stu-id="b7371-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="b7371-130">針對 **input** 類型屬性，指定對應程式的輸入檔 (包括位置)。</span><span class="sxs-lookup"><span data-stu-id="b7371-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="b7371-131">在 "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt" 範例中：adfsample 是 blob 容器，example/data/Gutenberg 是資料夾，而 davinci.txt 是 blob。</span><span class="sxs-lookup"><span data-stu-id="b7371-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="b7371-132">針對 **output** 類型屬性，指定減壓器的輸出檔 (包括位置)。</span><span class="sxs-lookup"><span data-stu-id="b7371-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="b7371-133">Hadoop 串流作業的輸出會寫入針對這個屬性指定的位置。</span><span class="sxs-lookup"><span data-stu-id="b7371-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="b7371-134">在 **filePaths** 區段中，指定對應程式和減壓器可執行檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="b7371-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="b7371-135">在 "adfsample/example/apps/wc.exe" 範例中，adfsample 是 blob 容器，example/apps 是資料夾，而 wc.exe 是可執行檔。</span><span class="sxs-lookup"><span data-stu-id="b7371-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="b7371-136">針對 **fileLinkedService** 屬性，指定代表 Azure 儲存體 (包含 filePaths 區段中指定的檔案) 的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="b7371-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="b7371-137">針對 **arguments** 屬性，指定串流工作的引數。</span><span class="sxs-lookup"><span data-stu-id="b7371-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="b7371-138">**getDebugInfo** 屬性是選擇性的元素。</span><span class="sxs-lookup"><span data-stu-id="b7371-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="b7371-139">該屬性設定為 [失敗] 時，只能在執行失敗時下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b7371-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="b7371-140">當其設定為「永遠」時，無論執行狀態為何，一律下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b7371-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="b7371-141">如範例所示，您必須為 Hadoop 串流活動的 **outputs** 屬性指定輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="b7371-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="b7371-142">這個資料集只是一個驅動管線排程所需的虛設資料集。</span><span class="sxs-lookup"><span data-stu-id="b7371-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="b7371-143">您不需要為活動的 **input** 屬性指定任何輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="b7371-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="b7371-144">範例</span><span class="sxs-lookup"><span data-stu-id="b7371-144">Example</span></span>
<span data-ttu-id="b7371-145">本逐步解說中的管線會在 Azure HDInsight 叢集上執行字數統計串流 Map/Reduce 程式。</span><span class="sxs-lookup"><span data-stu-id="b7371-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="b7371-146">連結的服務</span><span class="sxs-lookup"><span data-stu-id="b7371-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b7371-147">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="b7371-147">Azure Storage linked service</span></span>
<span data-ttu-id="b7371-148">首先，建立連結的服務，將 Azure HDInsight 叢集使用的 Azure 儲存體連結到  Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b7371-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="b7371-149">如果您複製/貼上下列程式碼，請記得使用 Azure 儲存體的名稱和金鑰來取代帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7371-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="b7371-150">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="b7371-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="b7371-151">接著，建立連結的服務，將 Azure HDInsight 叢集連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b7371-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="b7371-152">如果您複製/貼上下列程式碼，請使用您的 HDInsight 叢集的名稱來取代 HDInsight 叢集名稱，然後變更使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="b7371-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="b7371-153">資料集</span><span class="sxs-lookup"><span data-stu-id="b7371-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="b7371-154">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="b7371-154">Output dataset</span></span>
<span data-ttu-id="b7371-155">此範例中的管線不需要取得任何輸入。</span><span class="sxs-lookup"><span data-stu-id="b7371-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="b7371-156">您必須指定 HDInsight 串流活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="b7371-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="b7371-157">這個資料集只是一個驅動管線排程所需的虛設資料集。</span><span class="sxs-lookup"><span data-stu-id="b7371-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="b7371-158">管線</span><span class="sxs-lookup"><span data-stu-id="b7371-158">Pipeline</span></span>
<span data-ttu-id="b7371-159">此範例中的管線只含有一個類型為 **HDInsightStreaming**的活動。</span><span class="sxs-lookup"><span data-stu-id="b7371-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="b7371-160">HDInsight 叢集會使用範例程式 (wc.exe 和 cat.exe) 和資料 (將 davinci.txt) 自動填入。</span><span class="sxs-lookup"><span data-stu-id="b7371-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b7371-161">根據預設，HDInsight 叢集所使用的容器名稱是叢集本身的名稱。</span><span class="sxs-lookup"><span data-stu-id="b7371-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="b7371-162">例如，如果您的叢集名稱是 myhdicluster，相關聯的 Blob 容器名稱為 myhdicluster。</span><span class="sxs-lookup"><span data-stu-id="b7371-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="b7371-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7371-163">See Also</span></span>
* [<span data-ttu-id="b7371-164">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="b7371-165">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="b7371-166">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="b7371-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="b7371-167">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="b7371-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="b7371-168">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="b7371-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

