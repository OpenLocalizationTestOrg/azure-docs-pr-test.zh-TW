---
title: "Azure Data Factory 中使用 Pig 活動 aaaTransform 資料 |Microsoft 文件"
description: "了解如何使用 Azure data factory toorun Pig 指令碼中的 hello Pig 活動上指定/您自己的 HDInsight 叢集上。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="f698f-103">使用 Azure Data Factory 中的 Pig 活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="f698f-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="f698f-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="f698f-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="f698f-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="f698f-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="f698f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="f698f-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="f698f-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="f698f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="f698f-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="f698f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="f698f-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="f698f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="f698f-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="f698f-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="f698f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="f698f-114">hello Data Factory 中的 HDInsight Pig 活動[管線](data-factory-create-pipelines.md)上執行 Pig 查詢[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f698f-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f698f-115">這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="f698f-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="f698f-116">如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。</span><span class="sxs-lookup"><span data-stu-id="f698f-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="f698f-117">語法</span><span class="sxs-lookup"><span data-stu-id="f698f-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="f698f-118">語法詳細資料</span><span class="sxs-lookup"><span data-stu-id="f698f-118">Syntax details</span></span>
| <span data-ttu-id="f698f-119">屬性</span><span class="sxs-lookup"><span data-stu-id="f698f-119">Property</span></span> | <span data-ttu-id="f698f-120">說明</span><span class="sxs-lookup"><span data-stu-id="f698f-120">Description</span></span> | <span data-ttu-id="f698f-121">必要</span><span class="sxs-lookup"><span data-stu-id="f698f-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f698f-122">名稱</span><span class="sxs-lookup"><span data-stu-id="f698f-122">name</span></span> |<span data-ttu-id="f698f-123">Hello 活動的名稱。</span><span class="sxs-lookup"><span data-stu-id="f698f-123">Name of hello activity</span></span> |<span data-ttu-id="f698f-124">是</span><span class="sxs-lookup"><span data-stu-id="f698f-124">Yes</span></span> |
| <span data-ttu-id="f698f-125">說明</span><span class="sxs-lookup"><span data-stu-id="f698f-125">description</span></span> |<span data-ttu-id="f698f-126">描述用於 hello 活動的文字</span><span class="sxs-lookup"><span data-stu-id="f698f-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="f698f-127">否</span><span class="sxs-lookup"><span data-stu-id="f698f-127">No</span></span> |
| <span data-ttu-id="f698f-128">類型</span><span class="sxs-lookup"><span data-stu-id="f698f-128">type</span></span> |<span data-ttu-id="f698f-129">HDInsightPig</span><span class="sxs-lookup"><span data-stu-id="f698f-129">HDinsightPig</span></span> |<span data-ttu-id="f698f-130">是</span><span class="sxs-lookup"><span data-stu-id="f698f-130">Yes</span></span> |
| <span data-ttu-id="f698f-131">輸入</span><span class="sxs-lookup"><span data-stu-id="f698f-131">inputs</span></span> |<span data-ttu-id="f698f-132">一個或多個輸入供 hello Pig 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="f698f-133">否</span><span class="sxs-lookup"><span data-stu-id="f698f-133">No</span></span> |
| <span data-ttu-id="f698f-134">輸出</span><span class="sxs-lookup"><span data-stu-id="f698f-134">outputs</span></span> |<span data-ttu-id="f698f-135">一個或多個輸出所產生的 hello Pig 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="f698f-136">是</span><span class="sxs-lookup"><span data-stu-id="f698f-136">Yes</span></span> |
| <span data-ttu-id="f698f-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f698f-137">linkedServiceName</span></span> |<span data-ttu-id="f698f-138">註冊為 Data Factory 中連結的服務參考 toohello HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f698f-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="f698f-139">是</span><span class="sxs-lookup"><span data-stu-id="f698f-139">Yes</span></span> |
| <span data-ttu-id="f698f-140">script</span><span class="sxs-lookup"><span data-stu-id="f698f-140">script</span></span> |<span data-ttu-id="f698f-141">指定 hello Pig 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="f698f-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="f698f-142">否</span><span class="sxs-lookup"><span data-stu-id="f698f-142">No</span></span> |
| <span data-ttu-id="f698f-143">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="f698f-143">script path</span></span> |<span data-ttu-id="f698f-144">在 Azure blob 儲存體中儲存 hello Pig 指令碼，並提供 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="f698f-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="f698f-145">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="f698f-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="f698f-146">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="f698f-146">Both cannot be used together.</span></span> <span data-ttu-id="f698f-147">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f698f-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="f698f-148">否</span><span class="sxs-lookup"><span data-stu-id="f698f-148">No</span></span> |
| <span data-ttu-id="f698f-149">定義</span><span class="sxs-lookup"><span data-stu-id="f698f-149">defines</span></span> |<span data-ttu-id="f698f-150">指定參數做為索引鍵/值組內 hello Pig 指令碼參考</span><span class="sxs-lookup"><span data-stu-id="f698f-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="f698f-151">否</span><span class="sxs-lookup"><span data-stu-id="f698f-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="f698f-152">範例</span><span class="sxs-lookup"><span data-stu-id="f698f-152">Example</span></span>
<span data-ttu-id="f698f-153">讓我們看一下遊戲的範例記錄 tooidentify hello 時間花費在玩家玩遊戲由您的公司應用程式啟動所在的分析。</span><span class="sxs-lookup"><span data-stu-id="f698f-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="f698f-154">下列範例遊戲的記錄檔的 hello 是逗號 （，） 分隔的檔案。</span><span class="sxs-lookup"><span data-stu-id="f698f-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="f698f-155">它包含下列欄位 – ProfileID、 SessionStart、 持續時間、 SrcIPAddress 和遊戲類型 hello。</span><span class="sxs-lookup"><span data-stu-id="f698f-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="f698f-156">hello **Pig 指令碼**tooprocess 這項資料：</span><span class="sxs-lookup"><span data-stu-id="f698f-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="f698f-157">tooexecute 此 Pig 指令碼在 Data Factory 管線中，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f698f-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="f698f-158">建立連結的服務 tooregister[自己 HDInsight 運算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="f698f-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="f698f-159">讓我們將此連結服務命名為 **HDInsightLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="f698f-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="f698f-160">建立[連結服務](data-factory-azure-blob-connector.md)tooconfigure hello 連接 tooAzure Blob 儲存體裝載 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f698f-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="f698f-161">讓我們將此連結服務命名為 **StorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="f698f-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="f698f-162">建立[資料集](data-factory-create-datasets.md)指向 toohello 輸入 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="f698f-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="f698f-163">讓我們來呼叫 hello 輸入資料集**PigSampleIn** hello 輸出資料集和**PigSampleOut**。</span><span class="sxs-lookup"><span data-stu-id="f698f-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="f698f-164">複製檔案 hello 步驟 #2 中設定的 Azure Blob 儲存體中的 hello Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="f698f-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="f698f-165">如果 hello 裝載 hello 資料的 Azure 儲存體是 hello 其中一個裝載 hello 查詢檔案，建立個別的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="f698f-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="f698f-166">請參閱連結的 toohello hello 活動組態中的服務。</span><span class="sxs-lookup"><span data-stu-id="f698f-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="f698f-167">使用 * * scriptPath * * toospecify hello 路徑 toopig 指令碼檔案和**scriptLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="f698f-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f698f-168">您也可以提供 hello Pig 指令碼內嵌 hello 活動定義中的使用 hello**指令碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="f698f-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="f698f-169">不過，我們不建議這種方法為 hello 指令碼中的所有特殊字元必須 toobe 逸出，而且可能會造成偵錯問題。</span><span class="sxs-lookup"><span data-stu-id="f698f-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="f698f-170">hello 最佳作法是 toofollow 步驟 #4。</span><span class="sxs-lookup"><span data-stu-id="f698f-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="f698f-171">建立 hello 管線以 hello HDInsightPig 活動。</span><span class="sxs-lookup"><span data-stu-id="f698f-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="f698f-172">此活動的 HDInsight 叢集上執行 Pig 指令碼處理 hello 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="f698f-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="f698f-173">部署 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="f698f-173">Deploy hello pipeline.</span></span> <span data-ttu-id="f698f-174">如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="f698f-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="f698f-175">監視 hello 管線使用 hello 資料 factory 監視和管理檢視。</span><span class="sxs-lookup"><span data-stu-id="f698f-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="f698f-176">如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="f698f-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="f698f-177">指定 Pig 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="f698f-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="f698f-178">請考慮下列範例中的 hello： 遊戲的記錄檔會內嵌每日到 Azure Blob 儲存體並儲存在資料分割根據的日期和時間的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f698f-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="f698f-179">您希望 tooparameterize hello Pig 指令碼和執行階段期間以動態方式傳送 hello 輸入的資料夾的位置和也會產生 hello 輸出使用日期和時間進行分割區。</span><span class="sxs-lookup"><span data-stu-id="f698f-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="f698f-180">toouse 參數化 Pig 指令碼，請執行下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="f698f-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="f698f-181">定義中的 hello 參數**定義**。</span><span class="sxs-lookup"><span data-stu-id="f698f-181">Define hello parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="f698f-182">在 hello Pig 指令碼，請參閱 toohello 參數使用 '**$parameterName**' hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f698f-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="f698f-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f698f-183">See Also</span></span>
* [<span data-ttu-id="f698f-184">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="f698f-185">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="f698f-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="f698f-186">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="f698f-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="f698f-187">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="f698f-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="f698f-188">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="f698f-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

