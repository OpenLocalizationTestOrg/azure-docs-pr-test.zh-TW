---
title: "aaaWhat 是 Azure 事件中樞與為何使用 |Microsoft 文件"
description: "概觀和簡介 tooAzure 事件中心的雲端規模遙測擷取，從網站、 應用程式和裝置"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>何謂事件中樞？

Azure 事件中樞是可高度調整的資料串流平台，以及每秒能夠接收和處理數百萬個事件的事件內嵌服務。 事件中樞可以處理及儲存分散式軟體和裝置所產生的事件、資料或遙測。 資料會傳送 tooan 事件中心可以轉換及儲存使用任何即時的分析提供者或批次/儲存體介面卡。 與 hello 能力 tooprovide[發佈-訂閱功能](https://msdn.microsoft.com/library/aa560414.aspx)巨量資料的低延遲與大規模事件中心做為 「 開啟遞增"hello。

## <a name="why-use-event-hubs"></a>為何使用事件中樞？

事件中樞的事件和遙測處理功能特別適用於︰

* 應用程式檢測
* 使用者經驗或工作流程處理
* 物聯網 (IoT) 案例

例如，事件中樞能追蹤行動應用程式中的行為、接收 Web 伺服陣列的流量資訊、擷取遊戲機遊戲中的遊戲內部事件，或是從產業用機器、連接的車輛或其他裝置收集遙測。

## <a name="azure-event-hubs-overview"></a>Azure 事件中樞概觀

hello 常見事件中心在解決方案架構中所扮演的角色是 「 前端 」 是事件管線，通常稱為 hello*事件擷取器*。 事件擷取器是元件或服務位於事件發行者 」 和 「 從 hello 中取用這些事件的事件資料流的事件取用者 toodecouple hello 生產之間。 hello 下圖說明這個架構：

![事件中樞](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

事件中樞提供訊息串流處理能力，但特性迴異於傳統企業傳訊。 事件中樞功能是以高輸送量和事件處理案例為重點。 因此，事件中心是與不同[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)傳訊，但未實作的一些 hello 功能可供[服務匯流排傳訊](/azure/service-bus-messaging/)實體，例如主題。

## <a name="event-hubs-features"></a>事件中樞功能

事件中心包含下列索引鍵項目 hello:

- [**事件產生者/發行者**](event-hubs-features.md#event-publishers)： 傳送資料 tooan 事件中心的實體。 透過 AMQP 1.0 或 HTTPS 發佈事件。
- [**擷取**](event-hubs-features.md#capture)： 可讓您 toocapture 事件中心資料流處理資料，並將它儲存在 Azure Blob 儲存體帳戶。
- [**資料分割**](event-hubs-features.md#partitions)： 可讓每個取用者 tooonly 讀取的特定子集或資料分割，hello 事件資料流。
- [**SAS 權杖**](event-hubs-features.md#sas-tokens)： 識別並驗證 hello 事件發行者。
- [**事件取用者**](event-hubs-features.md#event-consumers)：任何從事件中樞讀取事件資料的實體。 事件取用者會透過 AMQP 1.0 連線。 
- [**取用者群組**](event-hubs-features.md#consumer-groups)： 提供取用應用程式與 hello 事件資料流的不同檢視，個別啟用這些取用者 tooact 每個倍數。
- [**輸送量單位**](event-hubs-features.md#capacity)：預先購買的容量單位。 每個磁碟分割有 1 個輸送量單位的規模上限。

如需這些和其他事件中心功能的技術詳細資訊，請參閱 hello[事件中心功能概觀](event-hubs-features.md)。 

## <a name="next-steps"></a>後續步驟

如需詳細的事件中樞價格資訊，請參閱[事件中樞價格](https://azure.microsoft.com/pricing/details/event-hubs/)。

如需有關事件中心的詳細資訊，請造訪下列連結查看 hello:

* 開始使用[事件中樞教學課程](event-hubs-dotnet-standard-getstarted-send.md)
* [事件中樞常見問題集](event-hubs-faq.md)
* [使用事件中樞的範例應用程式](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

