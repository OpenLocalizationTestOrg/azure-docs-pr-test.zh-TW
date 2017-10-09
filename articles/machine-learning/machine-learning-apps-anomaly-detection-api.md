---
title: "機器學習異常偵測 API aaaAzure |Microsoft 文件"
description: "「異常偵測 API」是一個搭配 Microsoft Azure Machine Learning 建置的範例，此 API 使用固定時間間隔的數值，偵測時間序列資料中的異常狀況。"
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>Machine Learning 異常偵測 API
## <a name="overview"></a>概觀
[異常偵測 API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) 是一個搭配 Azure Machine Learning 建置的範例，此 API 使用固定時間間隔的數值，偵測時間序列資料中的異常狀況。

此 API 可偵測下列類型的異常模式時間序列資料中的 hello:

* **正向和負向趨勢**：例如，在監視運算中所使用的記憶體數量時，趨勢向上可能會引起您的注意，因為這可能表示有記憶體流失。
* **Hello 動態範圍內的值變更**： 例如，監視時所擲回的雲端服務的 hello 例外狀況，值 hello 動態範圍中的任何變更可能表示不穩定的 hello 服務的 hello 健全狀況和
* **升高和畫 Dip**： 例如，監視時 hello 數目在服務中的登入失敗或簽出的電子商務網站中的數字，如果看到爆增情形或 dip 可能表示異常行為。

這些 Machine Learning 偵測器會追蹤數值在不同時間所發生的這一類變化，並以異常分數的形式報告數值正在進行的變化。 它們不需要調整特定閾值，及其分數可以是使用的 toocontrol false 正數的速率。 如同服務監視 Kpi 追蹤一段時間，使用數種案例中適合 hello 異常偵測應用程式開發介面透過度量資訊，例如數字的搜尋，數字的按鍵，監視效能監控計數器，例如記憶體、 CPU、 檔案透過讀取，經過一段時間等等。

hello 異常偵測供應項目隨附實用工具 tooget 您已啟動。

