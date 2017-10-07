---
title: "aaaUnderstand Azure IoT 中樞雲端到裝置訊息 |Microsoft 文件"
description: "開發人員指南-如何 toouse 雲端到裝置與 IoT 中樞通訊。 包含 hello 訊息生命週期和組態選項的詳細資訊。"
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>從 IoT 中樞傳送雲端到裝置訊息

toosend 單向通知 toohello 裝置應用程式從您的方案後端，從您的 IoT 中樞 tooyour 裝置傳送雲端到裝置訊息。 如需 IoT 中樞所支援之其他雲端到裝置選項的討論，請參閱[雲端對裝置通訊指引][lnk-c2d-guidance]。

您可以透過面向服務的端點 (**/messages/devicebound**) 來傳送雲端到裝置訊息。 裝置再收到 hello 訊息透過裝置的特定端點 (**/devices/ {deviceId} / 訊息/devicebound**)。

每個雲端到裝置訊息為目標的單一裝置設定 hello**至**屬性太**/devices/ {deviceId} / 訊息/devicebound**。

每個裝置佇列最多保留 50 則雲端到裝置訊息。 嘗試 toosend 詳細訊息 toohello 相同的裝置會導致錯誤。

## <a name="hello-cloud-to-device-message-lifecycle"></a>hello 雲端到裝置訊息生命週期

tooguarantee 在-至少一次訊息傳遞，IoT 中樞保存每一裝置的佇列中的雲端到裝置訊息。 裝置必須明確地認可*完成*的 IoT 中樞 tooremove 從 hello 佇列。 此方法保證連線失敗和裝置故障能夠恢復。

hello 下列圖表顯示 hello 生命週期狀態圖表雲端到裝置訊息在 IoT 中樞。

![雲端到裝置的訊息生命週期][img-lifecycle]

當 hello IoT 中樞服務傳送訊息 tooa 裝置、 hello 服務太設定 hello 訊息狀態**佇列**。 當裝置想太*接收*訊息時，IoT 中樞*鎖定*hello 訊息 (藉由設定 hello 狀態太**看不見**)，可讓其他執行緒上 hello 裝置 toostart接收其他訊息。 當裝置執行緒完成 hello 處理訊息時，它會通知的 IoT 中樞*完成*hello 訊息。 IoT 中樞設定 hello 狀態太**已完成**。

裝置也可以選擇：

* *拒絕*hello 訊息，導致 IoT 中樞 tooset 它 toohello**成為無效**狀態。 透過 hello MQTT 通訊協定連線的裝置無法拒絕雲端到裝置的訊息。
* *放棄*hello 訊息，導致 IoT 中樞 tooput hello 訊息回 hello 佇列中，與 hello 狀態設定得**佇列**。

執行緒可能會失敗 tooprocess 訊息且不會通知 IoT 中樞。 在此情況下，自動訊息從 hello 轉換**看不見**狀態回復 toohello**佇列**狀態之後*可見性 （或鎖定） 的逾時*。 此逾時的 hello 預設值是一分鐘。

訊息可以切換 hello**加入佇列**和**看不見**狀態，最多 hello 的 hello 中指定的次數**最大傳遞計數**IoT 中樞上的屬性。 轉換的次數之後, IoT 中樞設定 hello hello 訊息狀態太**成為無效**。 同樣地，IoT 中樞設定 hello 訊息狀態太**成為無效**的到期時間之後 (請參閱[時間 toolive][lnk-ttl])。

hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d-tutorial]會示範如何從 hello toosend 雲端到裝置訊息雲端及接收這些裝置上。

一般而言，裝置會在雲端到裝置訊息完成時 hello 遺失 hello 訊息不會影響 hello 應用程式邏輯。 比方說，當 hello 裝置已保存在本機 hello 訊息內容或已成功執行作業。 hello 訊息也可能具有暫時性資訊，其遺失不會影響 hello hello 應用程式功能。 某些情況下，對於長時間執行工作，您可以完成 hello 雲端到裝置訊息後保存 hello 本機儲存體中的工作描述。 然後您可以在各個階段的 hello 工作的進度通知 hello 與一或多個裝置到雲端訊息方案後的端。

## <a name="message-expiration-time-toolive"></a>訊息的過期 （toolive 時間）

每個雲端到裝置的訊息都有到期時間。 這次透過設定 hello 服務 (在 hello **ExpiryTimeUtc**屬性)，或使用 hello 預設的 IoT 中樞*時間 toolive*指定為 IoT 中樞內容。 請參閱[雲端到裝置的設定選項][lnk-c2d-configuration]。

