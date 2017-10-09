---
title: "aaaAzure 事件方格傳遞和重試"
description: "說明 Azure Event Grid 如何傳遞事件，以及如何處理未傳遞的訊息。"
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Event Grid 訊息傳遞與重試 

本文章說明未確認傳遞時，Azure Event Grid 如何處理事件。

Event Grid 提供持久的傳遞。 它針對每個訂用帳戶傳遞每則訊息至少一次。 事件會立即傳送每個訂用帳戶註冊 toohello webhook。 如果 webhook 不會通知事件的回條 hello 第一次傳遞的 60 秒內嘗試，會重試傳送嗨事件的事件方格。

## <a name="message-delivery-status"></a>訊息傳遞狀態

事件方格會使用 HTTP 回應代碼 tooacknowledge 回條的事件。 

### <a name="success-codes"></a>成功碼

hello 下列 HTTP 回應碼表示，事件已傳送成功 tooyour webhook。 Event Grid 會將傳遞視為完成。

- 200 確定
- 202 已接受

### <a name="failure-codes"></a>失敗碼

hello 遵循 HTTP 回應碼指出事件傳遞嘗試失敗。 事件方格會再次嘗試 toosend hello 事件。 

- 400 不正確的要求
- 401 未經授權
- 404 找不到
- 408 要求逾時
- 414 URI 太長
- 500 內部伺服器錯誤
- 503 服務無法使用
- 504 閘道逾時

任何其他回應碼或回應缺少回應表示失敗。 Event Grid 會重試傳遞。 

## <a name="retry-intervals"></a>重試間隔

Event Grid 針對事件傳遞使用指數輪詢重試原則。 如果您的 webhook 沒有回應，或是傳回失敗碼，事件方格重試傳送嗨下列排程上：

1. 10 秒
2. 30 秒
3. 1 分鐘
4. 5 分鐘
5. 10 分鐘
6. 30 分鐘
7. 1 小時

事件方格將小型隨機 tooall 重試間隔。

## <a name="retry-duration"></a>重試持續時間

Hello 在預覽期間，Azure 事件方格會到期，不會傳遞兩個小時內的所有事件。 之前上市時，這次將會增加的 too24 小時。 

## <a name="next-steps"></a>後續步驟

* 如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)。
* 使用事件方格啟動 tooquickly，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。