* hello [web 應用程式](http://anomalydetection-aml.azurewebsites.net/)可協助您評估，並將對資料的異常偵測應用程式開發介面的 hello 結果視覺化。

> [!NOTE]
> 請嘗試採用[這個 API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) 的 **IT 異常洞察解決方案**
> 
> tooget 這個端點 tooend 解決方案部署 tooyour Azure 訂用帳戶<a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank">**從這裡開始 >**</a>
> 
>

## <a name="api-deployment"></a>API 部署
在訂單 toouse hello API，您必須先部署 tooyour 它裝載為 Azure Machine Learning web 服務的 Azure 訂用帳戶。  您可以從 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)。  這會將部署兩個 AzureML Web 服務 （和其相關的資源） tooyour Azure 訂閱-一個季節性偵測的異常偵測，另一個不含季節性偵測。  Hello 部署完成後，請您將會無法 toomanage 從 Api hello [AzureML web 服務](https://services.azureml.net/webservices/)頁面。  從這個頁面上，您會將端點的位置，API 金鑰是可以 toofind 以及範例程式碼的呼叫 hello API。  在[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice)可取得更詳細的指示。

## <a name="scaling-hello-api"></a>調整 hello 應用程式開發介面
根據預設，部署將有免費的開發/測試計費方案，其中包括 1,000 筆交易/月和 2 個計算時數/月。  根據您的需求，您可以升級 tooanother 計劃。  上的不同的計劃的 hello 定價詳細資料可用[這裡](https://azure.microsoft.com/en-us/pricing/details/machine-learning/)下 」 定價生產環境 Web 應用程式開發介面 」。

## <a name="managing-aml-plans"></a>管理 AML 方案 
您可以在[這裡](https://services.azureml.net/plans/)管理您的計費方案。  hello 計劃名稱將會根據您選擇部署 hello API 時 hello 資源群組名稱加上唯一 tooyour 訂用帳戶的字串。  指示如何 tooupgrade 您計劃可用[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice)下 hello < 管理計費方案 > 一節。

## <a name="api-definition"></a>API 定義
hello web 服務提供 REST 型 API 透過 HTTPS，供不同的方式，包括 web 或行動應用程式，R、 Python、 Excel、 等等。傳送您的時間序列資料的 toothis 服務透過 REST API 呼叫，並且會執行 hello 如下所述三種異常類型的組合。

## <a name="calling-hello-api"></a>呼叫 hello API
在訂單 toocall hello API，您將需要 tooknow hello 端點位置和 API 金鑰。  這兩種，以及呼叫 hello API 的範例程式碼都是從 hello [AzureML web 服務](https://services.azureml.net/webservices/)頁面。  導覽 toohello 預期 API，然後按一下hello 「 取用 」 索引標籤 toofind 它們。  請注意，您可以呼叫 hello API 之 Swagger API (也就是與 hello URL 參數`format=swagger`) 或做為非-Swagger API (亦即，沒有 hello `format` URL 參數)。  hello 範例程式碼會使用 hello Swagger 格式。  以下是非 Swagger 格式的範例要求和回應。  這些範例是 toohello 季節性端點。  類似 hello 非季節性端點。

### <a name="sample-request-body"></a>範例要求本文
hello 要求包含兩個物件：`Inputs`和`GlobalParameters`。  在 hello 範例要求中下，某些參數就會傳送明確，有些則不 （向下捲動以每個端點參數的完整清單）。  Hello 要求中未明確傳送的參數會使用下面所列的 hello 預設值。

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>範例回應
請注意，在順序 toosee hello `ColumnNames`  欄位中，您必須包含`details=true`做為 URL 參數，在您的要求。  請參閱以下的每一個欄位背後的 hello 意義的 hello 資料表。

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>分數 API
hello 分數 API 用於非季節性的時間序列資料上執行的異常偵測。 hello API hello 資料上執行數目異常偵測器，並傳回其異常分數。 hello 下方圖的異常狀況範例分數 API 可以偵測到該 hello。 此時間序列有 2 個不同的層級變更和 3 個尖峰。 hello 紅點顯示 hello 時間在哪一個 hello 層級偵測到變更，而黑色 hello 點顯示 hello 偵測到的高峰。
![分數 API][1]

### <a name="detectors"></a>偵測器
hello 異常偵測應用程式開發介面支援 3 廣泛的類別中的偵測器。 Hello 下表中可以找到特定的輸入的參數及輸出的每個偵測器的詳細資訊。

| 偵測器類別 | 偵測器 | 說明 | 輸入參數 | 輸出 |
| --- | --- | --- | --- | --- |
| 尖峰偵測器 |TSpike 偵測器 |偵測如果看到爆增情形，並根據的值是從第一個和第三個四分位遠 hello dip |*tspikedetector.sensitivity:*採用 hello 範圍中的整數值 1-10，預設值： 3。較高的值將會攔截更多的極端值，使它的敏感性較低 |TSpike︰二進位值 - 如果偵測到尖峰/下降則為 ‘1’，否則為 ‘0’ |
| 尖峰偵測器 | ZSpike 偵測器 |偵測尖峰和 dip 根據伸展多遠 hello 資料都是來自平均數 |*zspikedetector.sensitivity:*採取 hello 範圍中的整數值 1-10，預設值： 3。較高的值將會攔截多個進行的敏感性較低的極端值 |ZSpike︰二進位值 - 如果偵測到尖峰/下降則為 ‘1’，否則為 ‘0’ | |
| 緩慢趨勢偵測器 |緩慢趨勢偵測器 |偵測到慢的正值趨勢根據 hello 組敏感度 |*trenddetector.sensitivity:*上偵測器分數臨界值 (預設： 3.25，3.25 – 5 是合理的範圍 tooselect 從; hello 區分較高 hello) |tscore︰代表趨勢異常分數的浮動數字 |
| 層級變更偵測器 | 雙向層級變更偵測器 |偵測到依據 hello 組敏感度向上和向下層級變更 |*bileveldetector.sensitivity:*上偵測器分數臨界值 (預設： 3.25，3.25 – 5 是合理的範圍 tooselect 從; hello 區分較高 hello) |rpscore︰代表向上和向下層級變更異常分數的浮動數字 | |

### <a name="parameters"></a>參數
在 hello 表中列出這些輸入參數的詳細的資訊：

| 輸入參數 | 說明 | 預設設定 | 類型 | 有效範圍 | 建議範圍 |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |用於計算異常分數的歷程記錄 (以資料點數目為單位) |500 |integer |10 - 2000 |取決於時間序列 |
| detectors.spikesdips | 是否 toodetect 只升高、 唯一的 dip，或兩者 |兩者 |列舉 |兩者、尖峰、下降 |兩者 |
| bileveldetector.sensitivity |雙向層級變更偵測器的敏感度。 |3.25 |double |None |3.25-5 (值愈低代表敏感度越高) |
| trenddetector.sensitivity |正向趨勢偵測器的敏感度。 |3.25 |double |None |3.25-5 (值愈低代表敏感度越高) |
| tspikedetector.sensitivity |TSpike 偵測器的敏感度 |3 |integer |1 - 10 |3-5 (值愈低代表敏感度越高) |
| zspikedetector.sensitivity |ZSpike 偵測器的敏感度 |3 |integer |1 - 10 |3-5 (值愈低代表敏感度越高) |
| postprocess.tailRows |數目 hello 最新的資料點 toobe 保留在 hello 輸出結果 |0 |integer |0 （保留所有資料點），或在結果中指定的點 tookeep 數目 |N/A |

### <a name="output"></a>輸出
hello API 對時間序列資料執行所有的偵測器並傳回異常分數與每個點的二進位突然增加指標中的時間。 hello 下表列出從 hello 應用程式開發介面的輸出。 

| 輸出 | 說明 |
| --- | --- |
| 時間 |未經處理資料或彙總 (和/或) 插補資料 (如果套用彙總 (和/或) 遺漏資料插補) 的時間戳記 |
| 資料 |未經處理資料或彙總 (和/或) 插補資料 (如果套用彙總 (和/或) 遺漏資料插補) 的值 |
| TSpike |二元指標 tooindicate 是否突然增加，而偵測到 TSpike 偵測器 |
| ZSpike |二元指標 tooindicate 是否突然增加，而偵測到 ZSpike 偵測器 |
| rpscore |代表雙向層級變更異常分數的浮動數字 |
| rpalert |1/0 值，指出雙向層級變更異常根據 hello 輸入大小寫 |
| tscore |代表正向趨勢異常分數的浮動數字 |
| talert |1/0 的值，指出有是根據 hello 輸入大小寫的正值趨勢異常 |

## <a name="scorewithseasonality-api"></a>ScoreWithSeasonality API
hello ScoreWithSeasonality API 用於具有季節性模式的時間序列上執行的異常偵測。 這個 API 已有用 toodetect 差季節性模式中。  
hello 下圖顯示季節性的時間序列中偵測到異常狀況的範例。 hello 時間序列有一個特殊圖文集 （hello 第 1 個黑色點）、 兩個 dip （hello 第 2 個黑色的點，一個 hello 結尾） 和一個層級變更 （紅點）。 請注意，兩者 hello hello 中間 hello 時間序列的 dip 季節性元件 hello 數列中移除後，才明顯 hello 層級變更。
![季節性 API][2]

### <a name="detectors"></a>偵測器
hello 季節性端點中的 hello 偵測器會類似 toohello 的 hello 非季節性端點，但稍微不同的參數名稱 （如下所示）。

### <a name="parameters"></a>參數

在 hello 表中列出這些輸入參數的詳細的資訊：

| 輸入參數 | 說明 | 預設設定 | 類型 | 有效範圍 | 建議範圍 |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |用來彙總輸入時間序列的彙總間隔 (秒) |0 (不執行彙總) |integer |0︰略過彙總，否則 > 0 |5 分鐘 too1 天，時間序列相依 |
| preprocess.aggregationFunc |使用資料彙總成 hello 函式指定 AggregationInterval |平均值 |列舉 |平均值、總和、長度 |N/A |
| preprocess.replaceMissing |使用 tooimpute 遺失的資料值。 |lkv (上一個已知值) |列舉 |零、lkv、平均值 |N/A |
| detectors.historyWindow |用於計算異常分數的歷程記錄 (以資料點數目為單位) |500 |integer |10 - 2000 |取決於時間序列 |
| detectors.spikesdips | 是否 toodetect 只升高、 唯一的 dip，或兩者 |兩者 |列舉 |兩者、尖峰、下降 |兩者 |
| bileveldetector.sensitivity |雙向層級變更偵測器的敏感度。 |3.25 |double |None |3.25-5 (值愈低代表敏感度越高) |
| postrenddetector.sensitivity |正向趨勢偵測器的敏感度。 |3.25 |double |None |3.25-5 (值愈低代表敏感度越高) |
| negtrenddetector.sensitivity |負向趨勢偵測器的敏感度。 |3.25 |double |None |3.25-5 (值愈低代表敏感度越高) |
| tspikedetector.sensitivity |TSpike 偵測器的敏感度 |3 |integer |1 - 10 |3-5 (值愈低代表敏感度越高) |
| zspikedetector.sensitivity |ZSpike 偵測器的敏感度 |3 |integer |1 - 10 |3-5 (值愈低代表敏感度越高) |
| seasonality.enable |季節性分析是否 toobe 執行 |true |布林值 |true、false |取決於時間序列 |
| seasonality.numSeasonality |定期循環 toobe 偵測到的最大數目 |1 |integer |1、2 |1 - 2 |
| seasonality.transform |在套用異常偵測之前，是否應該移除季節性 (和) 趨勢元件 |deseason |列舉 |無、deseason、deseasontrend |N/A |
| postprocess.tailRows |數目 hello 最新的資料點 toobe 保留在 hello 輸出結果 |0 |integer |0 （保留所有資料點），或在結果中指定的點 tookeep 數目 |N/A |

### <a name="output"></a>輸出
hello API 對時間序列資料執行所有的偵測器並傳回異常分數與每個點的二進位突然增加指標中的時間。 hello 下表列出從 hello 應用程式開發介面的輸出。 

| 輸出 | 說明 |
| --- | --- |
| 時間 |未經處理資料或彙總 (和/或) 插補資料 (如果套用彙總 (和/或) 遺漏資料插補) 的時間戳記 |
| OriginalData |未經處理資料或彙總 (和/或) 插補資料 (如果套用彙總 (和/或) 遺漏資料插補) 的值 |
| ProcessedData |Hello 下列其中一項： <ul><li>已進行季節性調整的時間序列 (在已偵測到明顯季節性並選取了 deseason 選項的前提下)</li><li>已進行季節性調整並去趨勢化的時間序列 (在已偵測到明顯季節性並選取了 deseasontrend 選項的前提下)</li><li>否則，這是 hello 與 OriginalData 相同</li> |
| TSpike |二元指標 tooindicate 是否突然增加，而偵測到 TSpike 偵測器 |
| ZSpike |二元指標 tooindicate 是否突然增加，而偵測到 ZSpike 偵測器 |
| BiLevelChangeScore |代表層級變更異常分數的浮動數字 |
| BiLevelChangeAlert |1/0 值，指出有是根據 hello 輸入大小寫層級變更異常 |
| PosTrendScore |代表正向趨勢異常分數的浮動數字 |
| PosTrendAlert |1/0 的值，指出有是根據 hello 輸入大小寫的正值趨勢異常 |
| NegTrendScore |代表負向趨勢異常分數的浮動數字 |
| NegTrendAlert |1/0 的值，指出有是根據 hello 輸入大小寫的負值趨勢異常 |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

