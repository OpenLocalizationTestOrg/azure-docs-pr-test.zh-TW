---
title: "Azure 時間數列深入解析的 aaaOverview |Microsoft 文件"
description: "簡介 tooAzure 時間數列深入解析，新的服務的時間序列資料分析和 IoT 解決方案"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>什麼是 Azure Time Series Insights

Azure 的時間序列 Insights 是使用儲存體、 分析和視覺效果元件可讓您輕鬆 tooingest、 儲存、 瀏覽及同時分析數十億個事件對受管理的雲端服務。 Time Series Insights 可讓您以全域方式檢視資料，這可協助您探索隱藏的趨勢和異常狀況，並近乎即時地執行根本原因分析，進而快速驗證 IoT 解決方案並避免代價高昂的裝置停機。 時間序列 Insights 內嵌事件仲介 （例如 IoT 中樞或事件中心） 從時間序列資料、 索引 hello 資料和淘汰時可設定的保留原則為基礎的資料。 使用者會使用透過直覺式的 UX 或 REST 查詢 Api 的 hello 資料。

![Time Series Insight 概觀](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>主要案例

* 在短短幾分鐘內監視和驗證 IoT 解決方案。
* 大規模視覺化和分析 IoT 資料。
* 加速進行根本原因分析和異常偵測。
* 建立含有多個裝置、工廠和資料的全域檢視。

## <a name="capabilities-and-benefits"></a>功能和優點

* **啟動的簡單 tooget**: Azure 時間數列 Insights 需要沒有足夠的事前資料準備工作，而且是非常快速地執行。 連接您的 Azure IoT 中樞或事件中心中的事件 toobillions 以分鐘為單位。 一旦連接之後，以視覺化方式檢視和與感應器資料互動，以秒為單位 tooquickly 驗證您的 IoT 解決方案。 時間序列 Insights 是簡單 toouse;您可以互動與您的資料，而不需要撰寫一行程式碼。  沒有任何新的語言 toolearn;時間序列 Insights 對於進階使用者，提供細微、 任意文字的查詢介面，並指向，然後按一下瀏覽所有。

* **接近即時的深入資訊**： 時間序列 Insights 可以內嵌數百萬個每日的感應器事件以一分鐘的延遲，因此您可以快速反應 toochanges。 Time Series Insights 協助您深入地了解感應器資料，它會協助您快速找出趨勢和異常狀況，進行複雜的根本原因分析，並避免耗費成本的停機時間。 藉由啟用交叉相互關聯之間即時和歷史資料，時間序列 Insights 可協助您解除鎖定隱藏的 hello 資料中的趨勢。

* **建置自訂解決方案**：將 Azure Time Series Insights 資料內嵌至現有應用程式，或使用 Time Series Insights REST API 建立新的自訂解決方案。 建立及共用個人化檢視，您可以共用其他 tooexplore 您探索。

* **延展性**： 時間序列 Insights 是大規模的設計的 toosupport IoT。 在預覽中，可以輸入從 1 百萬個 too100 百萬個事件每天，使用預設保留跨越的 31 天。 您可以用近乎即時的方式，來為即時資料流以及大量的歷史資料呈現視覺效果並對其進行分析。 向前移動，輸入與保留的速度將會增加 tooaccommodate 不斷演變的企業規模。

## <a name="time-series-insights-glossary"></a>Time Series Insights 詞彙

* **環境**︰環境是具有輸入和儲存容量的 Azure 資源。  客戶佈建透過 hello 與它們所需容量的 Azure 入口網站的環境。
* **事件來源**：事件來源衍生自事件代理人，例如 Azure 事件中樞。  時間序列 Insights 直接連接 tooEvent 來源，而不需要撰寫任何程式碼擷取 hello 資料流。 目前，Time Series Insights 支援 Azure 事件中樞與 Azure IoT 中樞。
* **參考資料**： 時間序列 Insights 提供使用者 hello 能力 toojoin 時間序列資料與參考資料。  參考資料可以包含關於裝置的中繼資料，也可以包含其他較不常變更的靜態資料。 時間序列 Insights 聯結可讓使用者 toovisualize hello 與資料流的參考資料和分析此資料接近即時。
