---
title: "Azure Event Grid 概觀"
description: "說明 Azure Event Grid 與其概念。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 12/14/2017
ms.author: babanisa
ms.openlocfilehash: e6665b3b0c6e92ed462f18dbd41d62ccd9304928
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2017
---
# <a name="an-introduction-to-azure-event-grid"></a>Azure Event Grid 簡介

Azure Event Grid 可讓您以事件型架構輕鬆地建立應用程式。 您可以選取您想要訂閱的 Azure 資源，並提供事件處理常式或 WebHook 端點以作為事件的傳送目的地。 對於來自 Azure 服務 (例如儲存體 Blob 和資源群組) 的事件，Event Grid 內建了支援功能。 對於應用程式和第三方的事件，Event Grid 也使用了自訂主題和自訂 Webhook 來提供自訂支援。 

您可以使用篩選器將特定事件路由傳送到不同的端點、多點傳送至多個端點，並確定您的事件會可靠地進行傳遞。 Event Grid 也針對自訂和第三方的事件提供了內建支援。

目前，事件方格都支援下列區域：

* 美國中部
*   美國東部
*   美國東部 2
*   美國中西部
*   美國西部
*   美國西部 2

未來將會新增其他區域。

本文提供 Azure Event Grid 的概觀。 若要開始使用 Event Grid，請參閱[使用 Azure Event Grid 建立和路由傳送自訂事件](custom-event-quickstart.md)。 下圖顯示事件方格將如何連接 「 發行者 」 和處理常式，但它不提供支援選項的完整清單。

![Event Grid 運作模型](./media/overview/event-grid-functional-model.png)

## <a name="event-publishers"></a>事件發佈者

目前有下列 Azure 服務具有內建的 Event Grid 發行者支援：

* Azure 訂用帳戶 (管理作業)
* 自訂主題
* 事件中樞
* 資源群組 (管理作業)
* 儲存體 Blob

今年將會新增其他 Azure 服務。

## <a name="event-handlers"></a>事件處理常式

目前有下列 Azure 服務具有內建的 Event Grid 處理常式支援： 

* Azure 自動化
* Azure Functions
* 事件中樞
* Logic Apps
* Microsoft Flow
* Webhook

今年將會新增其他 Azure 服務。

## <a name="concepts"></a>概念

Azure Event Grid 中有五個概念可讓您開始進行：

* **事件** - 發生了什麼事。
* **事件來源/發行者** - 事件發生位置。
* **主題** - 要作為發行者所傳送之事件的目的地端點。
* **事件訂閱** - 用來路由事件的端點或內建機制，有時會路由到多個處理常式。 處理常式也會使用訂閱來智慧地篩選內送事件。
* **事件處理常式** - 對事件做出回應的應用程式或服務。

如需這些概念的詳細資訊，請參閱 [Azure Event Grid 中的概念](concepts.md)。

## <a name="capabilities"></a>功能

以下是 Azure Event Grid 的一些主要功能︰

* **簡便性** - 點按即可瞄準從 Azure 資源到任何事件處理常式或端點的事件。
* **進階篩選** - 篩選事件類型或事件發佈路徑，以確定事件處理常式只會收到相關的事件。
* **展開傳送** - 讓多個端點訂閱相同的事件，以將事件的複本傳送到所需的多個位置。
* **可靠性** - 利用 24 小時的指數輪詢重試，來確保事件能夠傳遞出去。
* **依事件支付** - 只需就您使用的 Event Grid 數量來付費。
* **高輸送量** - 在每秒支援數百萬個事件的 Event Grid 上建置大量的工作負載。
* **內建事件** - 利用資源定義的內建事件來快速地啟動並執行。
* **自訂事件** - 使用 Event Grid 路由、篩選並在應用程式中可靠地傳遞自訂事件。

如需事件格線、事件中樞和服務匯流排的比較，請參閱[選擇傳遞訊息的 Azure 服務](compare-messaging-services.md)。

## <a name="what-can-i-do-with-event-grid"></a>我可以用 Event Grid 來做什麼？

Azure Event Grid 提供好幾種功能，可大幅提升無伺服器、作業自動化和整合工作： 

### <a name="serverless-application-architectures"></a>無伺服器應用程式架構

![無伺服器應用程式](./media/overview/serverless_web_app.png)

Event Grid 可連線資料來源與事件處理常式。 例如，使用 Event Grid 來立即觸發無伺服器功能，以在每次相片新增至 Blob 儲存體容器時執行影像分析。 

### <a name="ops-automation"></a>作業自動化

![作業自動化](./media/overview/Ops_automation.png)

Event Grid 可讓您加快自動化速度並簡化原則強制執行。 例如，Event Grid 可以在虛擬機器建立或 SQL Database 啟動時通知 Azure 自動化。 這些事件可用於自動檢查服務組態是否符合規範、將中繼資料放入作業工具、標記虛擬機器，或將工作項目歸檔。

### <a name="application-integration"></a>應用程式整合

![應用程式整合](./media/overview/app_integration.png)

Event Grid 可連線您的應用程式與其他服務。 例如，建立自訂主體，將應用程式的事件資料傳送至 Event Grid，並利用其可靠的傳遞、進階路由以及與 Azure 的直接整合。 或者，您可以使用 Event Grid 搭配 Logic Apps 隨處處理資料，而不需撰寫程式碼。 

## <a name="how-much-does-event-grid-cost"></a>Event Grid 的費用有多少？

Azure Event Grid 使用依事件支付計價模式，因此您只需就使用量來付費。

Event Grid 每百萬個作業的費用是 0.60 美元 (預覽期間為 0.30 美元)，而且每個月的前 100,000 個作業是免費的。 作業的定義是事件輸入、進階比對、傳遞嘗試及管理呼叫。  您可以在[定價頁面](https://azure.microsoft.com/pricing/details/event-grid/)找到更多詳細資料。

## <a name="next-steps"></a>後續步驟

* [路由儲存體 Blob 事件](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)  
  使用 Event Grid 回應儲存體 blob 事件。
* [建立並訂閱自訂事件](custom-event-quickstart.md)  
  直接進入正題並開始使用 Azure Event Grid 快速入門來將您自己的自訂事件傳送至任何端點。
* [使用 Logic Apps 來作為事件處理常式](monitor-virtual-machine-changes-event-grid-logic-app.md)  
  有關使用 Logic Apps 建置應用程式以回應 Event Grid 所推送之事件的教學課程。
* [將巨量資料串流處理至資料倉儲](event-grid-event-hubs-integration.md)  
  使用 Azure Functions 將資料從事件中樞串流到 SQL 資料倉儲的教學課程。
* [Event Grid REST API 參考](/rest/api/eventgrid)  
  提供更多有關 Azure Event Grid 的技術資訊，以及適用於管理事件訂閱、路由和篩選的參考。