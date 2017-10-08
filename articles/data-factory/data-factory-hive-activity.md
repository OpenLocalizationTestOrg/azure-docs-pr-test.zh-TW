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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>使用 Azure Data Factory 中的 Hive 活動轉換資料 
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

hello Data Factory 中的 HDInsight Hive 活動[管線](data-factory-create-pipelines.md)上執行 Hive 查詢[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。 這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。

> [!NOTE] 
> 如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。 

## <a name="syntax"></a>語法

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
## <a name="syntax-details"></a>語法詳細資料
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 名稱 |Hello 活動的名稱。 |是 |
| 說明 |描述用於 hello 活動的文字 |否 |
| 類型 |HDinsightHive |是 |
| 輸入 |輸入供 hello Hive 活動 |否 |
| 輸出 |Hello Hive 活動所產生的輸出 |是 |
| linkedServiceName |註冊為 Data Factory 中連結的服務參考 toohello HDInsight 叢集 |是 |
| script |指定內嵌 hello Hive 指令碼 |否 |
| 指令碼路徑 |存放區 hello Hive 指令碼在 Azure blob 儲存體，並提供 hello 路徑 toohello 檔案。 使用 'script' 或 'scriptPath' 屬性。 兩者無法同時使用。 hello 檔案名稱是區分大小寫。 |否 |
| 定義 |指定參數做為索引鍵/值組內使用 'hiveconf' hello Hive 指令碼參考 |否 |

## <a name="example"></a>範例
讓我們看一下遊戲的範例會記錄您想要玩遊戲貴公司所啟動的使用者所花費的 tooidentify hello 時間的分析。 

hello 下列記錄檔是遊戲記錄範例，這是逗號 (`,`) 分隔，而且包含下列欄位 – ProfileID、 SessionStart、 持續時間、 SrcIPAddress 和遊戲類型 hello。

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

hello **Hive 指令碼**tooprocess 這項資料：

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

tooexecute 此 Hive 指令碼的 Data Factory 管線中，您需要 toodo hello 下列

1. 建立連結的服務 tooregister[自己 HDInsight 運算叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或設定[隨選 HDInsight 計算叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。 讓我們將此連結服務命名為 "HDInsightLinkedService"。
2. 建立[連結服務](data-factory-azure-blob-connector.md)tooconfigure hello 連接 tooAzure Blob 儲存體裝載 hello 資料。 讓我們來呼叫此連結服務 "StorageLinkedService"
3. 建立[資料集](data-factory-create-datasets.md)指向 toohello 輸入 hello 輸出資料。 讓我們來呼叫 hello 輸入資料集 」 HiveSampleIn"和 hello 輸出資料集 」 HiveSampleOut"
4. 為檔案 tooAzure 設定步驟 2 中的 Blob 儲存體複製 hello Hive 查詢。 如果不同於裝載此查詢檔案的其中一個 hello hello 裝載 hello 資料的儲存體，建立個別的 Azure 儲存體連結服務，並參考 tooit hello 活動中。 使用 * * scriptPath * * toospecify hello 路徑 toohive 查詢檔案和**scriptLinkedService** toospecify hello hello 指令碼檔案所在的 Azure 儲存體。 
   
   > [!NOTE]
   > 您也可以提供 hello 內嵌 Hive 指令碼 hello 活動定義中的使用 hello**指令碼**屬性。 我們不建議這種方式為 hello JSON 文件中的 hello 指令碼中的所有特殊字元必須 toobe 逸出，而且可能會造成偵錯問題。 hello 最佳作法是 toofollow 步驟 #4。
   > 
   > 
5. 建立以 hello HDInsightHive 活動的管線。 hello 活動處理序/轉換 hello 資料。

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
6. 部署 hello 管線。 如需詳細資料，請參閱〈 [建立管線](data-factory-create-pipelines.md) 〉文章。 
7. 監視 hello 管線使用 hello 資料 factory 監視和管理檢視。 如需詳細資料，請參閱〈 [監視及管理 Data Factory 管線](data-factory-monitor-manage-pipelines.md) 〉文章。 

## <a name="specifying-parameters-for-a-hive-script"></a>指定 Hive 指令碼的參數
在此範例中，每天都會將遊戲記錄檔擷取到 Azure Blob 儲存體，並儲存在使用日期和時間分割的資料夾。 您希望 tooparameterize hello Hive 指令碼和執行階段期間以動態方式傳送 hello 輸入的資料夾的位置和也會產生 hello 輸出使用日期和時間進行分割區。

toouse 參數化的 Hive 指令碼，請執行下列的 hello

* 定義中的 hello 參數**定義**。

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
* 在 hello Hive 指令碼，請參閱 toohello 參數使用**${hiveconf: parametername}**。 
  
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
## <a name="see-also"></a>另請參閱
* [Pig 活動](data-factory-pig-activity.md)
* [MapReduce 活動](data-factory-map-reduce.md)
* [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
* [叫用 Spark 程式](data-factory-spark.md)
* [叫用 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

