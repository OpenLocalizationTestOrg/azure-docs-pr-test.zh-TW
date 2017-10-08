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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>使用 Azure Data Factory 中的 Hadoop 資料流活動轉換資料
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

您可以使用 hello HDInsightStreamingActivity 活動叫用 Hadoop 串流工作從 Azure Data Factory 管線。 hello 下列 JSON 片段顯示在管線 JSON 檔案中使用 hello HDInsightStreamingActivity hello 語法。 

hello Data Factory 中的 HDInsight 串流活動[管線](data-factory-create-pipelines.md)上執行 Hadoop 串流程式[自己](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)或[隨](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)Windows/linux 的 HDInsight叢集。 這篇文章是根據 hello[資料轉換活動](data-factory-data-transformation-activities.md)發行項，其呈現的資料轉換和支援的 hello 轉換活動的一般概觀。

> [!NOTE] 
> 如果您是新 tooAzure Data Factory，閱讀[簡介 tooAzure Data Factory](data-factory-introduction.md)和執行 hello 教學課程：[建置您的第一個資料管線](data-factory-build-your-first-pipeline.md)閱讀本文之前。 

## <a name="json-sample"></a>JSON 範例
hello HDInsight 叢集會自動填入範例程式 （wc.exe 和 cat.exe） 和資料 (而 davinci.txt)。 根據預設，hello HDInsight 叢集所用的 hello 容器的名稱會是 hello 的 hello 叢集本身的名稱。 比方說，如果您的叢集名稱是 myhdicluster，hello 相關聯的 blob 容器的名稱將 myhdicluster。 

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

請注意下列點 hello:

1. 設定 hello **linkedServiceName** hello toohello 名稱連結點 tooyour HDInsight 叢集執行哪些 hello 串流 mapreduce 作業的服務。
2. 設定 hello hello 活動型別太**HDInsightStreaming**。
3. Hello**對應工具**屬性，指定 hello 的對應工具可執行檔的名稱。 在 hello 範例 cat.exe 會是 hello 對應工具可執行檔。
4. Hello**減壓器**屬性，指定減壓器可執行檔的 hello 名稱。 在 hello 範例 wc.exe 是 hello 減壓器可執行檔。
5. Hello**輸入**輸入屬性，指定 hello 對應工具的 hello 輸入的檔 （包括 hello 位置）。 在 hello 範例: 「 wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample 是 blob 容器，hello 範例/data/Gutenberg 是 hello 資料夾，而 davinci.txt 是 hello blob。
6. Hello**輸出**輸入屬性，指定減壓器 hello hello 輸出檔 （包括 hello 位置）。 hello hello Hadoop 串流工作輸出寫入 toohello 針對此屬性指定的位置。
7. 在 hello **filePaths**區段中，指定 hello hello 對應工具和減壓器可執行檔的路徑。 在 hello 範例:"adfsample/example/apps/wc.exe"，adfsample 是 hello blob 容器，example/apps 是 hello 資料夾和 wc.exe 是可執行檔的 hello。
8. Hello **fileLinkedService**屬性，指定 hello Azure 儲存體連結的服務代表 hello hello hello filePaths 區段中指定的檔案所在的 Azure 儲存體。
9. Hello**引數**屬性，指定資料流工作的 hello hello 引數。
10. hello **getDebugInfo**屬性是選擇性項目。 當它設定為 tooFailure 時，只在失敗下載 hello 記錄檔。 當它設定為 tooAlways 時，無論 hello 執行狀態永遠下載記錄檔。

> [!NOTE]
> Hello 範例所示，您指定的輸出資料集 hello Hadoop 資料流活動 hello**輸出**屬性。 此資料集是只空資料集是必要的 toodrive hello 管線的排程。 您不需要 toospecify 任何輸入資料集 hello 的 hello 活動**輸入**屬性。  
> 
> 

## <a name="example"></a>範例
本逐步解說中的 hello 管線執行 hello 字數統計資料流 Map/Reduce 程式 Azure HDInsight 叢集上。 

### <a name="linked-services"></a>連結的服務
#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
首先，您可以建立連結的服務 toolink hello Azure 儲存體，以供 hello Azure HDInsight 叢集的 toohello Azure data factory。 如果您複製/貼上下列程式碼的 hello，別忘了 tooreplace 帳戶名稱和帳戶金鑰 hello 名稱和您的 Azure 儲存體金鑰。 

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
接下來，您建立連結的服務 toolink Azure HDInsight 叢集 toohello Azure data factory。 如果您複製/貼上下列程式碼的 hello，以您的 HDInsight 叢集 hello 名稱取代 HDInsight 叢集名稱，並變更使用者名稱和密碼值。 

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
這個範例中的 hello 管線不接受任何輸入。 您指定 hello HDInsight 串流活動的輸出資料集。 此資料集是只空資料集是必要的 toodrive hello 管線的排程。 

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

### <a name="pipeline"></a>管線
在此範例中的 hello 管線有只有一個活動的型別： **HDInsightStreaming**。 

hello HDInsight 叢集會自動填入範例程式 （wc.exe 和 cat.exe） 和資料 (而 davinci.txt)。 根據預設，hello HDInsight 叢集所用的 hello 容器的名稱會是 hello 的 hello 叢集本身的名稱。 比方說，如果您的叢集名稱是 myhdicluster，hello 相關聯的 blob 容器的名稱將 myhdicluster。  

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
## <a name="see-also"></a>另請參閱
* [Hive 活動](data-factory-hive-activity.md)
* [Pig 活動](data-factory-pig-activity.md)
* [MapReduce 活動](data-factory-map-reduce.md)
* [叫用 Spark 程式](data-factory-spark.md)
* [叫用 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

