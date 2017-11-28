---
title: "使用 Hive 活動-Azure aaaTransform 資料 |Microsoft 文件"
description: "了解如何使用 Azure data factory toorun Hive 查詢中的 hello Hive 活動上指定/您自己的 HDInsight 叢集上。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="7f46e-103">使用 Azure Data Factory 中的 Hive 活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="7f46e-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="7f46e-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="7f46e-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="7f46e-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="7f46e-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="7f46e-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="7f46e-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="7f46e-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="7f46e-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="7f46e-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="7f46e-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="7f46e-114">hello Data Factory 中的 HDInsight Hive 活動[管線](data-factory-create-pipelines.md)上執行 Hive 查詢[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7f46e-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7f46e-115">這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="7f46e-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="7f46e-116">如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。</span><span class="sxs-lookup"><span data-stu-id="7f46e-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="7f46e-117">語法</span><span class="sxs-lookup"><span data-stu-id="7f46e-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="7f46e-118">語法詳細資料</span><span class="sxs-lookup"><span data-stu-id="7f46e-118">Syntax details</span></span>
| <span data-ttu-id="7f46e-119">屬性</span><span class="sxs-lookup"><span data-stu-id="7f46e-119">Property</span></span> | <span data-ttu-id="7f46e-120">說明</span><span class="sxs-lookup"><span data-stu-id="7f46e-120">Description</span></span> | <span data-ttu-id="7f46e-121">必要</span><span class="sxs-lookup"><span data-stu-id="7f46e-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f46e-122">名稱</span><span class="sxs-lookup"><span data-stu-id="7f46e-122">name</span></span> |<span data-ttu-id="7f46e-123">Hello 活動的名稱。</span><span class="sxs-lookup"><span data-stu-id="7f46e-123">Name of hello activity</span></span> |<span data-ttu-id="7f46e-124">是</span><span class="sxs-lookup"><span data-stu-id="7f46e-124">Yes</span></span> |
| <span data-ttu-id="7f46e-125">說明</span><span class="sxs-lookup"><span data-stu-id="7f46e-125">description</span></span> |<span data-ttu-id="7f46e-126">描述用於 hello 活動的文字</span><span class="sxs-lookup"><span data-stu-id="7f46e-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="7f46e-127">否</span><span class="sxs-lookup"><span data-stu-id="7f46e-127">No</span></span> |
| <span data-ttu-id="7f46e-128">類型</span><span class="sxs-lookup"><span data-stu-id="7f46e-128">type</span></span> |<span data-ttu-id="7f46e-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="7f46e-129">HDinsightHive</span></span> |<span data-ttu-id="7f46e-130">是</span><span class="sxs-lookup"><span data-stu-id="7f46e-130">Yes</span></span> |
| <span data-ttu-id="7f46e-131">輸入</span><span class="sxs-lookup"><span data-stu-id="7f46e-131">inputs</span></span> |<span data-ttu-id="7f46e-132">輸入供 hello Hive 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="7f46e-133">否</span><span class="sxs-lookup"><span data-stu-id="7f46e-133">No</span></span> |
| <span data-ttu-id="7f46e-134">輸出</span><span class="sxs-lookup"><span data-stu-id="7f46e-134">outputs</span></span> |<span data-ttu-id="7f46e-135">Hello Hive 活動所產生的輸出</span><span class="sxs-lookup"><span data-stu-id="7f46e-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="7f46e-136">是</span><span class="sxs-lookup"><span data-stu-id="7f46e-136">Yes</span></span> |
| <span data-ttu-id="7f46e-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7f46e-137">linkedServiceName</span></span> |<span data-ttu-id="7f46e-138">註冊為 Data Factory 中連結的服務參考 toohello HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="7f46e-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="7f46e-139">是</span><span class="sxs-lookup"><span data-stu-id="7f46e-139">Yes</span></span> |
| <span data-ttu-id="7f46e-140">script</span><span class="sxs-lookup"><span data-stu-id="7f46e-140">script</span></span> |<span data-ttu-id="7f46e-141">指定內嵌 hello Hive 指令碼</span><span class="sxs-lookup"><span data-stu-id="7f46e-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="7f46e-142">否</span><span class="sxs-lookup"><span data-stu-id="7f46e-142">No</span></span> |
| <span data-ttu-id="7f46e-143">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="7f46e-143">script path</span></span> |<span data-ttu-id="7f46e-144">存放區 hello Hive 指令碼在 Azure blob 儲存體，並提供 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f46e-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="7f46e-145">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f46e-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="7f46e-146">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="7f46e-146">Both cannot be used together.</span></span> <span data-ttu-id="7f46e-147">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7f46e-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="7f46e-148">否</span><span class="sxs-lookup"><span data-stu-id="7f46e-148">No</span></span> |
| <span data-ttu-id="7f46e-149">定義</span><span class="sxs-lookup"><span data-stu-id="7f46e-149">defines</span></span> |<span data-ttu-id="7f46e-150">指定參數做為索引鍵/值組內使用 'hiveconf' hello Hive 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="7f46e-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="7f46e-151">否</span><span class="sxs-lookup"><span data-stu-id="7f46e-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="7f46e-152">範例</span><span class="sxs-lookup"><span data-stu-id="7f46e-152">Example</span></span>
<span data-ttu-id="7f46e-153">讓我們看一下遊戲的範例會記錄您想要玩遊戲貴公司所啟動的使用者所花費的 tooidentify hello 時間的分析。</span><span class="sxs-lookup"><span data-stu-id="7f46e-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="7f46e-154">hello 下列記錄檔是遊戲記錄範例，這是逗號 (`,`) 分隔，而且包含下列欄位 – ProfileID、 SessionStart、 持續時間、 SrcIPAddress 和遊戲類型 hello。</span><span class="sxs-lookup"><span data-stu-id="7f46e-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="7f46e-155">hello **Hive 指令碼**tooprocess 這項資料：</span><span class="sxs-lookup"><span data-stu-id="7f46e-155">hello **Hive script** tooprocess this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="7f46e-156">tooexecute 此 Hive 指令碼的 Data Factory 管線中，您需要 toodo hello 下列</span><span class="sxs-lookup"><span data-stu-id="7f46e-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="7f46e-157">建立連結的服務 tooregister[自己 HDInsight 運算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="7f46e-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="7f46e-158">讓我們將此連結服務命名為 "HDInsightLinkedService"。</span><span class="sxs-lookup"><span data-stu-id="7f46e-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="7f46e-159">建立[連結服務](data-factory-azure-blob-connector.md)tooconfigure hello 連接 tooAzure Blob 儲存體裝載 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7f46e-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="7f46e-160">讓我們來呼叫此連結服務 "StorageLinkedService"</span><span class="sxs-lookup"><span data-stu-id="7f46e-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="7f46e-161">建立[資料集](data-factory-create-datasets.md)指向 toohello 輸入 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="7f46e-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="7f46e-162">讓我們來呼叫 hello 輸入資料集 」 HiveSampleIn"和 hello 輸出資料集 」 HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="7f46e-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="7f46e-163">為檔案 tooAzure 設定步驟 2 中的 Blob 儲存體複製 hello Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="7f46e-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="7f46e-164">如果不同於裝載此查詢檔案的其中一個 hello hello 裝載 hello 資料的儲存體，建立個別的 Azure 儲存體連結服務，並參考 tooit hello 活動中。</span><span class="sxs-lookup"><span data-stu-id="7f46e-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="7f46e-165">使用 * * scriptPath * * toospecify hello 路徑 toohive 查詢檔案和**scriptLinkedService** toospecify hello hello 指令碼檔案所在的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7f46e-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7f46e-166">您也可以提供 hello 內嵌 Hive 指令碼 hello 活動定義中的使用 hello**指令碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="7f46e-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="7f46e-167">我們不建議這種方式為 hello JSON 文件中的 hello 指令碼中的所有特殊字元必須 toobe 逸出，而且可能會造成偵錯問題。</span><span class="sxs-lookup"><span data-stu-id="7f46e-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="7f46e-168">hello 最佳作法是 toofollow 步驟 #4。</span><span class="sxs-lookup"><span data-stu-id="7f46e-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="7f46e-169">建立以 hello HDInsightHive 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="7f46e-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="7f46e-170">hello 活動處理序/轉換 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7f46e-170">hello activity processes/transforms hello data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="7f46e-171">部署 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="7f46e-171">Deploy hello pipeline.</span></span> <span data-ttu-id="7f46e-172">如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="7f46e-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="7f46e-173">監視 hello 管線使用 hello 資料 factory 監視和管理檢視。</span><span class="sxs-lookup"><span data-stu-id="7f46e-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="7f46e-174">如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="7f46e-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="7f46e-175">指定 Hive 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="7f46e-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="7f46e-176">在此範例中，每天都會將遊戲記錄檔擷取到 Azure Blob 儲存體，並儲存在使用日期和時間分割的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7f46e-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="7f46e-177">您希望 tooparameterize hello Hive 指令碼和執行階段期間以動態方式傳送 hello 輸入的資料夾的位置和也會產生 hello 輸出使用日期和時間進行分割區。</span><span class="sxs-lookup"><span data-stu-id="7f46e-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="7f46e-178">toouse 參數化的 Hive 指令碼，請執行下列的 hello</span><span class="sxs-lookup"><span data-stu-id="7f46e-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="7f46e-179">定義中的 hello 參數**定義**。</span><span class="sxs-lookup"><span data-stu-id="7f46e-179">Define hello parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="7f46e-180">在 hello Hive 指令碼，請參閱 toohello 參數使用**${hiveconf: parametername}**。</span><span class="sxs-lookup"><span data-stu-id="7f46e-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="7f46e-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7f46e-181">See Also</span></span>
* [<span data-ttu-id="7f46e-182">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="7f46e-183">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="7f46e-184">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="7f46e-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="7f46e-185">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="7f46e-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="7f46e-186">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="7f46e-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

