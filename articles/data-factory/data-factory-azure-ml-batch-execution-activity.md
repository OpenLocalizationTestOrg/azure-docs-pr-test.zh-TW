---
title: "使用 Azure Data Factory aaaCreate 預測的資料管線 |Microsoft 文件"
description: "描述如何 toocreate 建立預測管線使用 Azure Data Factory 和 Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>使用 Azure Machine Learning 和 Azure Data Factory 來建立預測管線

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

## <a name="introduction"></a>簡介

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)可讓您 toobuild 測試和部署的預測分析解決方案。 從高階觀點而言，由下列三個步驟完成這個動作：

1. **建立訓練實驗**。 您可以使用 hello Azure ML Studio，以進行此步驟。 hello ML studio 是共同作業視覺式開發環境，您使用 tootrain 和測試模型使用定型資料的預測分析。
2. **將它轉換 tooa 預測實驗**。 一旦您的模型已定型使用現有的資料，而且您準備好 toouse 它 tooscore 新資料準備，並簡化計分實驗。
3. **將其部署為 Web 服務**。 只要按一下，您就可以將評分實驗當做 Azure Web 服務發佈。 您可以傳送資料 tooyour 模型，透過此 web 服務端點，並接收從 hello 模型結果的預測。  

### <a name="azure-data-factory"></a>Azure Data Factory
Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello**移動**和**轉換**的資料。 您可以建立資料整合方案使用 Azure Data Factory 可以擷取從各種資料存放區的資料，轉換/處理序 hello 資料，並將發行 hello 結果資料 toohello 資料存放區。

資料處理站服務 toocreate 資料管線，而移動和轉換資料，可讓您，然後再執行指定的排程 （每小時、 每天、 每週等等） 上的 hello 管線。 它也提供豐富的視覺效果 toodisplay hello 歷程和您的資料管線之間的相依性監視所有您在資料管線，從單一統一的檢視 tooeasily 找出問題並設定監視警示。

請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)和[建置您的第一個管線](data-factory-build-your-first-pipeline.md)文章 tooquickly 開始 hello Azure Data Factory 服務使用。

### <a name="data-factory-and-machine-learning-together"></a>Data Factory 和 Machine Learning 一起合作
Azure Data Factory 可讓您 tooeasily 建立使用已發行的管線[Azure Machine Learning] [ azure-machine-learning] web 服務的預測分析。 使用 hello**批次執行活動**在 Azure Data Factory 管線中，您可以叫用 Azure ML web 服務 toomake 預測 hello 批次中的資料。 請參閱[叫用 Azure ML web 服務使用 hello 批次執行活動](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity)如需詳細資訊。

經過一段時間，在 hello Azure ML 計分實驗中的 hello 預測模型需要 toobe 原樣使用新的輸入資料集。 您可以執行下列步驟的 hello 重新訓練從 Data Factory 管線的 Azure ML 模型：

1. 將 hello 定型實驗 （不預測實驗） 發佈為 web 服務。 您可以如同 tooexpose 預測實驗為 web 服務在 hello 前一個案例中，您 hello Azure ML Studio 中的這個步驟。
2. 使用 hello Azure ML 批次執行活動 tooinvoke hello web 服務的 hello 定型實驗。 基本上，您可以使用 hello Azure ML 批次執行活動 tooinvoke web 服務的定型和計分 web 服務。

您完成定型之後，更新 hello 計分 web 服務 （預測實驗公開為 web 服務） 與 hello 定型新模型，使用 hello **Azure ML 更新資源活動**。 如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>使用批次執行活動來叫用 Web 服務
您使用 Azure Data Factory tooorchestrate 資料移動和處理，並執行使用 Azure Machine Learning 批次執行。 Hello 最上層步驟如下：

