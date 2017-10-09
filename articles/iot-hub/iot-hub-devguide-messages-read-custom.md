---
title: "aaaUnderstand Azure IoT 中樞自訂端點 |Microsoft 文件"
description: "開發人員指南-使用 路由規則 tooroute 裝置到雲端訊息 toocustom 端點。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>針對裝置對雲端訊息使用訊息路由和自訂端點

IoT 中樞可讓您 tooroute[裝置到雲端訊息][ lnk-device-to-cloud] tooIoT 中樞服務向端點根據訊息屬性。 路由規則提供 hello 彈性 toosend 訊息需要 toogo hello 不需要其他服務 tooprocess 訊息或 toowrite 額外的程式碼。 您設定每個路由規則具有下列屬性的 hello:

| 屬性      | 說明 |
| ------------- | ----------- |
| **名稱**      | hello 唯一識別名稱 hello 規則。 |
| **來源**    | hello hello 資料來源資料流 toobe 作用時。 例如裝置遙測。 |
| **Condition** | hello hello 路由規則針對 hello 訊息標頭和主體執行，並使用 toodetermine 是否 hello 端點的相符項目查詢運算式。 如需有關如何建構路由條件的詳細資訊，請參閱 hello[參考-裝置雙及作業的查詢語言][lnk-devguide-query-language]。 |
| **端點**  | hello hello 端點 IoT 中樞讓傳送訊息符合 hello 條件的名稱。 端點應該位於 hello hello IoT 中樞與相同的區域，否則您可能需要支付費用的跨地區寫入。 |

在多個路由規則、 大小寫 IoT 中樞將傳遞每個相符的規則相關聯的 hello 訊息 toohello 端點上 hello 狀況時，可能會比單一訊息。 IoT 中樞也會自動 deduplicates 訊息傳遞，因此如果訊息符合多個規則都有 hello 相同的目的地，它僅寫入 toothat 目的地一次。

IoT 中樞具有預設[內建端點][lnk-built-in]。 您可以建立自訂端點 tooroute 訊息 tooby 連結您的訂用帳戶 toohello 中樞中的其他服務。 IoT 中樞目前支援事件中樞、服務匯流排佇列，及服務匯流排主題做為自訂端點。

> [!WARNING]
> 不支援將啟用 [工作階段] 或 [重複偵測] 的服務匯流排佇列和主題作為自訂端點。

如需在 IoT 中樞建立自訂端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。

如需從自訂端點讀取的詳細資訊，請參閱：

* 從[事件中樞][lnk-getstarted-eh]讀取。
* 從[服務匯流排佇列][lnk-getstarted-queue]讀取。
* 從[服務匯流排主題][lnk-getstarted-topic]讀取。

### <a name="next-steps"></a>後續步驟

如需 IoT 中樞端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。

如需有關 hello 查詢語言使用 toodefine 路由規則，請參閱[裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query-language]。

hello[使用路由的處理序 IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程示範如何 toouse 路由規則，並自訂端點。

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
