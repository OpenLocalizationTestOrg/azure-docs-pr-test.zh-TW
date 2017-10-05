---
title: "使用 Hive 活動轉換資料 - Azure | Microsoft Docs"
description: "了解如何使用 Azure 資料處理站中的 Hive 活動，以在隨選/您自己的 HDInsight 叢集上執行 Hive 查詢。"
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="66ee4-103">使用 Azure Data Factory 中的 Hive 活動轉換資料</span><span class="sxs-lookup"><span data-stu-id="66ee4-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="66ee4-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="66ee4-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="66ee4-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="66ee4-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="66ee4-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="66ee4-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="66ee4-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="66ee4-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="66ee4-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="66ee4-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="66ee4-114">Data Factory [管線](data-factory-create-pipelines.md)中的 HDInsight Hive 活動會在[您自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨選的](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 架構 HDInsight 叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="66ee4-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="66ee4-115">本文是根據 [資料轉換活動](data-factory-data-transformation-activities.md) 一文，它呈現資料轉換和支援的轉換活動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="66ee4-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="66ee4-116">如果您是 Azure Data Factory 的新手，請在閱讀本文章之前閱讀 [Azure Data Factory 簡介](data-factory-introduction.md)，以及進行教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="66ee4-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="66ee4-117">語法</span><span class="sxs-lookup"><span data-stu-id="66ee4-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="66ee4-118">語法詳細資料</span><span class="sxs-lookup"><span data-stu-id="66ee4-118">Syntax details</span></span>
| <span data-ttu-id="66ee4-119">屬性</span><span class="sxs-lookup"><span data-stu-id="66ee4-119">Property</span></span> | <span data-ttu-id="66ee4-120">說明</span><span class="sxs-lookup"><span data-stu-id="66ee4-120">Description</span></span> | <span data-ttu-id="66ee4-121">必要</span><span class="sxs-lookup"><span data-stu-id="66ee4-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66ee4-122">名稱</span><span class="sxs-lookup"><span data-stu-id="66ee4-122">name</span></span> |<span data-ttu-id="66ee4-123">活動的名稱</span><span class="sxs-lookup"><span data-stu-id="66ee4-123">Name of the activity</span></span> |<span data-ttu-id="66ee4-124">是</span><span class="sxs-lookup"><span data-stu-id="66ee4-124">Yes</span></span> |
| <span data-ttu-id="66ee4-125">說明</span><span class="sxs-lookup"><span data-stu-id="66ee4-125">description</span></span> |<span data-ttu-id="66ee4-126">說明活動用途的文字</span><span class="sxs-lookup"><span data-stu-id="66ee4-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="66ee4-127">否</span><span class="sxs-lookup"><span data-stu-id="66ee4-127">No</span></span> |
| <span data-ttu-id="66ee4-128">類型</span><span class="sxs-lookup"><span data-stu-id="66ee4-128">type</span></span> |<span data-ttu-id="66ee4-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="66ee4-129">HDinsightHive</span></span> |<span data-ttu-id="66ee4-130">是</span><span class="sxs-lookup"><span data-stu-id="66ee4-130">Yes</span></span> |
| <span data-ttu-id="66ee4-131">輸入</span><span class="sxs-lookup"><span data-stu-id="66ee4-131">inputs</span></span> |<span data-ttu-id="66ee4-132">Hive 活動所耗用的輸入</span><span class="sxs-lookup"><span data-stu-id="66ee4-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="66ee4-133">否</span><span class="sxs-lookup"><span data-stu-id="66ee4-133">No</span></span> |
| <span data-ttu-id="66ee4-134">輸出</span><span class="sxs-lookup"><span data-stu-id="66ee4-134">outputs</span></span> |<span data-ttu-id="66ee4-135">Hive 活動所耗用的輸出</span><span class="sxs-lookup"><span data-stu-id="66ee4-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="66ee4-136">是</span><span class="sxs-lookup"><span data-stu-id="66ee4-136">Yes</span></span> |
| <span data-ttu-id="66ee4-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="66ee4-137">linkedServiceName</span></span> |<span data-ttu-id="66ee4-138">參考 HDInsight 叢集註冊為 Data Factory 中的連結服務</span><span class="sxs-lookup"><span data-stu-id="66ee4-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="66ee4-139">是</span><span class="sxs-lookup"><span data-stu-id="66ee4-139">Yes</span></span> |
| <span data-ttu-id="66ee4-140">script</span><span class="sxs-lookup"><span data-stu-id="66ee4-140">script</span></span> |<span data-ttu-id="66ee4-141">指定 Hive 指令碼內嵌</span><span class="sxs-lookup"><span data-stu-id="66ee4-141">Specify the Hive script inline</span></span> |<span data-ttu-id="66ee4-142">否</span><span class="sxs-lookup"><span data-stu-id="66ee4-142">No</span></span> |
| <span data-ttu-id="66ee4-143">指令碼路徑</span><span class="sxs-lookup"><span data-stu-id="66ee4-143">script path</span></span> |<span data-ttu-id="66ee4-144">在 Azure Blob 儲存體中儲存 Hive 指令碼，並提供檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="66ee4-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="66ee4-145">使用 'script' 或 'scriptPath' 屬性。</span><span class="sxs-lookup"><span data-stu-id="66ee4-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="66ee4-146">兩者無法同時使用。</span><span class="sxs-lookup"><span data-stu-id="66ee4-146">Both cannot be used together.</span></span> <span data-ttu-id="66ee4-147">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="66ee4-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="66ee4-148">否</span><span class="sxs-lookup"><span data-stu-id="66ee4-148">No</span></span> |
| <span data-ttu-id="66ee4-149">定義</span><span class="sxs-lookup"><span data-stu-id="66ee4-149">defines</span></span> |<span data-ttu-id="66ee4-150">在使用 'hiveconf' 的 Hive 指令碼內指定參數做為參考的金鑰/值組</span><span class="sxs-lookup"><span data-stu-id="66ee4-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="66ee4-151">否</span><span class="sxs-lookup"><span data-stu-id="66ee4-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="66ee4-152">範例</span><span class="sxs-lookup"><span data-stu-id="66ee4-152">Example</span></span>
<span data-ttu-id="66ee4-153">我們來看看遊戲記錄檔分析的範例，您想要識別使用者花多少時間在玩貴公司開發的遊戲。</span><span class="sxs-lookup"><span data-stu-id="66ee4-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="66ee4-154">下列記錄檔是範例遊戲記錄檔，以逗號 (`,`) 分隔，並包含下列欄位 – ProfileID、SessionStart、Duration、SrcIPAddress 和 GameType。</span><span class="sxs-lookup"><span data-stu-id="66ee4-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="66ee4-155">用來處理此資料的 **Hive 指令碼** ：</span><span class="sxs-lookup"><span data-stu-id="66ee4-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="66ee4-156">若要在 Data Factory 管線中執行此 Hive 指令碼，您需要執行下列動作</span><span class="sxs-lookup"><span data-stu-id="66ee4-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="66ee4-157">建立連結服務以註冊[您自己的 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="66ee4-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="66ee4-158">讓我們將此連結服務命名為 "HDInsightLinkedService"。</span><span class="sxs-lookup"><span data-stu-id="66ee4-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="66ee4-159">建立 [連結服務](data-factory-azure-blob-connector.md) 以設定裝載資料之 Azure Blob 儲存體的連接。</span><span class="sxs-lookup"><span data-stu-id="66ee4-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="66ee4-160">讓我們來呼叫此連結服務 "StorageLinkedService"</span><span class="sxs-lookup"><span data-stu-id="66ee4-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="66ee4-161">建立指向輸入和輸出資料的 [資料集](data-factory-create-datasets.md) 。</span><span class="sxs-lookup"><span data-stu-id="66ee4-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="66ee4-162">讓我們來呼叫輸入資料集 "HiveSampleIn" 和輸出資料集 "HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="66ee4-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="66ee4-163">將 Hive 查詢作為檔案複製到步驟 #2 中設定的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="66ee4-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="66ee4-164">如果裝載資料的儲存體和裝載此查詢檔案的儲存體不同，請建立個別的 Azure 儲存體連結服務並在活動中參考它。</span><span class="sxs-lookup"><span data-stu-id="66ee4-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="66ee4-165">使用 **scriptPath ** 指定 Hive 查詢檔案的路徑，並使用 **scriptLinkedService** 指定包含指令碼檔案的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="66ee4-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="66ee4-166">您也可以使用 **script** 屬性，在活動定義中以內嵌方式提供 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="66ee4-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="66ee4-167">不建議使用此方法，因為必須逸出 JSON 文件的指令碼中的所有特殊字元，而且可能造成偵錯問題。</span><span class="sxs-lookup"><span data-stu-id="66ee4-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="66ee4-168">最佳做法是遵循步驟 #4。</span><span class="sxs-lookup"><span data-stu-id="66ee4-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="66ee4-169">建立具有 HDInsightHive 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="66ee4-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="66ee4-170">活動會處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="66ee4-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="66ee4-171">部署管線。</span><span class="sxs-lookup"><span data-stu-id="66ee4-171">Deploy the pipeline.</span></span> <span data-ttu-id="66ee4-172">如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="66ee4-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="66ee4-173">使用資料處理站監視和管理檢視來監視管線。</span><span class="sxs-lookup"><span data-stu-id="66ee4-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="66ee4-174">如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。</span><span class="sxs-lookup"><span data-stu-id="66ee4-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="66ee4-175">指定 Hive 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="66ee4-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="66ee4-176">在此範例中，每天都會將遊戲記錄檔擷取到 Azure Blob 儲存體，並儲存在使用日期和時間分割的資料夾。</span><span class="sxs-lookup"><span data-stu-id="66ee4-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="66ee4-177">您想要參數化 Hive 指令碼，在執行階段期間以動態方式傳遞輸入資料夾位置，並且產生使用日期和時間分割的輸出。</span><span class="sxs-lookup"><span data-stu-id="66ee4-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="66ee4-178">若要使用參數化的 Hive 指令碼，請執行下列動作</span><span class="sxs-lookup"><span data-stu-id="66ee4-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="66ee4-179">定義 **defines**中的參數。</span><span class="sxs-lookup"><span data-stu-id="66ee4-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="66ee4-180">在 Hive 指令碼中，參考使用 **${hiveconf:parameterName}**的參數。</span><span class="sxs-lookup"><span data-stu-id="66ee4-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="66ee4-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66ee4-181">See Also</span></span>
* [<span data-ttu-id="66ee4-182">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="66ee4-183">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="66ee4-184">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="66ee4-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="66ee4-185">叫用 Spark 程式</span><span class="sxs-lookup"><span data-stu-id="66ee4-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="66ee4-186">叫用 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="66ee4-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