1. 建立 Azure Machine Learning 連結服務。 您需要下列值的 hello:

   1. **要求 URI** hello 批次執行應用程式開發介面。 您可以找到要求的 URI hello 按一下 hello**批次執行**hello web 服務 頁面中的連結。
   2. **API 金鑰**hello 已發行的 Azure Machine Learning web 服務。 您可以按一下 hello 已發行的 web 服務，以尋找 hello API 金鑰。
   3. 使用 hello **AzureMLBatchExecution**活動。

      ![機器學習服務儀表板](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![批次 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>案例： 實驗使用 Web 服務輸入/輸出參考 Azure Blob 儲存體 toodata
在此案例中，hello Azure 機器學習 Web 服務會使用 Azure blob 儲存體中的檔案中的資料做出預測，並將 hello blob 儲存體中的 hello 預測結果。 hello 下列 JSON 定義與 AzureMLBatchExecution 活動的 Data Factory 管線。 hello 活動有 hello 集**DecisionTreeInputBlob**做為輸入和**DecisionTreeResultBlob**做為 hello 輸出。 hello **DecisionTreeInputBlob**被當做輸入的 toohello web 服務，方法是使用 hello **webServiceInput** JSON 屬性。 hello **DecisionTreeResultBlob**被當做輸出 toohello Web 服務，方法是使用 hello **webServiceOutputs** JSON 屬性。  

> [!IMPORTANT]
> 如果 hello web 服務接受多個輸入，使用 hello **webServiceInputs**屬性，而不要使用**webServiceInput**。 請參閱 hello [Web 服務需要多個輸入](#web-service-requires-multiple-inputs)> 一節使用 hello webServiceInputs 屬性的範例。
>
> 資料集所參考的 hello **webServiceInput**/**webServiceInputs**和**webServiceOutputs**屬性 (在**typeProperties**) 也必須包含在 hello 活動**輸入**和**輸出**。
>
> 在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。 您使用 webServiceInputs、 webServiceOutputs，和 globalParameters 設定 hello 名稱必須完全符合 hello 實驗中的 hello 名稱。 您可以在 Azure ML 端點 tooverify hello 預期對應 hello 批次執行說明頁面上檢視 hello 範例要求裝載。
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> 只有輸入及輸出的 hello AzureMLBatchExecution 活動可以傳遞為參數 toohello Web 服務。 例如，在 JSON 片段上方 hello，DecisionTreeInputBlob 是輸入的 toohello AzureMLBatchExecution 活動，以透過 webServiceInput 參數當做輸入的 toohello Web 服務。   
>
>

### <a name="example"></a>範例
這個範例會使用 Azure 儲存體 toohold 兩者 hello 輸入和輸出資料。

我們建議您通過 hello[建置您的第一個管線，使用 Data Factory] [ adf-build-1st-pipeline]再通過此範例中，教學課程。 在此範例中使用 hello Data Factory 編輯器 toocreate Data Factory 成品連結的服務、 資料集 （管線）。   

1. 為您的 **Azure 儲存體**建立**連結服務**。 如果 hello 輸入和輸出檔案位於不同的儲存體帳戶，您需要兩個連結的服務。 以下是 JSON 範例：

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. 建立 hello**輸入**Azure Data Factory**資料集**。 與某些其他 Data Factory 資料集不同的是，這些資料集必須同時包含 **folderPath** 和 **fileName** 值。 您可以使用資料分割 toocause 每個批次執行 （每一個資料配量） tooprocess 或產生唯一的輸入和輸出檔。 您可能需要的 tooinclude 某些上游活動 tootransform hello 輸入 hello CSV 檔案格式，並將它放在每個配量的 hello 儲存體帳戶。 在此情況下，您不會加入 hello**外部**和**externalData**顯示 hello 下列在範例中和您 DecisionTreeInputBlob 會 hello 的不同活動的輸出資料集設定。

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    您輸入的 csv 檔案必須有 hello 欄標題列。 如果您使用 hello**複製活動**toocreate/移動到 hello blob 儲存體 hello csv，您應該設定 hello 接收屬性**blobWriterAddHeader**太**true**。 例如：

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    如果 hello csv 檔案並沒有 hello 標頭資料列，您可能會看到下列錯誤 hello:**活動中的錯誤： 讀取字串時發生錯誤。非預期的權杖：StartObject。路徑 ''、行 1、位置 1**。
3. 建立 hello**輸出**Azure Data Factory**資料集**。 這個範例會使用每個配量執行分割 toocreate 唯一的輸出路徑。 沒有資料分割的 hello，hello 活動會覆寫 hello 檔。

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. 建立**連結服務**的型別： **AzureMLLinkedService**、 提供 hello API 金鑰，以及模型批次執行 URL。

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. 最後，撰寫一個包含 **AzureMLBatchExecution** 活動的管線。 在執行階段，管線會執行下列步驟的 hello:

   1. 從您的輸入資料集取得 hello hello 輸入檔的位置。
   2. 叫用 hello Azure Machine Learning 批次執行應用程式開發介面
   3. 複製 hello 在輸出資料集中指定的批次執行輸出 toohello blob。

      > [!NOTE]
      > AzureMLBatchExecution 活動可以有零個或多個輸入，以及一個或多個輸出。
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      **開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2014-10-14T16:32:41Z。 hello**結束**次為選擇性。 如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時。**" 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。 如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。

      > [!NOTE]
      > 指定 hello AzureMLBatchExecution 活動的輸入是選擇性的。
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>案例： 實驗不同的儲存體中使用讀取器/寫入器模組 toorefer toodata
建立 Azure ML 實驗時的另一個常見案例是 toouse 讀取器和寫入器模組。 hello 讀取器模組是使用的 tooload 實驗資料而 hello 編寫器模組 toosave 將實驗中的資料。 如需讀取器和寫入器模組的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。     

使用時 hello 讀取器和寫入器模組，它是很好的作法 toouse 這些讀取器/寫入器模組的每一個屬性的 Web 服務參數。 這些 web 參數可讓您 tooconfigure hello 值在執行階段。 例如，建立實驗時，您可以利用讀取器模組使用 Azure SQL Database：XXX.database.windows.net。 Hello web 服務完成部署之後，您要的 hello web 服務 toospecify tooenable hello 取用者呼叫 YYY.database.windows.net 另一個 Azure SQL Server。 您可以使用 Web 服務參數 tooallow 設定此值 toobe。

> [!NOTE]
> Web 服務的輸入和輸出與 Web 服務參數不同。 在 hello 第一個案例中，您已經知道如何為 Azure ML Web 服務指定為輸入及輸出。 在此案例中，您可以將 Web 服務對應 tooproperties 的讀取器/寫入器模組的參數來傳遞。
>
>

讓我們看看使用 Web 服務參數的案例。 您有已部署的 Azure Machine Learning web 服務使用其中一個支援的 Azure Machine Learning hello 資料來源的讀取器模組 tooread 資料 (例如： Azure SQL Database)。 執行 hello 批次執行之後，hello 結果會寫入使用 (Azure SQL Database) 寫入器模組。  Hello 實驗中定義任何 web 服務輸入及輸出。 在此情況下，我們建議您設定 hello 讀取器和寫入器模組的相關 web 服務參數。 此設定可讓使用 hello AzureMLBatchExecution 活動時，設定模組 toobe hello 讀取器/寫入器。 您指定 Web 服務參數在 hello **globalParameters**區段 hello 活動 JSON 中，如下所示。

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

您也可以使用[Data Factory 函數](data-factory-functions-variables.md)傳遞值 hello Web 服務參數 hello 下列範例所示：

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> hello Web 服務參數會區分大小寫，因此請確定您指定在 hello 活動中的 hello 名稱 JSON 符合 hello hello Web 服務所公開的。
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>使用讀取器模組 tooread 資料從 Azure Blob 中的多個檔案
具有 Pig 和 Hive 等活動的巨量資料管線可以產生沒有副檔名的一個或多個輸出檔案。 例如，當您指定外部的 Hive 資料表，hello hello 外部的 Hive 資料表的資料可以儲存在 Azure blob 儲存體以下列名稱 000000_0 hello。 您可以使用在實驗 tooread hello 讀取器模組的多個檔案，並用於預測。

當使用 hello 讀取器模組在 Azure 機器學習實驗中，您可以指定 Azure Blob 做為輸入。 hello Azure blob 儲存體中的 hello 檔案可以是 hello 輸出檔案 (範例： 000000_0)，在 HDInsight 上執行 Pig 和 Hive 指令碼所產生。 hello 讀取器模組可讓您 tooread 副檔名的檔案 （無） 藉由設定 hello**路徑 toocontainer、 目錄/blob**。 hello**路徑 toocontainer**點 toohello 容器和**目錄/blob**點 toofolder hello 檔案所在 hello 下列影像所示。 也就是星號 hello \*)**指定所有 hello hello 容器/資料夾中的檔案 (也就是資料/aggregateddata/年 = 6-2014年/月 /\*)** hello 實驗中讀取。

![Azure Blob 屬性](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>範例
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>AzureMLBatchExecution 活動使用 Web 服務參數的管線

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

在上述範例 JSON hello:

* hello 部署 Azure 機器學習 Web 服務會使用讀取器和寫入器模組 tooread/寫入資料，從 / tooan Azure SQL Database。 此 Web 服務會公開下列四個參數的 hello： 資料庫伺服器名稱、 資料庫名稱、 伺服器使用者帳戶名稱，以及伺服器的使用者帳戶密碼。  
* **開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2014-10-14T16:32:41Z。 hello**結束**次為選擇性。 如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時。**" 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。 如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。

### <a name="other-scenarios"></a>其他案例
#### <a name="web-service-requires-multiple-inputs"></a>Web 服務需要多個輸入
如果 hello web 服務接受多個輸入，使用 hello **webServiceInputs**屬性，而不要使用**webServiceInput**。 資料集所參考的 hello **webServiceInputs**也必須包含在 hello 活動**輸入**。

在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。 您使用 webServiceInputs、 webServiceOutputs，和 globalParameters 設定 hello 名稱必須完全符合 hello 實驗中的 hello 名稱。 您可以在 Azure ML 端點 tooverify hello 預期對應 hello 批次執行說明頁面上檢視 hello 範例要求裝載。

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Web 服務不需要輸入
Azure ML 批次執行 web 服務可以是任何工作流程使用的 toorun，例如 R 或 Python 指令碼，可能不需要任何輸入。 或者，hello 實驗可能不會公開任何 GlobalParameters 讀取器模組以進行設定。 在此情況下，hello AzureMLBatchExecution 活動會設定如下：

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Web 服務不需要輸入/輸出
hello Azure ML 批次執行 web 服務可能沒有設定任何 Web 服務輸出。 在此範例中，沒有任何 Web 服務輸入或輸出，也不會設定任何 GlobalParameters。 仍有本身，hello 活動上設定的輸出，但它不指定為 webServiceOutput。

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web 服務會使用讀取器和寫入器，和其他活動成功時，才 hello 活動執行
hello Azure ML web 服務讀取器和寫入器模組可能會設定的 toorun，不論任何 GlobalParameters。 不過，您可能想 tooembed 服務呼叫某些上游處理完成時，才會使用資料集相依性 tooinvoke hello 服務在管線中。 使用這種方式完成 hello 批次執行之後，您也可以觸發某些其他動作。 在此情況下，你可以使用活動輸入及輸出，但不命名它們其中任何一個為 Web 服務輸入或輸出的 hello 相依性。

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

hello**心得**是：

* 如果您的實驗端點使用 webServiceInput： 它由 blob 資料集，並納入 hello 活動輸入] 和 [hello webServiceInput 屬性。 否則，會省略 hello webServiceInput 屬性。
* 如果您的實驗端點使用 webServiceOutput(s)： 它們由 blob 資料集，且會包含在 hello 活動輸出以及 hello webServiceOutputs 屬性中。 hello 活動會輸出和 webServiceOutputs hello hello 實驗中的每個輸出名稱對應。 否則，會省略 hello webServiceOutputs 屬性。
* 如果您的實驗端點公開 globalParameter(s)，會收到 hello 活動 globalParameters 屬性中做為索引鍵的值組。 否則，會省略 hello globalParameters 屬性。 hello 索引鍵是區分大小寫。 [Azure Data Factory 函數](data-factory-functions-variables.md)可能用於 hello 值。
* 額外的資料集可能包含在 hello 活動輸入及輸出屬性，不含 hello 活動 typeProperties 中所參考。 這些資料集控管使用配量相依性的執行，但 hello AzureMLBatchExecution 活動會加以忽略。


## <a name="updating-models-using-update-resource-activity"></a>使用更新資源活動來更新模型
您完成定型之後，更新 hello 計分 web 服務 （預測實驗公開為 web 服務） 與 hello 定型新模型，使用 hello **Azure ML 更新資源活動**。 如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。

### <a name="reader-and-writer-modules"></a>讀取器和寫入器模組
使用 Web 服務參數的常見案例是 hello 使用 Azure SQL 讀取器和寫入器。 hello 讀取器模組已從 Azure Machine Learning Studio 以外的資料管理服務的實驗使用的 tooload 資料。 hello 寫入器模組是 toosave 資料到 Azure Machine Learning Studio 以外的資料管理服務將實驗中。  

如需 Azure Blob/Azure SQL 讀取器/寫入器的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。 hello 前一節中的 hello 範例使用 hello Azure Blob 讀取器和 Azure Blob 的寫入器。 本節討論如何使用 Azure SQL 讀取器和 Azure SQL 寫入器。

## <a name="frequently-asked-questions"></a>常見問題集
**問：** 我擁有巨量資料管線所產生的多個檔案。 可以使用 hello AzureMLBatchExecution 活動 toowork 所有 hello 檔案嗎？

**答：** 是。 請參閱 hello**使用讀取器模組 tooread 資料從 Azure Blob 中的多個檔案**如需詳細資訊。

## <a name="azure-ml-batch-scoring-activity"></a>AzureML 批次計分活動
如果您使用 hello **AzureMLBatchScoring**活動 toointegrate 與 Azure Machine Learning 中的，我們建議您使用 hello 最新**AzureMLBatchExecution**活動。

hello AzureMLBatchExecution 活動 hello 2015 年 8 月發行的 Azure SDK 和 Azure PowerShell 中引進。

如果您想 toocontinue 使用 hello AzureMLBatchScoring 活動，請繼續閱讀本節。  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>使用 Azure 儲存體進行輸入/輸出的 AzureML 批次計分活動

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Web 服務參數
新增 Web 服務參數，toospecify 值**typeProperties**區段 toohello **AzureMLBatchScoringActivty** > 一節中 hello 管線 JSON hello 下列範例所示：

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
您也可以使用[Data Factory 函數](data-factory-functions-variables.md)傳遞值 hello Web 服務參數 hello 下列範例所示：

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> hello Web 服務參數會區分大小寫，因此請確定您指定在 hello 活動中的 hello 名稱 JSON 符合 hello hello Web 服務所公開的。
>
>

## <a name="see-also"></a>另請參閱
* [Azure 部落格文章：開始使用 Azure Data Factory 和 Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
