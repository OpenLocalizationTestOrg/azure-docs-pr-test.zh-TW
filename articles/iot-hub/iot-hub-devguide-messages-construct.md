---
title: "aaaUnderstand Azure IoT 中樞訊息格式 |Microsoft 文件"
description: "開發人員指南-descibes hello 格式和預期的 IoT 中樞訊息的內容。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>建立及讀取 IoT 中樞訊息

toosupport 順暢互通性之間的通訊協定，IoT 中樞定義所有面對裝置的通訊協定的一般訊息格式。 此訊息格式可用於[裝置對雲端][lnk-d2c]和[雲端對裝置][lnk-c2d]訊息。 [IoT 中樞訊息][lnk-messaging]包含：

* 一組 *系統屬性*。 IoT 中樞解譯或設定的屬性。 這個集合是預先決定的。
* 一組 *應用程式屬性*。 字串 hello 應用程式可以定義的屬性與存取權，而不需要 toodeserialize hello 訊息本文的字典。 IoT 中樞不會修改這些屬性。
* 不透明的二進位主體。

在下列情況下，屬性名稱和值只能包含 ASCII 英數字元和 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}``：

* 傳送使用 hello HTTP 通訊協定的裝置到雲端訊息。
* 傳送雲端到裝置的訊息。

如需有關如何 tooencode 和解碼使用不同的通訊協定傳送訊息，請參閱[Azure IoT Sdk][lnk-sdks]。

hello 下表列出 hello 的 IoT 中樞訊息中的系統屬性。

| 屬性 | 說明 |
| --- | --- |
| MessageId |Hello 訊息，要求-回覆模式使用使用者可設定識別項。 格式： 區分大小寫字串 （向上 too128 字元） 的英數字元的 ASCII 7 位元 + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。 |
| 序號 |數字 （每個裝置佇列唯一） 指派的 IoT 中樞 tooeach 雲端到裝置的訊息。 |
| 太|[雲端到裝置][lnk-c2d]訊息中指定的目的地。 |
| ExpiryTimeUtc |訊息到期的日期和時間。 |
| EnqueuedTime |日期和時間的 hello[雲端到裝置][ lnk-c2d] IoT 中心已接收訊息。 |
| CorrelationId |通常包含 hello MessageId hello 要求，要求-回覆模式中的回應訊息中的字串屬性。 |
| UserId |使用 toospecify hello 訊息來源的識別碼。 當訊息透過 IoT 中樞產生時，它會設定太`{iot hub name}`。 |
| Ack |意見反應訊息產生器。 這個屬性是雲端到裝置訊息 toorequest IoT 中樞 toogenerate 意見反應在訊息中使用結果 hello 耗用量的 hello 訊息 hello 裝置。 可能的值：**無**（預設值）： 不意見反應會產生訊息，**正數**: hello 訊息已完成，如果收到的意見反應**負數**： 接收如果沒有完成 hello 裝置 hello 訊息過期 （或已達到最大傳遞計數） 的意見反應訊息或**完整**： 正數和負數。 若需詳細資訊，請參閱[訊息意見反應][lnk-feedback]。 |
| ConnectionDeviceId |由 IoT 中樞在裝置到雲端訊息上設定的識別碼。 它包含 hello **deviceId**的 hello 裝置傳送 hello 訊息。 |
| ConnectionDeviceGenerationId |由 IoT 中樞在裝置到雲端訊息上設定的識別碼。 它包含 hello **generationId** (根據[裝置身分識別屬性][lnk-device-properties]) 的 hello 裝置傳送 hello 訊息。 |
| ConnectionAuthMethod |由 IoT 中樞在裝置到雲端訊息上設定的驗證方法。 此屬性包含 hello 驗證方法使用 tooauthenticate hello 裝置傳送 hello 訊息的相關資訊。 如需詳細資訊，請參閱[裝置 toocloud 的防詐騙功能][lnk-antispoofing]。 |

## <a name="message-size"></a>訊息大小

IoT 中樞測量訊息大小無從驗證通訊協定的方式，考慮只有 hello 實際的承載。 hello 大小 （位元組） 會計算為 hello hello 下列總和：

* hello 本文大小 （位元組）。
* hello 大小 （位元組） 的所有 hello 值 hello 訊息系統屬性。
* hello 大小 （位元組） 的所有使用者的屬性名稱和值。

屬性名稱和值都是有限的 tooASCII 字元，因此 hello 字串 hello 長度等於 hello 大小 （位元組）。

## <a name="next-steps"></a>後續步驟

如需 IoT 中樞訊息大小限制的資訊，請參閱 [IoT 中樞配額和節流][lnk-quotas]。

toolearn 如何 toocreate 和讀取的 IoT 中樞訊息不同的程式語言，請參閱 hello[開始][ lnk-get-started]教學課程。

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
