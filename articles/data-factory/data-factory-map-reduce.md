---
title: "從 Azure Data Factory 叫用 MapReduce 程式"
description: "了解如何從 Azure Data Factory，在 Azure HDInsight 叢集上執行 MapReduce 程式以處理資料。"
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="64070-103">從 Data Factory 叫用 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="64070-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="64070-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="64070-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="64070-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="64070-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="64070-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="64070-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="64070-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="64070-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="64070-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="64070-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="64070-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="64070-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="64070-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="64070-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="64070-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="64070-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="64070-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="64070-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="64070-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="64070-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="64070-114">Data Factory [管線](data-factory-create-pipelines.md)中的 HDInsight MapReduce 活動會在[您自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨選](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)的 Windows/Linux 架構 HDInsight 叢集上執行 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="64070-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="64070-115">本文是根據 [資料轉換活動](data-factory-data-transformation-activities.md) 一文，它呈現資料轉換和支援的轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="64070-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="64070-116">如果您是 Azure Data Factory 的新手，請在閱讀本文章之前閱讀 [Azure Data Factory 簡介](data-factory-introduction.md)，以及進行教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="64070-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="64070-117">簡介</span><span class="sxs-lookup"><span data-stu-id="64070-117">Introduction</span></span>
<span data-ttu-id="64070-118">Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="64070-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="64070-119">它包含一系列活動，其中每個活動都會執行特定的處理作業。</span><span class="sxs-lookup"><span data-stu-id="64070-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="64070-120">本文說明如何使用「HDInsight MapReduce 活動」。</span><span class="sxs-lookup"><span data-stu-id="64070-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="64070-121">若要了解如何使用 HDInsight 的 Pig 和 Hive 活動，在 Windows/Linux 型 HDInsight 叢集上從管線執行 Pig/Hive 指令碼，請參閱 [Pig](data-factory-pig-activity.md) 和 [Hive](data-factory-hive-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="64070-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="64070-122">「HDInsight MapReduce 活動」的 JSON</span><span class="sxs-lookup"><span data-stu-id="64070-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="64070-123">在 HDInsight 活動的 JSON 定義中：</span><span class="sxs-lookup"><span data-stu-id="64070-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="64070-124">將 **activity** 的 **type** 設為 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="64070-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="64070-125">指定 **className** 屬性的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="64070-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="64070-126">為 **jarFilePath** 屬性指定包含檔案名稱的 JAR 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="64070-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="64070-127">為 **jarLinkedService** 屬性指定連結服務，此連結服務參考包含 JAR 檔案的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="64070-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="64070-128">在 **arguments** 區段中，為 MapReduce 程式指定所有引數。</span><span class="sxs-lookup"><span data-stu-id="64070-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="64070-129">在執行階段，您會看到幾個來自 MapReduce 架構的額外引數 (例如：mapreduce.job.tags)。</span><span class="sxs-lookup"><span data-stu-id="64070-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="64070-130">若要區分您的引數與 MapReduce 引數，請考慮同時使用選項和值作為引數，如下列範例所示 (-s、--input、--output 等等是後面接著其值的選項)。</span><span class="sxs-lookup"><span data-stu-id="64070-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="64070-131">您可以使用「HDInsight MapReduce 活動」，在 HDInsight 叢集上執行任何 MapReduce Jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="64070-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="64070-132">在下列管線的範例 JSON 定義中，已設定讓「HDInsight 活動」執行 Mahout JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="64070-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="64070-133">GitHub 上的範例</span><span class="sxs-lookup"><span data-stu-id="64070-133">Sample on GitHub</span></span>
<span data-ttu-id="64070-134">您可以從 [GitHub 上的 Data Factory 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)下載使用「HDInsight MapReduce 活動」的範例。</span><span class="sxs-lookup"><span data-stu-id="64070-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="64070-135">執行字數統計程式</span><span class="sxs-lookup"><span data-stu-id="64070-135">Running the Word Count program</span></span>
<span data-ttu-id="64070-136">本範例中的管線會在 Azure HDInsight 叢集上執行字數統計 Map/Reduce 程式。</span><span class="sxs-lookup"><span data-stu-id="64070-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="64070-137">連結的服務</span><span class="sxs-lookup"><span data-stu-id="64070-137">Linked Services</span></span>
<span data-ttu-id="64070-138">首先，建立連結的服務，將 Azure HDInsight 叢集使用的 Azure 儲存體連結到  Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64070-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="64070-139">如果您複製/貼上下列程式碼，請記得使用 Azure 儲存體的名稱和金鑰來取代**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="64070-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="64070-140">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="64070-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="64070-141">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="64070-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="64070-142">接著，建立連結的服務，將 Azure HDInsight 叢集連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64070-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="64070-143">如果您複製/貼上下列程式碼，請使用您的 HDInsight 叢集的名稱來取代 **HDInsight 叢集名稱** ，並變更使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="64070-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="64070-144">資料集</span><span class="sxs-lookup"><span data-stu-id="64070-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="64070-145">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="64070-145">Output dataset</span></span>
<span data-ttu-id="64070-146">此範例中的管線不需要取得任何輸入。</span><span class="sxs-lookup"><span data-stu-id="64070-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="64070-147">您需指定「HDInsight MapReduce 活動」的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="64070-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="64070-148">這個資料集只是一個驅動管線排程所需的虛設資料集。</span><span class="sxs-lookup"><span data-stu-id="64070-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="64070-149">管線</span><span class="sxs-lookup"><span data-stu-id="64070-149">Pipeline</span></span>
<span data-ttu-id="64070-150">此範例中的管線只含有一個類型為 HDInsightMapReduce 的活動。</span><span class="sxs-lookup"><span data-stu-id="64070-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="64070-151">JSON 中的幾個重要屬性如下：</span><span class="sxs-lookup"><span data-stu-id="64070-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="64070-152">屬性</span><span class="sxs-lookup"><span data-stu-id="64070-152">Property</span></span> | <span data-ttu-id="64070-153">注意事項</span><span class="sxs-lookup"><span data-stu-id="64070-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="64070-154">類型</span><span class="sxs-lookup"><span data-stu-id="64070-154">type</span></span> |<span data-ttu-id="64070-155">類型必須設為 **HDInsightMapReduce**。</span><span class="sxs-lookup"><span data-stu-id="64070-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="64070-156">className</span><span class="sxs-lookup"><span data-stu-id="64070-156">className</span></span> |<span data-ttu-id="64070-157">類別的名稱是： **wordcount**</span><span class="sxs-lookup"><span data-stu-id="64070-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="64070-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="64070-158">jarFilePath</span></span> |<span data-ttu-id="64070-159">包含類別的 Jar 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="64070-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="64070-160">如果您複製/貼上下列程式碼，請記得變更叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="64070-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="64070-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="64070-161">jarLinkedService</span></span> |<span data-ttu-id="64070-162">包含 Jar 檔案的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="64070-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="64070-163">這個連結服務會參考與 HDInsight 叢集關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="64070-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="64070-164">arguments</span><span class="sxs-lookup"><span data-stu-id="64070-164">arguments</span></span> |<span data-ttu-id="64070-165">字數統計程式會採用輸入和輸出兩個引數。</span><span class="sxs-lookup"><span data-stu-id="64070-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="64070-166">輸入檔為 davinci.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="64070-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="64070-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="64070-167">frequency/interval</span></span> |<span data-ttu-id="64070-168">這些屬性的值符合輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="64070-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="64070-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="64070-169">linkedServiceName</span></span> |<span data-ttu-id="64070-170">表示您先前建立的 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="64070-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="64070-171">執行 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="64070-171">Run Spark programs</span></span>
<span data-ttu-id="64070-172">您可以使用 MapReduce 活動，在 HDInsight Spark 叢集上執行 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="64070-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="64070-173">如需詳細資訊，請參閱 [從 Azure Data Factory 叫用 Spark 程式](data-factory-spark.md) 。</span><span class="sxs-lookup"><span data-stu-id="64070-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="64070-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64070-174">See Also</span></span>
* [<span data-ttu-id="64070-175">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="64070-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="64070-176">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="64070-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="64070-177">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="64070-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="64070-178">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="64070-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="64070-179">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="64070-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

