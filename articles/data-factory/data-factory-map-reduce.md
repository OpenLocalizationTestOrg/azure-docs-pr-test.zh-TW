---
title: "aaaInvoke 從 Azure Data Factory 的 MapReduce 程式"
description: "了解 Azure HDInsight 上執行 MapReduce 程式 tooprocess 資料從 Azure data factory 的叢集化。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="7c70a-103">從 Data Factory 叫用 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="7c70a-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="7c70a-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="7c70a-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="7c70a-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="7c70a-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="7c70a-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="7c70a-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="7c70a-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="7c70a-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="7c70a-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="7c70a-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="7c70a-114">hello Data Factory 中的 HDInsight MapReduce 活動[管線](data-factory-create-pipelines.md)上執行 MapReduce 程式[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7c70a-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7c70a-115">這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="7c70a-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="7c70a-116">如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。</span><span class="sxs-lookup"><span data-stu-id="7c70a-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="7c70a-117">簡介</span><span class="sxs-lookup"><span data-stu-id="7c70a-117">Introduction</span></span>
<span data-ttu-id="7c70a-118">Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="7c70a-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="7c70a-119">它包含一系列活動，其中每個活動都會執行特定的處理作業。</span><span class="sxs-lookup"><span data-stu-id="7c70a-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="7c70a-120">本文說明如何使用 hello HDInsight MapReduce 活動。</span><span class="sxs-lookup"><span data-stu-id="7c70a-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="7c70a-121">若要了解如何使用 HDInsight 的 Pig 和 Hive 活動，在 Windows/Linux 型 HDInsight 叢集上從管線執行 Pig/Hive 指令碼，請參閱 [Pig](data-factory-pig-activity.md) 和 [Hive](data-factory-hive-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="7c70a-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="7c70a-122">「HDInsight MapReduce 活動」的 JSON</span><span class="sxs-lookup"><span data-stu-id="7c70a-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="7c70a-123">在 hello hello HDInsight 活動的 JSON 定義：</span><span class="sxs-lookup"><span data-stu-id="7c70a-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="7c70a-124">設定 hello**類型**的 hello**活動**太**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="7c70a-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="7c70a-125">指定 hello hello 類別名稱**className**屬性。</span><span class="sxs-lookup"><span data-stu-id="7c70a-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="7c70a-126">指定 hello 路徑 toohello JAR 檔包括檔案名稱 hello **jarFilePath**屬性。</span><span class="sxs-lookup"><span data-stu-id="7c70a-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="7c70a-127">指定參照 toohello 包含 hello JAR 檔案的 Azure Blob 儲存體之連結的 hello 服務**jarLinkedService**屬性。</span><span class="sxs-lookup"><span data-stu-id="7c70a-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="7c70a-128">指定 hello MapReduce 程式的任何引數中 hello**引數**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7c70a-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="7c70a-129">在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。</span><span class="sxs-lookup"><span data-stu-id="7c70a-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="7c70a-130">toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項)。</span><span class="sxs-lookup"><span data-stu-id="7c70a-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="7c70a-131">您可以使用 hello HDInsight MapReduce 活動 toorun 在 HDInsight 叢集上的任何 MapReduce jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70a-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="7c70a-132">在 hello 管線，hello HDInsight 活動的下列 JSON 定義範例會設定 toorun 砲象兵 JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70a-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="7c70a-133">GitHub 上的範例</span><span class="sxs-lookup"><span data-stu-id="7c70a-133">Sample on GitHub</span></span>
<span data-ttu-id="7c70a-134">您可以下載範例，以使用 hello HDInsight MapReduce 活動從： [GitHub 上的資料處理站範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)。</span><span class="sxs-lookup"><span data-stu-id="7c70a-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="7c70a-135">執行 hello 字數統計程式</span><span class="sxs-lookup"><span data-stu-id="7c70a-135">Running hello Word Count program</span></span>
<span data-ttu-id="7c70a-136">這個範例中的 hello 管線執行 Azure HDInsight 叢集上的 hello 字數統計 Map/Reduce 程式。</span><span class="sxs-lookup"><span data-stu-id="7c70a-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="7c70a-137">連結的服務</span><span class="sxs-lookup"><span data-stu-id="7c70a-137">Linked Services</span></span>
<span data-ttu-id="7c70a-138">首先，您可以建立連結的服務 toolink hello Azure 儲存體，以供 hello Azure HDInsight 叢集的 toohello Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="7c70a-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="7c70a-139">如果您複製/貼上下列程式碼的 hello，別忘了 tooreplace**帳戶名稱**和**帳戶金鑰**hello 名稱與您 Azure 儲存體的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7c70a-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="7c70a-140">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="7c70a-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="7c70a-141">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="7c70a-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="7c70a-142">接下來，您建立連結的服務 toolink Azure HDInsight 叢集 toohello Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="7c70a-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="7c70a-143">如果您複製/貼上下列程式碼的 hello，取代**HDInsight 叢集名稱**hello 名稱為您的 HDInsight 叢集和變更的使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="7c70a-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="7c70a-144">資料集</span><span class="sxs-lookup"><span data-stu-id="7c70a-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="7c70a-145">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="7c70a-145">Output dataset</span></span>
<span data-ttu-id="7c70a-146">這個範例中的 hello 管線不接受任何輸入。</span><span class="sxs-lookup"><span data-stu-id="7c70a-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="7c70a-147">您指定 hello HDInsight MapReduce 活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="7c70a-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="7c70a-148">此資料集是只空資料集是必要的 toodrive hello 管線的排程。</span><span class="sxs-lookup"><span data-stu-id="7c70a-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="7c70a-149">管線</span><span class="sxs-lookup"><span data-stu-id="7c70a-149">Pipeline</span></span>
<span data-ttu-id="7c70a-150">在此範例中的 hello 管線有只有一個活動的型別： HDInsightMapReduce。</span><span class="sxs-lookup"><span data-stu-id="7c70a-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="7c70a-151">Hello hello JSON 中的重要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="7c70a-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="7c70a-152">屬性</span><span class="sxs-lookup"><span data-stu-id="7c70a-152">Property</span></span> | <span data-ttu-id="7c70a-153">注意事項</span><span class="sxs-lookup"><span data-stu-id="7c70a-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="7c70a-154">類型</span><span class="sxs-lookup"><span data-stu-id="7c70a-154">type</span></span> |<span data-ttu-id="7c70a-155">hello 類型必須設定太**HDInsightMapReduce**。</span><span class="sxs-lookup"><span data-stu-id="7c70a-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="7c70a-156">className</span><span class="sxs-lookup"><span data-stu-id="7c70a-156">className</span></span> |<span data-ttu-id="7c70a-157">Hello 類別名稱是： **wordcount**</span><span class="sxs-lookup"><span data-stu-id="7c70a-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="7c70a-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="7c70a-158">jarFilePath</span></span> |<span data-ttu-id="7c70a-159">路徑包含 hello 類別 toohello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70a-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="7c70a-160">如果您複製/貼上下列程式碼的 hello，別忘了 toochange hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="7c70a-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="7c70a-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="7c70a-161">jarLinkedService</span></span> |<span data-ttu-id="7c70a-162">Azure 儲存體連結服務，其中包含 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70a-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="7c70a-163">這項連結的服務是指 toohello hello HDInsight 叢集相關聯的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="7c70a-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="7c70a-164">arguments</span><span class="sxs-lookup"><span data-stu-id="7c70a-164">arguments</span></span> |<span data-ttu-id="7c70a-165">hello wordcount 程式會採用兩個引數、 輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="7c70a-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="7c70a-166">hello 輸入的檔是 hello 而 davinci.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70a-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="7c70a-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7c70a-167">frequency/interval</span></span> |<span data-ttu-id="7c70a-168">這些屬性的 hello 值符合 hello 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="7c70a-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="7c70a-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7c70a-169">linkedServiceName</span></span> |<span data-ttu-id="7c70a-170">是指您稍早建立的 toohello HDInsight 連結的服務。</span><span class="sxs-lookup"><span data-stu-id="7c70a-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="7c70a-171">執行 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="7c70a-171">Run Spark programs</span></span>
<span data-ttu-id="7c70a-172">您可以使用 MapReduce 活動 toorun Spark 程式 HDInsight Spark 叢集上。</span><span class="sxs-lookup"><span data-stu-id="7c70a-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="7c70a-173">如需詳細資訊，請參閱 [從 Azure Data Factory 叫用 Spark 程式](data-factory-spark.md) 。</span><span class="sxs-lookup"><span data-stu-id="7c70a-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="7c70a-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7c70a-174">See Also</span></span>
* [<span data-ttu-id="7c70a-175">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="7c70a-176">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="7c70a-177">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="7c70a-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="7c70a-178">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="7c70a-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="7c70a-179">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="7c70a-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

