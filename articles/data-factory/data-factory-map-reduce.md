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
# <a name="invoke-mapreduce-programs-from-data-factory"></a>從 Data Factory 叫用 MapReduce 程式
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

hello Data Factory 中的 HDInsight MapReduce 活動[管線](data-factory-create-pipelines.md)上執行 MapReduce 程式[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight 叢集。 這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。

> [!NOTE] 
> 如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。  

## <a name="introduction"></a>簡介
Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。 它包含一系列活動，其中每個活動都會執行特定的處理作業。 本文說明如何使用 hello HDInsight MapReduce 活動。

若要了解如何使用 HDInsight 的 Pig 和 Hive 活動，在 Windows/Linux 型 HDInsight 叢集上從管線執行 Pig/Hive 指令碼，請參閱 [Pig](data-factory-pig-activity.md) 和 [Hive](data-factory-hive-activity.md)。 

## <a name="json-for-hdinsight-mapreduce-activity"></a>「HDInsight MapReduce 活動」的 JSON
在 hello hello HDInsight 活動的 JSON 定義： 

1. 設定 hello**類型**的 hello**活動**太**HDInsight**。
2. 指定 hello hello 類別名稱**className**屬性。
3. 指定 hello 路徑 toohello JAR 檔包括檔案名稱 hello **jarFilePath**屬性。
4. 指定參照 toohello 包含 hello JAR 檔案的 Azure Blob 儲存體之連結的 hello 服務**jarLinkedService**屬性。   
5. 指定 hello MapReduce 程式的任何引數中 hello**引數**> 一節。 在執行階段，您會看到幾個額外的引數 (例如： mapreduce.job.tags) 從 hello MapReduce 架構。 toodifferentiate hello MapReduce 引數時，您的引數，請考慮使用選項和值做為引數中 hello 下列範例所示 (-s，-輸入、--輸出等，是後面緊跟著其值的選項)。

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
您可以使用 hello HDInsight MapReduce 活動 toorun 在 HDInsight 叢集上的任何 MapReduce jar 檔案。 在 hello 管線，hello HDInsight 活動的下列 JSON 定義範例會設定 toorun 砲象兵 JAR 檔案。

## <a name="sample-on-github"></a>GitHub 上的範例
您可以下載範例，以使用 hello HDInsight MapReduce 活動從： [GitHub 上的資料處理站範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)。  

## <a name="running-hello-word-count-program"></a>執行 hello 字數統計程式
這個範例中的 hello 管線執行 Azure HDInsight 叢集上的 hello 字數統計 Map/Reduce 程式。   

### <a name="linked-services"></a>連結的服務
首先，您可以建立連結的服務 toolink hello Azure 儲存體，以供 hello Azure HDInsight 叢集的 toohello Azure data factory。 如果您複製/貼上下列程式碼的 hello，別忘了 tooreplace**帳戶名稱**和**帳戶金鑰**hello 名稱與您 Azure 儲存體的索引鍵。 

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務

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

#### <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 連結服務
接下來，您建立連結的服務 toolink Azure HDInsight 叢集 toohello Azure data factory。 如果您複製/貼上下列程式碼的 hello，取代**HDInsight 叢集名稱**hello 名稱為您的 HDInsight 叢集和變更的使用者名稱和密碼值。   

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

### <a name="datasets"></a>資料集
#### <a name="output-dataset"></a>輸出資料集
這個範例中的 hello 管線不接受任何輸入。 您指定 hello HDInsight MapReduce 活動的輸出資料集。 此資料集是只空資料集是必要的 toodrive hello 管線的排程。  

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

### <a name="pipeline"></a>管線
在此範例中的 hello 管線有只有一個活動的型別： HDInsightMapReduce。 Hello hello JSON 中的重要屬性包括： 

| 屬性 | 注意事項 |
|:--- |:--- |
| 類型 |hello 類型必須設定太**HDInsightMapReduce**。 |
| className |Hello 類別名稱是： **wordcount** |
| jarFilePath |路徑包含 hello 類別 toohello jar 檔案。 如果您複製/貼上下列程式碼的 hello，別忘了 toochange hello hello 叢集名稱。 |
| jarLinkedService |Azure 儲存體連結服務，其中包含 hello jar 檔案。 這項連結的服務是指 toohello hello HDInsight 叢集相關聯的存放裝置。 |
| arguments |hello wordcount 程式會採用兩個引數、 輸入和輸出。 hello 輸入的檔是 hello 而 davinci.txt 檔案。 |
| frequency/interval |這些屬性的 hello 值符合 hello 輸出資料集。 |
| linkedServiceName |是指您稍早建立的 toohello HDInsight 連結的服務。 |

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

## <a name="run-spark-programs"></a>執行 Spark 程式
您可以使用 MapReduce 活動 toorun Spark 程式 HDInsight Spark 叢集上。 如需詳細資訊，請參閱 [從 Azure Data Factory 叫用 Spark 程式](data-factory-spark.md) 。  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>另請參閱
* [Hive 活動](data-factory-hive-activity.md)
* [Pig 活動](data-factory-pig-activity.md)
* [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
* [叫用 Spark 程式](data-factory-spark.md)
* [叫用 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

