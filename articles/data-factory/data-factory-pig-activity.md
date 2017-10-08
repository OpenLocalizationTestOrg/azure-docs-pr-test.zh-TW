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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>使用 Azure Data Factory 中的 Pig 活動轉換資料
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md) 
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

hello Data Factory 中的 HDInsight Pig 活動[管線](data-factory-create-pipelines.md)上執行 Pig 查詢[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。 這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。

> [!NOTE] 
> 如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。 

## <a name="syntax"></a>語法

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
## <a name="syntax-details"></a>語法詳細資料
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 活動的名稱。 |是 |
| 說明 |描述用於 hello 活動的文字 |否 |
| 類型 |HDInsightPig |是 |
| 輸入 |一個或多個輸入供 hello Pig 活動 |否 |
| 輸出 |一個或多個輸出所產生的 hello Pig 活動 |是 |
| linkedServiceName |註冊為 Data Factory 中連結的服務參考 toohello HDInsight 叢集 |是 |
| script |指定 hello Pig 指令碼內嵌 |否 |
| 指令碼路徑 |在 Azure blob 儲存體中儲存 hello Pig 指令碼，並提供 hello 路徑 toohello 檔案。 使用 'script' 或 'scriptPath' 屬性。 兩者無法同時使用。 hello 檔案名稱是區分大小寫。 |否 |
| 定義 |指定參數做為索引鍵/值組內 hello Pig 指令碼參考 |否 |

## <a name="example"></a>範例
讓我們看一下遊戲的範例記錄 tooidentify hello 時間花費在玩家玩遊戲由您的公司應用程式啟動所在的分析。

下列範例遊戲的記錄檔的 hello 是逗號 （，） 分隔的檔案。 它包含下列欄位 – ProfileID、 SessionStart、 持續時間、 SrcIPAddress 和遊戲類型 hello。

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

hello **Pig 指令碼**tooprocess 這項資料：

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

tooexecute 此 Pig 指令碼在 Data Factory 管線中，請勿 hello 下列步驟：

1. 建立連結的服務 tooregister[自己 HDInsight 運算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。 讓我們將此連結服務命名為 **HDInsightLinkedService**。
2. 建立[連結服務](data-factory-azure-blob-connector.md)tooconfigure hello 連接 tooAzure Blob 儲存體裝載 hello 資料。 讓我們將此連結服務命名為 **StorageLinkedService**。
3. 建立[資料集](data-factory-create-datasets.md)指向 toohello 輸入 hello 輸出資料。 讓我們來呼叫 hello 輸入資料集**PigSampleIn** hello 輸出資料集和**PigSampleOut**。
4. 複製檔案 hello 步驟 #2 中設定的 Azure Blob 儲存體中的 hello Pig 查詢。 如果 hello 裝載 hello 資料的 Azure 儲存體是 hello 其中一個裝載 hello 查詢檔案，建立個別的 Azure 儲存體連結服務。 請參閱連結的 toohello hello 活動組態中的服務。 使用 * * scriptPath * * toospecify hello 路徑 toopig 指令碼檔案和**scriptLinkedService**。 
   
   > [!NOTE]
   > 您也可以提供 hello Pig 指令碼內嵌 hello 活動定義中的使用 hello**指令碼**屬性。 不過，我們不建議這種方法為 hello 指令碼中的所有特殊字元必須 toobe 逸出，而且可能會造成偵錯問題。 hello 最佳作法是 toofollow 步驟 #4。
   > 
   > 
5. 建立 hello 管線以 hello HDInsightPig 活動。 此活動的 HDInsight 叢集上執行 Pig 指令碼處理 hello 輸入的資料。

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
6. 部署 hello 管線。 如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。 
7. 監視 hello 管線使用 hello 資料 factory 監視和管理檢視。 如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。

## <a name="specifying-parameters-for-a-pig-script"></a>指定 Pig 指令碼的參數
請考慮下列範例中的 hello： 遊戲的記錄檔會內嵌每日到 Azure Blob 儲存體並儲存在資料分割根據的日期和時間的資料夾。 您希望 tooparameterize hello Pig 指令碼和執行階段期間以動態方式傳送 hello 輸入的資料夾的位置和也會產生 hello 輸出使用日期和時間進行分割區。

toouse 參數化 Pig 指令碼，請執行下列的 hello:

* 定義中的 hello 參數**定義**。

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
* 在 hello Pig 指令碼，請參閱 toohello 參數使用 '**$parameterName**' hello 下列範例所示：

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>另請參閱
* [Hive 活動](data-factory-hive-activity.md)
* [MapReduce 活動](data-factory-map-reduce.md)
* [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
* [叫用 Spark 程式](data-factory-spark.md)
* [叫用 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

