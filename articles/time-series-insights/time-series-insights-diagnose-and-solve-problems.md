---
title: "aaaDiagnose 並解決問題 |Microsoft 文件"
description: "本教學課程涵蓋如何 toodiagnose 並解決問題，在時間序列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>在 Time Series Insights 環境中診斷與解決問題

## <a name="i-dont-see-my-data"></a>我看不見我的資料
以下是一些原因為什麼您可能不會看到您的資料在您的環境中 hello [Azure 時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>您事件來源的資料不是 JSON 格式
Azure Time Series Insights 現在只支援 JSON 資料。 如需 JSON 範例，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>當您註冊事件來源時，您未提供具有 hello 所需的權限的 hello 金鑰
* IoT 中樞，您需要具有 tooprovide hello 金鑰**服務連線**權限。

   ![IoT 中樞服務連線權限](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   示 hello 前面映像，其中一個 hello 原則**iothubowner**和**服務**運作，因為兩者都有**服務連線**權限。
* 事件中心，您需要具有 tooprovide hello 金鑰**接聽**權限。

   ![事件中樞接聽權限](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   示 hello 前面映像，其中一個 hello 原則**讀取**和**管理**運作，因為兩者都有**接聽**權限。

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>hello 提供取用者群組不是獨占 tooTime 數列 Insights
IoT 中樞或事件中心，請在註冊期間我們需要您應該用來讀取資料的 toospecify hello 取用者群組。 不可共用此取用者群組。 如果它共用，基礎事件中心 hello 自動中斷連線 hello 讀取器的其中一個隨機。

## <a name="i-see-my-data-but-theres-a-lag"></a>我可以看到我的資料，但有延遲情形
以下是為什麼您可能會看到您的環境中 hello 的部分資料的原因[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。

### <a name="your-environment-is-getting-throttled"></a>您的環境正在進行節流
會強制執行節流限制的 hello，根據 hello 環境 SKU 類型和容量。 Hello 環境中的所有事件來源會都共用此容量。 如果 hello IoT 中心] 或 [事件中樞的事件來源是 hello 強制執行限制之外的資料，您會看到節流和延遲。

hello 下列圖表顯示的時間序列 Insights 環境具有 SKU S1 和 3 的容量。 該環境可以每日輸入 3 百萬個事件。

![環境 SKU 目前容量](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

假設此環境擷取自事件中心的訊息，以 hello 輸入速率 hello 下列圖表所示：

![事件中樞的範例輸入率](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Hello 圖表所示，每日輸入速率 hello 是 ~ 67,000 訊息。 此比率將轉譯大致 too46 訊息每隔一分鐘。 如果每個事件中樞的訊息是扁平化的 tooa 單一時間序列 Insights 事件，會看到此環境沒有節流。 如果每個事件中樞的訊息是扁平化的 too100 時間數列 Insights 事件，然後 4,600 事件應該被 ingested 每隔一分鐘。 容量為 3 的 S1 SKU 環境每分鐘只能輸入 2,100 個事件 (每天 1 百萬個事件 = 每 3 單位每分鐘 700 個事件 = 每分鐘 2,100 個事件)。 因此，您看到延隔時間到期 toothrottling。 

若要概略了解壓平合併邏輯的運作方式，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。

#### <a name="recommended-steps"></a>建議的步驟
toofix hello 延隔時間，增加 hello 環境的 SKU 容量。 如需詳細資訊，請參閱[如何 tooscale 時間數列 Insights 環境](time-series-insights-how-to-scale-your-environment.md)。

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>您正在推送歷程記錄資料並造成輸入緩慢
如果您正與現有事件來源連線，則您的 IoT 中樞或事件中樞裡可能已有資料。 因此 hello 環境啟動 hello 事件來源的訊息保留期限的 hello 開頭從中提取資料。 

此行為是 hello 預設行為，而且不能覆寫。 您可以進行節流，而且可能需要一段 toocatch 向上上擷取歷程記錄資料。

#### <a name="recommended-steps"></a>建議的步驟
toofix hello 延隔，採取下列步驟的 hello:
1. 增加 hello SKU 容量 toohello 最大允許值 (在本例中為 10)。 Hello 容量會增加之後，hello 輸入開始程序趕上進度更快。 您可以視覺化速度您正在趕上透過 hello 可用性圖表中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。 您必須支付 hello 增加容量。
2. Hello 延隔時間趕上之後，會降低 hello SKU 容量後 tooyour 一般輸入速率。

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>我的事件來源的時間戳記屬性名稱設定沒有作用
請確定 hello 名稱和值符合 toohello 下列規則：
* hello 時間戳記屬性名稱_區分大小寫_。
* hello 時間戳記屬性值，來自事件來源，為 JSON 字串時，應該具有 hello 格式_yyyy-MM-Yyyy-mm-ddthh。SS'.'FFFFFFFK_。 字串的範例如 “2008-04-12T12:53Z”。
