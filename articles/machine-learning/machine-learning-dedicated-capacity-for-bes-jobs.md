---
title: "機器學習批次執行服務作業的容量 aaaDedicated |Microsoft 文件"
description: "適用於 Machine Learning 作業的 Azure Batch 服務概觀。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>適用於 Machine Learning 作業的 Azure Batch 服務

機器學習批次集區處理 hello Azure 機器學習批次執行服務可提供客戶管理的小數位數。 機器學習的傳統批次處理發生在多租用戶環境中，並行處理作業，您可以提交，且作業哪些限制 hello 數目會排入佇列以先進先出為基礎。 這種不確定性，表示您無法準確地預測何時會執行您的作業。

批次集區處理可讓您 toocreate 集區，您可以提交批次作業。 控制 hello hello 集區的大小，而且 toowhich 集區 hello 作業傳送。 BES 工作會執行自己的處理空間提供可預測的處理效能和 hello 能力 toocreate 資源集區對應 toohello 您送出的處理負載。

## <a name="how-toouse-batch-pool-processing"></a>如何 toouse 批次集區處理

無法透過 hello Azure 入口網站目前可用的批次進行處理集區設定。 toouse 批次集區處理，您必須：

-   呼叫 CSS toocreate 批次集區帳戶，並取得集區服務 URL 和授權金鑰
-   建立新的 Resource Manager 型 Web 服務和計費方案

toocreate 您的帳戶，呼叫 Microsoft 客戶服務及支援 (CSS)，並提供您的訂用帳戶識別碼。 CSS 將適用於您 toodetermine hello 適當容量，以您的案例。 然後，CSS 會設定您的帳戶與 hello 集區，您可以建立並 hello 可以在每個集區的虛擬機器 (Vm) 的最大數目的數目上限。 設定您的帳戶後，您便會取得集區服務 URL 和授權金鑰。

建立您的帳戶之後，您會使用 hello 集區服務 URL 和授權金鑰 tooperform 集區上的管理作業批次集區。

![批次集區服務架構。](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

您可以呼叫該 CSS 提供 tooyou hello hello 集區服務 URL 建立集區作業建立集區。 當您建立一個集區時，指定的 Vm 和 hello hello swagger.json 新資源管理員的 URL 的 hello 數目基礎的機器學習 web 服務。 此 web 服務提供 tooestablish hello 計費關聯。 hello 批次集區服務會使用計費的方案中的 hello swagger.json tooassociate hello 集區。 您可以執行任何 BES web 服務，這兩個新的資源管理員，以基礎而且傳統，您選擇 hello 集區上。

您可以使用任何基礎的新資源管理員的 web 服務，但請留意 hello 計費 hello 工作負責針對 hello 與該服務相關聯的計費方案。 您可能想的 toocreate web 服務和新的計費計劃，專門用來執行批次集區工作。

如需關於建立 Web 服務的詳細資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

當您建立集區之後時，您送出 hello BES hello web 服務工作使用 hello 批次要求的 URL。 您可以選擇 toosubmit 它 tooa 集區或 tooclassic 批次的處理。 toosubmit 作業 tooBatch 集區處理，您會加入下列參數 toohello 工作提交要求主體的 hello:

"AzureBatchPoolId":"&lt;pool ID&gt;"

如果您不需要新增 hello 參數，hello 作業會執行 hello 傳統的批次的處理序環境中。 如果 hello 集區有可用的資源，會啟動 hello 工作立即執行。 如果 hello 集區沒有可用的資源，您的工作會排入佇列，直到有可用的資源。

如果您發現，定期連線到您的集區的 hello 容量，您需要更高的容量，您可以連絡 CSS，並使用代表性 tooincrease 您的配額。

範例要求︰

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>使用批次集區處理時的考量

批次進行處理集區是一直在計費服務，而且這需要您 tooassociate 它與資源管理員內以計費方案。 您僅支付 hello 時數計算 hello 集區正在執行;不論 hello 期間該階段集區執行的作業數目。 如果您建立一個集區，您所要支付 hello 運算時數的 hello 集區中每個虛擬機器直到刪除為止 hello 集區，即使 hello 集區中執行任何批次工作。 計費 hello 虛擬機器的佈建完成時啟動，並停止時已被刪除。 您可以使用任何 hello hello 上找不到方案[機器學習定價頁面](https://azure.microsoft.com/pricing/details/machine-learning/)。

計費範例︰

如果您建立包含 2 部虛擬機器的批次集區，並在 24 小時後將它刪除，您的計費方案會借記 48 個計算小時；不論該期間內執行了多少作業。

如果您建立包含 4 部虛擬機器的批次集區，並在 12 小時後將它刪除，您的計費方案也會借記 48 個計算小時。

我們建議您輪詢 hello 作業狀態 toodetermine，當工作完成。 當所有的作業完成執行時，呼叫 hello 調整集區大小作業 tooset hello 數目 hello 集區 toozero 中的虛擬機器。 如果您是簡短的資源集區，而且您需要 toocreate 新的集區，例如 toobill 針對不同的計費方案，您可以刪除 hello 集區改為所有的作業完成執行。


| **使用批次集區處理的時機**    | **使用傳統批次處理的時機**  |
|---|---|
|您需要 toorun 大量作業<br>或<br/>您需要您的作業會立即執行的 tooknow<br/>或<br/>您需要保證的輸送量。 例如，您需要 toorun 中指定的時間範圍內，作業數目，並想 tooscale 您計算資源 toomeet 出您的需求。    | 您正在執行一些作業<br/>和<br/> 您不立即需要 hello 作業 toorun |
