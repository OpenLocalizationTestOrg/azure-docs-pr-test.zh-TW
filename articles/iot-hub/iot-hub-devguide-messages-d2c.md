---
title: "aaaUnderstand Azure IoT Hub 裝置到雲端訊息 |Microsoft 文件"
description: "開發人員指南-如何 toouse 裝置到雲端訊息與 IoT 中樞。 包含傳送遙測和非 telemtry 資料，並使用 toodeliver 訊息路由的相關資訊。"
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>傳送裝置到雲端訊息 tooIoT 中樞

toosend 時間序列遙測和警示的來源裝置 tooyour 方案後端，請從您的裝置 tooyour IoT 中樞傳送裝置到雲端訊息。 如需 IoT 中樞所支援之其他裝置到雲端選項的討論，請參閱[裝置對雲端通訊指引][lnk-d2c-guidance]。

您透過裝置面向端點傳送裝置到雲端訊息 (**/devices/{deviceId}/messages/events**)。 路由規則，然後將您的郵件 tooone hello 服務向端點的路由 IoT 中樞上。 路由規則使用 hello 標頭和本文 hello 裝置到雲端訊息通過集線器 toodetermine 其中 tooroute 它們。 根據預設，訊息會路由的 toohello 內建的服務對向端點 (**事件訊息/**)，也就是與相容[事件中心][lnk-event-hubs]。 因此，您可以使用標準[事件中心 」 整合和 Sdk] [ lnk-compatible-endpoint] tooreceive 方案中的裝置到雲端訊息後端。

IoT 中樞使用串流訊息模式實作裝置到雲端傳訊。 IoT 中樞的裝置到雲端訊息是更像[事件中心][ lnk-event-hubs] *事件*比[Service Bus] [ lnk-servicebus]*訊息*中會有大量通過 hello 服務可由多個讀取器讀取的事件。

裝置的雲端與 IoT 中樞傳訊具有下列特性的 hello:

* 裝置到雲端訊息是永久性的 IoT 中樞的預設保留**事件訊息/**向上 tooseven 天的結束點。
* 裝置到雲端訊息最多可達 256 KB，並可以分組 toooptimize 傳送的批次中。 批次最多可達 256 KB。
* Hello 中所述[控制存取 tooIoT 中樞][ lnk-devguide-security] ] 區段中，IoT 中樞可讓每一裝置的驗證和存取控制。
* IoT 中樞可讓您 toocreate 個 too10 自訂端點。 訊息會傳遞 toohello 根據您的 IoT 中樞上設定路由的端點。 如需詳細資訊，請參閱[路由規則](#routing-rules)。
* IoT 中樞可同時連線到數百萬部裝置 (請參閱[配額和節流][lnk-quotas])。
* IoT 中樞不允許任意進行資料分割。 裝置到雲端訊息會根據其原始的 **deviceId**進行分割。

如需 hello IoT 中樞與事件中心服務的 hello 差異的詳細資訊，請參閱[Azure IoT 中樞的比較與 Azure 事件中心][lnk-comparison]。

## <a name="send-non-telemetry-traffic"></a>傳送非遙測流量

通常，除了 tootelemetry 資料點、 裝置傳送訊息和需要個別的執行與 hello 方案後端中的處理要求。 例如，必須觸發在 hello 特定動作的重要警示後端。 您可以輕鬆地撰寫[路由規則][ lnk-devguide-custom] toosend 這些類型的訊息 tooan 端點專用 tootheir 處理 hello 訊息上的任一個標頭或 hello 訊息內文中的值為基礎。

如需 hello 最佳方式 tooprocess 這種訊息的詳細資訊，請參閱 hello[教學課程： 如何 tooprocess IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程。

## <a name="route-device-to-cloud-messages"></a>路由傳送裝置到雲端訊息

您有兩個路由裝置到雲端訊息 tooyour 後端應用程式的選項：

* 使用內建的 hello[事件中樞相容端點][ lnk-compatible-endpoint] tooenable 後端應用程式 tooread hello 裝置到雲端所收到的訊息 hello 中樞。 toolearn 有關內建事件中樞相容端點 hello，請參閱[讀取 hello 內建端點的裝置到雲端訊息][lnk-devguide-builtin]。
* 使用您的 IoT 中樞中的路由規則 toosend 訊息 toocustom 端點。 自訂端點可讓您使用事件中心、 服務匯流排佇列或服務匯流排主題的後端應用程式 tooread 裝置到雲端訊息。 toolearn 有關路由和自訂端點，請參閱[用於裝置到雲端訊息的自訂端點和路由規則][lnk-devguide-custom]。

## <a name="anti-spoofing-properties"></a>防詐騙屬性

詐騙裝置到雲端訊息，IoT 中樞中的下列屬性的 hello 與所有訊息的戳記 tooavoid 裝置：

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

hello 前兩個包含 hello **deviceId**和**generationId**的 hello 源自裝置，請依照[裝置身分識別屬性][lnk-device-properties]。

hello **ConnectionAuthMethod**屬性包含序列化的 JSON 物件，具有下列屬性的 hello:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>後續步驟

如需 hello Sdk，您可以使用 toosend 裝置到雲端訊息，請參閱[Azure IoT Sdk][lnk-sdks]。

hello[開始][ lnk-get-started]教學課程告訴您如何 toosend 裝置到雲端訊息從模擬與實體裝置。 如需詳細資訊，請參閱 hello[使用路由的處理序 IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程。

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
