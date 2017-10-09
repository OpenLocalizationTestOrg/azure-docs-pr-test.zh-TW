---
title: "aaaAzure 事件方格概觀"
description: "說明 Azure Event Grid 與其概念。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>簡介 tooAzure 事件方格

Azure 事件方格可讓您以事件為基礎的架構 tooeasily 建置應用程式。 您選取 hello Azure 資源，toosubscribe，然後授與 hello 事件處理常式或 WebHook 端點 toosend hello 事件。 對於來自 Azure 服務 (例如儲存體 Blob 和資源群組) 的事件，Event Grid 內建了支援功能。 對於應用程式和第三方的事件，Event Grid 也使用了自訂主題和自訂 Webhook 來提供自訂支援。 

您可以使用篩選器 tooroute 特定事件 toodifferent 端點，多點傳送的 toomultiple 端點，並確定您的事件會可靠地傳遞。 Event Grid 也針對自訂和第三方的事件提供了內建支援。

Hello 預覽版本，支援事件方格**westus2**和**westcentralus**位置。 未來將會新增其他區域。

本文提供 Azure Event Grid 的概觀。 如果您想 tooget 與事件方格啟動，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。

![Event Grid 運作模型](./media/overview/event-grid-functional-model.png)

目前，Blob 儲存體未公開作為發行者。

## <a name="concepts"></a>概念

Azure Event Grid 中有五個概念可讓您開始進行：

* **事件** - 發生了什麼事。
* **事件來源發行者**-hello 事件發生。
* **主題**-hello 的端點的 「 發行者 」 傳送事件的位置。
* **事件訂閱**-hello 端點或內建機制 tooroute 事件，有時候 toomultiple 處理常式。 訂用帳戶也會使用處理常式 toointelligently 篩選內送事件。
* **事件處理常式**-hello 應用程式或服務對回應 toohello 事件。

如需這些概念的詳細資訊，請參閱 [Azure Event Grid 中的概念](concepts.md)。

## <a name="capabilities"></a>功能

以下是一些 Azure 事件方格的 hello 重要功能：

* **為了簡單起見**-從您的 Azure 資源 tooany 事件處理常式或端點的點，並按一下 tooaim 事件。
* **進階篩選**-篩選事件類型或事件發行路徑 tooensure 事件處理常式只會接收相關的事件。
* **展開傳送**-訂閱多個端點 toohello 相同事件 toosend 複製 hello 事件 tooas 的許多地方視。
* **可靠性**-利用使用指數型輪詢 tooensure 事件傳遞的 24 小時重試。
* **支付每一個事件**-付費 hello 數量僅供您使用事件方格。
* **高輸送量** - 在每秒支援數百萬個事件的 Event Grid 上建置大量的工作負載。
* **內建事件** - 利用資源定義的內建事件來快速地啟動並執行。
* **自訂事件** - 使用 Event Grid 路由、篩選並在應用程式中可靠地傳遞自訂事件。

## <a name="built-in-publisher-and-handler-integration"></a>內建的發行者和處理常式整合

Azure 使用多項服務 (包括發行者和處理常式) 來提供內建的事件支援。

### <a name="publishers"></a>發行者

目前，hello 下列 Azure 服務都有內建的 「 發行者 」 支援的事件方格：

* 資源群組 (管理作業)
* Azure 訂用帳戶 (管理作業)
* 事件中樞
* 自訂主題

今年將會新增其他 Azure 服務。

### <a name="handlers"></a>處理常式

目前，hello 下列 Azure 服務都有內建的處理常式的事件方格支援： 

* Azure Functions
* Logic Apps
* Azure 自動化
* Webhook

今年將會新增其他 Azure 服務。

## <a name="what-can-i-do-with-event-grid"></a>我可以用 Event Grid 來做什麼？

Azure Event Grid 提供好幾種功能，可大幅提升無伺服器、作業自動化和整合工作： 

### <a name="serverless-application-architectures"></a>無伺服器應用程式架構

![無伺服器應用程式](./media/overview/serverless_web_app.png)

Event Grid 可連線資料來源與事件處理常式。 例如，使用事件方格 tooinstantly 觸發程序無伺服器函式 toorun 映像分析新相片是每次加入 tooa blob 儲存體容器。 

### <a name="ops-automation"></a>作業自動化

![作業自動化](./media/overview/Ops_automation.png)

事件方格可讓您 toospeed 自動化，並簡化原則強制執行。 例如，Event Grid 可以在虛擬機器建立或 SQL Database 啟動時通知 Azure 自動化。 可以使用這些事件 tooautomatically 檢查服務組態是否符合標準，將中繼資料放入作業的工具、 標記的虛擬機器或檔案的工作項目。

### <a name="application-integration"></a>應用程式整合

![應用程式整合](./media/overview/app_integration.png)

Event Grid 可連線您的應用程式與其他服務。 比方說，您的應用程式事件資料 tooEvent 方格中，建立自訂主題 toosend 充分利用其可靠的傳遞，進階路由，並直接與 Azure 的整合。 或者，您可以使用的任何地方、 Logic Apps tooprocess 資料的事件方格，而不需要撰寫程式碼。 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Event Grid 與其他 Azure 整合服務有何不同？

Event Grid 是可供進行回應式事件導向程式設計的事件背板。 它不僅與 Azure 服務緊密整合，並可與第三方服務整合。 hello 事件訊息包含您需要 tooreact toochanges 服務和應用程式中的 hello 資訊。 事件方格不是在資料管線，並不會傳遞 hello 已更新的實際物件。

服務匯流排很適合需要交易、排序、重複偵測和瞬間一致性的傳統企業應用程式使用。 Event Grid 則是設計來為回應式模型提供速度、擴充性、廣度和低成本。 它是適合的 tooserverless 架構。

Event Grid 可彌補其他 Azure 服務 (例如 Logic Apps 和事件中樞) 的不足。 事件方格觸發程序 hello 邏輯應用程式 toobegin 其工作流程。 事件中心會讓您從事件中心擷取並建置資料輸入和轉換管線 tooreact tooevents 搭配事件方格。

## <a name="how-much-does-event-grid-cost"></a>Event Grid 的費用有多少？

Azure Event Grid 使用依事件支付計價模式，因此您只需就使用量來付費。

事件方格成本 $0.60 每百萬個作業 (0.30 美元在預覽期間)，而且可用 hello 每月的第一次 100,000 作業。 作業的定義是事件輸入、進階比對、傳遞嘗試及管理呼叫。  更多詳細資料位於 hello[定價頁面](https://azure.microsoft.com/pricing/details/event-grid/)。

## <a name="next-steps"></a>後續步驟

* [建立並訂閱 toocustom 事件](custom-event-quickstart.md)直接並開始傳送您自己的自訂事件 tooany 端點使用 hello Azure 事件方格快速入門。
* [使用邏輯應用程式做為事件處理常式](monitor-virtual-machine-changes-event-grid-logic-app.md)的教學課程建置應用程式使用 Logic Apps tooreact tooevents 推入的事件方格。
* [Event Grid REST API 參考](/rest/api/eventgrid)  
  提供管理事件訂閱 hello Azure 事件方格中的其他技術資訊和參考路由及篩選。
