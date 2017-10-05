---
title: "使用 Azure Data Factory 中的 Pig 活動轉換資料 | Microsoft Docs"
description: "了解如何使用 Azure 資料處理站中的 Pig 活動，以在隨選/您自己的 HDInsight 叢集上執行 Pig 指令碼。"
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
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="083c9-103">使用 Azure Data Factory 中的 Pig 活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="083c9-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="083c9-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="083c9-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="083c9-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="083c9-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="083c9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="083c9-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="083c9-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="083c9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="083c9-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="083c9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="083c9-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="083c9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="083c9-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="083c9-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="083c9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="083c9-114">Data Factory [管線](data-factory-create-pipelines.md)中的 HDInsight Pig 活動會在[您自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨選](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)的 Windows/Linux 架構 HDInsight 叢集上執行 Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="083c9-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="083c9-115">本文是根據 [資料轉換活動](data-factory-data-transformation-activities.md) 一文，它呈現資料轉換和支援的轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="083c9-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="083c9-116">如果您是 Azure Data Factory 的新手，請在閱讀本文章之前閱讀 [Azure Data Factory 簡介](data-factory-introduction.md)，以及進行教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="083c9-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="083c9-117">語法</span><span class="sxs-lookup"><span data-stu-id="083c9-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="083c9-118">語法詳細資料</span><span class="sxs-lookup"><span data-stu-id="083c9-118">Syntax details</span></span>
| <span data-ttu-id="083c9-119">屬性</span><span class="sxs-lookup"><span data-stu-id="083c9-119">Property</span></span> | <span data-ttu-id="083c9-120">說明</span><span class="sxs-lookup"><span data-stu-id="083c9-120">Description</span></span> | <span data-ttu-id="083c9-121">必要</span><span class="sxs-lookup"><span data-stu-id="083c9-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="083c9-122">名稱</span><span class="sxs-lookup"><span data-stu-id="083c9-122">name</span></span> |<span data-ttu-id="083c9-123">活動的名稱</span><span class="sxs-lookup"><span data-stu-id="083c9-123">Name of the activity</span></span> |<span data-ttu-id="083c9-124">是</span><span class="sxs-lookup"><span data-stu-id="083c9-124">Yes</span></span> |
| <span data-ttu-id="083c9-125">說明</span><span class="sxs-lookup"><span data-stu-id="083c9-125">description</span></span> |<span data-ttu-id="083c9-126">說明活動用途的文字</span><span class="sxs-lookup"><span data-stu-id="083c9-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="083c9-127">否</span><span class="sxs-lookup"><span data-stu-id="083c9-127">No</span></span> |
| <span data-ttu-id="083c9-128">類型</span><span class="sxs-lookup"><span data-stu-id="083c9-128">type</span></span> |<span data-ttu-id="083c9-129">HDInsightPig</span><span class="sxs-lookup"><span data-stu-id="083c9-129">HDinsightPig</span></span> |<span data-ttu-id="083c9-130">是</span><span class="sxs-lookup"><span data-stu-id="083c9-130">Yes</span></span> |
| <span data-ttu-id="083c9-131">輸入</span><span class="sxs-lookup"><span data-stu-id="083c9-131">inputs</span></span> |<span data-ttu-id="083c9-132">Pig 活動所取用的一或多項輸入</span><span class="sxs-lookup"><span data-stu-id="083c9-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="083c9-133">否</span><span class="sxs-lookup"><span data-stu-id="083c9-133">No</span></span> |
| <span data-ttu-id="083c9-134">輸出</span><span class="sxs-lookup"><span data-stu-id="083c9-134">outputs</span></span> |<span data-ttu-id="083c9-135">Pig 活動所產生的一或多項輸出</span><span class="sxs-lookup"><span data-stu-id="083c9-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="083c9-136">是</span><span class="sxs-lookup"><span data-stu-id="083c9-136">Yes</span></span> |
| <span data-ttu-id="083c9-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="083c9-137">linkedServiceName</span></span> |<span data-ttu-id="083c9-138">參考 HDInsight 叢集註冊為 Data Factory 中的連結服務</span><span class="sxs-lookup"><span data-stu-id="083c9-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="083c9-139">是</span><span class="sxs-lookup"><span data-stu-id="083c9-139">Yes</span></span> |
| <span data-ttu-id="083c9-140">script</span><span class="sxs-lookup"><span data-stu-id="083c9-140">script</span></span> |<span data-ttu-id="083c9-141">指定 Pig 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="083c9-141">Specify the Pig script inline</span></span> |<span data-ttu-id="083c9-142">否</span><span class="sxs-lookup"><span data-stu-id="083c9-142">No</span></span> |
| <span data-ttu-id="083c9-143">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="083c9-143">script path</span></span> |<span data-ttu-id="083c9-144">在 Azure blob 儲存體中儲存 Pig 指令碼，並提供檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="083c9-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="083c9-145">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="083c9-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="083c9-146">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="083c9-146">Both cannot be used together.</span></span> <span data-ttu-id="083c9-147">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="083c9-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="083c9-148">否</span><span class="sxs-lookup"><span data-stu-id="083c9-148">No</span></span> |
| <span data-ttu-id="083c9-149">定義</span><span class="sxs-lookup"><span data-stu-id="083c9-149">defines</span></span> |<span data-ttu-id="083c9-150">在使用 Pig 指令碼內指定參數做為參考的機碼/值組</span><span class="sxs-lookup"><span data-stu-id="083c9-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="083c9-151">否</span><span class="sxs-lookup"><span data-stu-id="083c9-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="083c9-152">範例</span><span class="sxs-lookup"><span data-stu-id="083c9-152">Example</span></span>
<span data-ttu-id="083c9-153">讓我們思考一下一個遊戲記錄檔分析範例，在此範例中，您想要了解遊戲玩家花費多少時間玩貴公司所推出的遊戲。</span><span class="sxs-lookup"><span data-stu-id="083c9-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="083c9-154">下列範例遊戲記錄檔是一個逗點 (,) 分隔檔。</span><span class="sxs-lookup"><span data-stu-id="083c9-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="083c9-155">它包含下列欄位 – ProfileID、SessionStart、Duration、SrcIPAddress 及 GameType。</span><span class="sxs-lookup"><span data-stu-id="083c9-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="083c9-156">用來處理此資料的「Pig 指令碼」  ：</span><span class="sxs-lookup"><span data-stu-id="083c9-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="083c9-157">若要在 Data Factory 管線中執行此 Pig 指令碼，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="083c9-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="083c9-158">建立連結服務以註冊[您自己的 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="083c9-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="083c9-159">讓我們將此連結服務命名為 **HDInsightLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="083c9-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="083c9-160">建立 [連結服務](data-factory-azure-blob-connector.md) 以設定裝載資料之 Azure Blob 儲存體的連接。</span><span class="sxs-lookup"><span data-stu-id="083c9-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="083c9-161">讓我們將此連結服務命名為 **StorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="083c9-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="083c9-162">建立指向輸入和輸出資料的 [資料集](data-factory-create-datasets.md) 。</span><span class="sxs-lookup"><span data-stu-id="083c9-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="083c9-163">讓我們將此輸出資料集命名為 **PigSampleIn**，以及將輸出資料集命名為 **PigSampleOut**。</span><span class="sxs-lookup"><span data-stu-id="083c9-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="083c9-164">複製「Azure Blob 儲存體」在步驟 #2 所設定之檔案中的Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="083c9-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="083c9-165">如果裝載資料的 Azure 儲存體與裝載查詢檔案的儲存體不同，請建立個別的「Azure 儲存體」連結服務。</span><span class="sxs-lookup"><span data-stu-id="083c9-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="083c9-166">請參考活動組態中的連結服務。</span><span class="sxs-lookup"><span data-stu-id="083c9-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="083c9-167">使用 **scriptPath ** 來指定 Pig 指令碼檔案和 **scriptLinkedService** 的路徑。</span><span class="sxs-lookup"><span data-stu-id="083c9-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="083c9-168">您也可以使用 **script** 屬性，在活動定義中以內嵌方式提供 Pig 指令碼。</span><span class="sxs-lookup"><span data-stu-id="083c9-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="083c9-169">不過，不建議使用此方法，因為必須逸出指令碼中的所有特殊字元，而且可能造成偵錯問題。</span><span class="sxs-lookup"><span data-stu-id="083c9-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="083c9-170">最佳做法是遵循步驟 #4。</span><span class="sxs-lookup"><span data-stu-id="083c9-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="083c9-171">建立具有 HDInsightPig 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="083c9-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="083c9-172">此活動會透過在 HDInsight 叢集上執行 Pig 指令碼來處理輸入資料。</span><span class="sxs-lookup"><span data-stu-id="083c9-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="083c9-173">部署管線。</span><span class="sxs-lookup"><span data-stu-id="083c9-173">Deploy the pipeline.</span></span> <span data-ttu-id="083c9-174">如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="083c9-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="083c9-175">使用資料處理站監視和管理檢視來監視管線。</span><span class="sxs-lookup"><span data-stu-id="083c9-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="083c9-176">如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="083c9-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="083c9-177">指定 Pig 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="083c9-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="083c9-178">請思考一下下列範例：遊戲記錄檔每天都會被擷取至「Azure Blob 儲存體」，並儲存在根據日期和時間分割的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="083c9-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="083c9-179">您想要參數化 Pig 指令碼，在執行階段期間以動態方式傳遞輸入資料夾位置，並且產生使用日期和時間分割的輸出。</span><span class="sxs-lookup"><span data-stu-id="083c9-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="083c9-180">若要使用參數化 Pig 指令碼，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="083c9-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="083c9-181">定義 **defines**中的參數。</span><span class="sxs-lookup"><span data-stu-id="083c9-181">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="083c9-182">在 Pig 指令碼中，使用 '**$parameterName**' 參考參數，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="083c9-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="083c9-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="083c9-183">See Also</span></span>
* [<span data-ttu-id="083c9-184">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="083c9-185">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="083c9-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="083c9-186">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="083c9-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="083c9-187">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="083c9-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="083c9-188">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="083c9-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

