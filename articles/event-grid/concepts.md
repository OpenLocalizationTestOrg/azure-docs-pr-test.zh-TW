---
title: "aaaAzure 事件方格概念"
description: "說明 Azure Event Grid 與其概念。 定義 Event Grid 的數個重要元件。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Azure Event Grid 中的概念

hello Azure 事件方格中的主要概念如下：

## <a name="events"></a>事件

事件是資訊的 hello 小量的完整描述的項目發生 hello 系統中。  每個事件都有類似的一般資訊： hello 事件時間 hello 事件的來源所需的位置，以及唯一識別項。  每個事件也會有相關 toohello 特定事件的特定資訊。 例如，在 Azure 儲存體中建立新檔案的相關事件包含 hello 檔案，例如 hello lastTimeModified 值詳細資料。 或者，關於虛擬機器重新開機事件包含 hello 名稱 hello 虛擬機器，以及重新開機的 hello 原因。

## <a name="event-sourcespublishers"></a>事件來源/發行者

事件來源是 hello 事件發生時的所在。 例如，Azure 儲存體是 hello blob 建立事件的事件來源。 Azure VM 網狀架構是 hello 事件來源虛擬機器的事件。 事件來源負責發佈事件 tooEvent 方格。

## <a name="topics"></a>主題

發行者將事件分類成各主題。 hello 主題包含 hello 發行者將事件的傳送位置的端點。 toorespond toocertain 類型的事件，「 訂閱者 」 會決定要哪些主題 toosubscribe。 主題也提供事件結構描述，以便 「 訂閱者 」 可以探索如何 tooconsume hello 事件適當。

系統主題是由 Azure 服務提供的內建主題。 自訂主題是應用程式和協力廠商的主題。

## <a name="event-subscriptions"></a>事件訂閱

訂用帳戶指示 Event Grid 訂閱者有興趣接收主題上的何種事件。  訂用帳戶也會包含有關如何事件應傳遞 toohello 訂閱者。

## <a name="event-handlers"></a>事件處理常式

從事件方格的觀點而言，事件處理常式會是 hello 位置的傳送嗨事件。 hello 處理常式會接受一些進一步的動作 tooprocess hello 事件。  Event Grid 支援多個訂閱者類型。 Hello 的訂閱者的類型，根據事件方格會遵循不同的機制 tooguarantee hello 傳遞 hello 事件。  HTTP webhook 事件處理常式的 hello 事件會重試直到 hello 處理常式會傳回狀態碼`200 – OK`。 Azure 儲存體佇列，直到 hello 佇列服務無法 toosuccessfully 程序 hello 訊息發送到 hello 佇列，會重試 hello 事件。

## <a name="filters"></a>篩選器

訂閱時 tooa 主題，您可以篩選 toohello 端點傳送的 hello 事件。 您可以依事件類型或主旨模式進行篩選。 如需詳細資訊，請參閱 [Event Grid 訂用帳戶結構描述](subscription-creation-schema.md)。

## <a name="security"></a>安全性

事件提供安全性訂閱 tootopics，和發佈主題。 訂閱時，您必須在 hello 資源或主題上的適當權限。 發行時，您必須具有 SAS 權杖或金鑰驗證 hello 主題。 如需詳細資訊，請參閱 [Event Grid 安全性和驗證](security-authentication.md)。

## <a name="failed-delivery"></a>傳遞失敗

當事件方格而無法確認 hello 訂閱者的端點已收到事件時，它會 redelivers hello 事件。 如需詳細資訊，請參閱 [Event Grid 訊息傳遞與重試](delivery-and-retry.md)。

## <a name="next-steps"></a>後續步驟

* 如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)。
* 使用事件方格啟動 tooquickly，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。