常見方式 tootake 優點訊息過期並避免 toodisconnected 裝置傳送訊息，是 tooset toolive 的簡短時間值。 這種方法可達到相同結果與維護 hello 裝置連接狀態，同時會更有效率的 hello。 當您要求訊息收條時，IoT 中樞會通知您哪些裝置可以 tooreceive 訊息，以及哪些裝置不在線上或已失敗。

## <a name="message-feedback"></a>訊息意見反應

當您傳送雲端到裝置訊息時，hello 服務可以要求 hello 傳送 hello 訊息的最終狀態有關的每個訊息意見反應。

| Ack 屬性 | 行為 |
| ------------ | -------- |
| **positive** | IoT 中樞會產生回應訊息，並僅有，hello 雲端到裝置訊息已到達 hello**已完成**狀態。 |
| **negative** | IoT 中樞會產生回應訊息時，如果且只有，hello 雲端到裝置訊息到達 hello**成為無效**狀態。 |
| **full**     | IoT 中樞在任一情況下都會產生意見反應訊息。 |

如果**Ack**是**完整**，而且您沒有收到回應訊息，則表示該 hello 回應訊息過期。 hello 服務無法知道哪些情形的 toohello 原始訊息。 在實務上，服務應該確定在到期之前可以處理 hello 意見反應。 hello 最長有效時間是兩天內，這允許充足的時間 tooget hello 服務執行一次發生失敗時。

如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/feedback**) 利用訊息來傳遞意見反應。 hello 語意收到意見 hello 相同與雲端到裝置訊息與 hello 相同[訊息生命週期][lnk-lifecycle]。 可能的話，會在單一訊息中，以下列格式的 hello 進行批次處理訊息的意見反應：

| 屬性     | 說明 |
| ------------ | ----------- |
| EnqueuedTime | 指出建立 hello 訊息時的時間戳記。 |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

hello 內文是 JSON 序列化的記錄陣列，每個都具有下列屬性的 hello:

| 屬性           | 說明 |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | 指出發生 hello 結果 hello 訊息的時間戳記。 例如，hello 完成裝置或 hello 訊息過期。 |
| OriginalMessageId  | **MessageId**的 hello 雲端到裝置訊息 toowhich 此意見反應資訊與相關。 |
| StatusCode         | 必要字串。 用於 IoT 中樞所產生的回饋訊息中。 <br/> 「成功」 <br/> 「已過期」 <br/> 「DeliveryCountExceeded」 <br/> 「已拒絕」 <br/> 「已清除」 |
| 描述        | **StatusCode**的字串值。 |
| deviceId           | **DeviceId** hello 目標裝置的 hello 雲端到裝置訊息 toowhich 相關的意見反應此片段。 |
| DeviceGenerationId | **DeviceGenerationId** hello 目標裝置的 hello 雲端到裝置訊息 toowhich 相關的意見反應此片段。 |

必須指定 hello 服務**MessageId** hello 雲端到裝置訊息 toobe 無法 toocorrelate 其意見反應與 hello 原始訊息。

hello 下列範例顯示 hello 訊息本文的意見反應。

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>雲端到裝置組態選項

每個 IoT 中樞會公開下列組態選項適用於雲端到裝置訊息 hello:

| 屬性                  | 說明 | 範圍和預設值 |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | 雲端到裝置訊息的預設 TTL。 | 向上 too2D ISO_8601 間隔 （最小的 1 分鐘）。 預設值︰1 小時。 |
| maxDeliveryCount          | 每個裝置佇列的雲端到裝置最大傳遞計數。 | 1 too100。 預設值：10 |
| feedback.ttlAsIso8601     | 保留服務繫結的意見反應訊息。 | 向上 too2D ISO_8601 間隔 （最小的 1 分鐘）。 預設值︰1 小時。 |
| feedback.maxDeliveryCount |意見反應佇列的最大傳遞計數。 | 1 too100。 預設值 = 100。 |

如需有關如何 tooset 這些組態選項，請參閱[建立 IoT 中樞][lnk-portal]。

## <a name="next-steps"></a>後續步驟

如需 hello Sdk，您可以使用 tooreceive 雲端到裝置訊息，請參閱[Azure IoT Sdk][lnk-sdks]。

tootry 出接收雲端到裝置訊息，請參閱 hello[傳送雲端到裝置][ lnk-c2d-tutorial]教學課程。

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
