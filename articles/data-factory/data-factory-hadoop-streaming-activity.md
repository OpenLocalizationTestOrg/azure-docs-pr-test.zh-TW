---
title: "使用 Hadoop 資料流活動的 Azure aaaTransform 資料 |Microsoft 文件"
description: "了解如何使用 Azure data factory tootransform 資料中的 hello Hadoop 資料流活動上指定/您自己的 HDInsight 叢集上執行 Hadoop 串流程式。"
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
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="b96ea-103">使用 Azure Data Factory 中的 Hadoop 資料流活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="b96ea-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b96ea-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b96ea-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b96ea-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b96ea-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b96ea-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b96ea-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b96ea-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b96ea-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b96ea-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b96ea-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b96ea-114">您可以使用 hello HDInsightStreamingActivity 活動叫用 Hadoop 串流工作從 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="b96ea-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="b96ea-115">hello 下列 JSON 片段顯示在管線 JSON 檔案中使用 hello HDInsightStreamingActivity hello 語法。</span><span class="sxs-lookup"><span data-stu-id="b96ea-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="b96ea-116">hello Data Factory 中的 HDInsight 串流活動[管線](data-factory-create-pipelines.md)上執行 Hadoop 串流程式[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight叢集。</span><span class="sxs-lookup"><span data-stu-id="b96ea-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b96ea-117">這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="b96ea-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="b96ea-118">如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。</span><span class="sxs-lookup"><span data-stu-id="b96ea-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="b96ea-119">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="b96ea-119">JSON sample</span></span>
<span data-ttu-id="b96ea-120">hello HDInsight 叢集會自動填入範例程式 （wc.exe 和 cat.exe） 和資料 (而 davinci.txt)。</span><span class="sxs-lookup"><span data-stu-id="b96ea-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b96ea-121">根據預設，hello HDInsight 叢集所用的 hello 容器的名稱會是 hello 的 hello 叢集本身的名稱。</span><span class="sxs-lookup"><span data-stu-id="b96ea-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="b96ea-122">比方說，如果您的叢集名稱是 myhdicluster，hello 相關聯的 blob 容器的名稱將 myhdicluster。</span><span class="sxs-lookup"><span data-stu-id="b96ea-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="b96ea-123">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="b96ea-123">Note hello following points:</span></span>

1. <span data-ttu-id="b96ea-124">設定 hello **linkedServiceName** hello toohello 名稱連結點 tooyour HDInsight 叢集執行哪些 hello 串流 mapreduce 作業的服務。</span><span class="sxs-lookup"><span data-stu-id="b96ea-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="b96ea-125">設定 hello hello 活動型別太**HDInsightStreaming**。</span><span class="sxs-lookup"><span data-stu-id="b96ea-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="b96ea-126">Hello**對應工具**屬性，指定 hello 的對應工具可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="b96ea-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="b96ea-127">在 hello 範例 cat.exe 會是 hello 對應工具可執行檔。</span><span class="sxs-lookup"><span data-stu-id="b96ea-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="b96ea-128">Hello**減壓器**屬性，指定減壓器可執行檔的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b96ea-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="b96ea-129">在 hello 範例 wc.exe 是 hello 減壓器可執行檔。</span><span class="sxs-lookup"><span data-stu-id="b96ea-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="b96ea-130">Hello**輸入**輸入屬性，指定 hello 對應工具的 hello 輸入的檔 （包括 hello 位置）。</span><span class="sxs-lookup"><span data-stu-id="b96ea-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="b96ea-131">在 hello 範例: 「 wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample 是 blob 容器，hello 範例/data/Gutenberg 是 hello 資料夾，而 davinci.txt 是 hello blob。</span><span class="sxs-lookup"><span data-stu-id="b96ea-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="b96ea-132">Hello**輸出**輸入屬性，指定減壓器 hello hello 輸出檔 （包括 hello 位置）。</span><span class="sxs-lookup"><span data-stu-id="b96ea-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="b96ea-133">hello hello Hadoop 串流工作輸出寫入 toohello 針對此屬性指定的位置。</span><span class="sxs-lookup"><span data-stu-id="b96ea-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="b96ea-134">在 hello **filePaths**區段中，指定 hello hello 對應工具和減壓器可執行檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="b96ea-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="b96ea-135">在 hello 範例:"adfsample/example/apps/wc.exe"，adfsample 是 hello blob 容器，example/apps 是 hello 資料夾和 wc.exe 是可執行檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="b96ea-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="b96ea-136">Hello **fileLinkedService**屬性，指定 hello Azure 儲存體連結的服務代表 hello hello hello filePaths 區段中指定的檔案所在的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b96ea-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="b96ea-137">Hello**引數**屬性，指定資料流工作的 hello hello 引數。</span><span class="sxs-lookup"><span data-stu-id="b96ea-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="b96ea-138">hello **getDebugInfo**屬性是選擇性項目。</span><span class="sxs-lookup"><span data-stu-id="b96ea-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="b96ea-139">當它設定為 tooFailure 時，只在失敗下載 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b96ea-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="b96ea-140">當它設定為 tooAlways 時，無論 hello 執行狀態永遠下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b96ea-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="b96ea-141">Hello 範例所示，您指定的輸出資料集 hello Hadoop 資料流活動 hello**輸出**屬性。</span><span class="sxs-lookup"><span data-stu-id="b96ea-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="b96ea-142">此資料集是只空資料集是必要的 toodrive hello 管線的排程。</span><span class="sxs-lookup"><span data-stu-id="b96ea-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="b96ea-143">您不需要 toospecify 任何輸入資料集 hello 的 hello 活動**輸入**屬性。</span><span class="sxs-lookup"><span data-stu-id="b96ea-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="b96ea-144">範例</span><span class="sxs-lookup"><span data-stu-id="b96ea-144">Example</span></span>
<span data-ttu-id="b96ea-145">本逐步解說中的 hello 管線執行 hello 字數統計資料流 Map/Reduce 程式 Azure HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="b96ea-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="b96ea-146">連結的服務</span><span class="sxs-lookup"><span data-stu-id="b96ea-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b96ea-147">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="b96ea-147">Azure Storage linked service</span></span>
<span data-ttu-id="b96ea-148">首先，您可以建立連結的服務 toolink hello Azure 儲存體，以供 hello Azure HDInsight 叢集的 toohello Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="b96ea-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b96ea-149">如果您複製/貼上下列程式碼的 hello，別忘了 tooreplace 帳戶名稱和帳戶金鑰 hello 名稱和您的 Azure 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="b96ea-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="b96ea-150">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="b96ea-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="b96ea-151">接下來，您建立連結的服務 toolink Azure HDInsight 叢集 toohello Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="b96ea-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b96ea-152">如果您複製/貼上下列程式碼的 hello，以您的 HDInsight 叢集 hello 名稱取代 HDInsight 叢集名稱，並變更使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="b96ea-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="b96ea-153">資料集</span><span class="sxs-lookup"><span data-stu-id="b96ea-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="b96ea-154">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="b96ea-154">Output dataset</span></span>
<span data-ttu-id="b96ea-155">這個範例中的 hello 管線不接受任何輸入。</span><span class="sxs-lookup"><span data-stu-id="b96ea-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="b96ea-156">您指定 hello HDInsight 串流活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="b96ea-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="b96ea-157">此資料集是只空資料集是必要的 toodrive hello 管線的排程。</span><span class="sxs-lookup"><span data-stu-id="b96ea-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="b96ea-158">管線</span><span class="sxs-lookup"><span data-stu-id="b96ea-158">Pipeline</span></span>
<span data-ttu-id="b96ea-159">在此範例中的 hello 管線有只有一個活動的型別： **HDInsightStreaming**。</span><span class="sxs-lookup"><span data-stu-id="b96ea-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="b96ea-160">hello HDInsight 叢集會自動填入範例程式 （wc.exe 和 cat.exe） 和資料 (而 davinci.txt)。</span><span class="sxs-lookup"><span data-stu-id="b96ea-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b96ea-161">根據預設，hello HDInsight 叢集所用的 hello 容器的名稱會是 hello 的 hello 叢集本身的名稱。</span><span class="sxs-lookup"><span data-stu-id="b96ea-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="b96ea-162">比方說，如果您的叢集名稱是 myhdicluster，hello 相關聯的 blob 容器的名稱將 myhdicluster。</span><span class="sxs-lookup"><span data-stu-id="b96ea-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="b96ea-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b96ea-163">See Also</span></span>
* [<span data-ttu-id="b96ea-164">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="b96ea-165">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="b96ea-166">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="b96ea-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="b96ea-167">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="b96ea-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="b96ea-168">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="b96ea-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

