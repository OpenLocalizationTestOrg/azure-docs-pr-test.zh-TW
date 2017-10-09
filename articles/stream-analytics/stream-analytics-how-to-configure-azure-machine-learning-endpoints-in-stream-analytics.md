---
title: "在 Stream Analytics aaaUse Azure Machine Learning 端點 |Microsoft 文件"
description: "串流分析中的機器語言使用者定義函式"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a>在串流分析中整合機器學習服務
串流分析支援呼叫 tooAzure 機器學習端點的使用者定義函數。 這項功能的 REST API 支援會詳細說明 hello[資料流分析 REST API 文件庫](https://msdn.microsoft.com/library/azure/dn835031.aspx)。 本文提供要在串流分析中成功實作這項功能所需的補充資訊。 您也可以在 [這裡](stream-analytics-machine-learning-integration-tutorial.md)取得已發佈的教學課程。

## <a name="overview-azure-machine-learning-terminology"></a>概觀：Azure Machine Learning 術語
Microsoft Azure Machine Learning 提供共同作業、 拖放的工具，您可以使用 toobuild、 測試及部署您的資料的預測分析解決方案。 此工具會呼叫 hello *Azure Machine Learning Studio*。 hello studio 是以 hello 使用的 toointeract 機器學習資源和輕鬆建置、 測試及逐一查看設計。 這些資源和其定義如下。

* **工作區**: hello*工作區*會保留所有其他機器學習資源集中管理及控制容器的容器。
* **實驗**:*實驗*資料科學家 tooutilize 資料集所建立並定型的機器學習模型。
* **端點**:*端點*會做為輸入 hello Azure 機器學習使用物件 tootake 功能、 適用於指定的機器學習模型，再傳回評分的輸出。
* **評分 Web 服務**： *評分 Web 服務* 是上述端點的集合。

每個端點都有適用於批次執行和同步執行的 API。 串流分析使用同步執行。 hello 特定服務的名稱為[要求/回應服務](../machine-learning/machine-learning-consume-web-services.md)AzureML studio 中。

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>串流分析作業所需的機器學習服務資源
基於 hello 資料流分析作業正在處理的要求/回應端點， [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)，而且 swagger 定義所有必要才能成功執行。 資料流分析已建構 hello swagger 端點 url、 查詢 hello 介面並傳回預設 UDF 定義 toohello 使用者的其他端點。

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>透過 REST API 設定串流分析和機器學習服務 UDF
使用 REST Api，您可以設定工作 toocall Azure 機器語言函式。 hello 步驟如下所示：

1. 建立串流分析工作
2. 定義輸入
3. 定義輸出
4. 建立使用者定義函式 (UDF)
5. 寫入資料流分析轉換呼叫 hello UDF
6. 啟動 hello 工作

## <a name="creating-a-udf-with-basic-properties"></a>使用基本屬性建立 UDF
例如，下列範例程式碼的 hello 建立名為的純量 UDF *newudf* tooan Azure Machine Learning 端點繫結。 請注意該 hello*端點*（服務 URI） 可以選擇服務和 hello hello hello API 說明頁面上找到*apiKey* hello 服務主頁面上可以找到。

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

要求本文範例：  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>呼叫預設 UDF 的 RetrieveDefaultDefinition 端點
一次 hello hello hello UDF 需要完整定義會建立 UDF 的基本架構。 hello RetreiveDefaultDefinition 端點可協助您取得繫結的 tooan Azure Machine Learning 端點的純量函式的 hello default 定義。 hello 裝載下列需要您 tooget hello 預設 UDF 定義繫結的 tooan Azure Machine Learning 端點的純量函式。 它不會指定 hello 實際的端點，因為它已經提供在 PUT 要求。 資料流分析呼叫 hello hello 要求中提供，如果提供明確的端點。 否則它會使用原本所參考的其中一個 hello。 這裡 hello UDF 會接受單一字串參數 （句子），並傳回表示該句子 hello 「 情緒"標籤字串類型的單一輸出。

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

要求本文範例：  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

此項目的範例輸出會看起來像下面這樣。  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a>修補程式 UDF hello 回應
現在 hello UDF 必須先安裝修補與前一個回應 hello，如下所示。

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

要求本文 (RetrieveDefaultDefinition 的輸出)：

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>實作資料流分析轉換 toocall hello UDF
現在每個輸入的事件查詢 hello UDF （以下稱為 scoreTweet），以及撰寫該事件 tooan 輸出的回應。  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
