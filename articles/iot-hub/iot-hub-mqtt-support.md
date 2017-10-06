---
title: "Azure IoT 中樞 MQTT 支援 aaaUnderstand |Microsoft 文件"
description: "開發人員指南-連線 tooan IoT 中樞面對裝置的端點使用的裝置 hello MQTT 通訊協定的支援。 Hello Azure IoT 裝置 Sdk 中包含內建 MQTT 支援的相關資訊。"
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>與您使用 hello MQTT 通訊協定的 IoT 中樞通訊

IoT 中樞讓裝置 toocommunicate hello IoT 中樞裝置端點使用 hello [MQTT v3.1.1] [ lnk-mqtt-org]連接埠 8883 或 MQTT v3.1.1 透過 WebSocket 通訊協定連接埠 443 上的通訊協定。 IoT 中樞需要使用 TLS/SSL 來保護所有裝置通訊 toobe （因此，IoT 中樞不支援非安全連線透過連接埠 1883年）。

## <a name="connecting-tooiot-hub"></a>連接 tooIoT 中樞

裝置可以使用 hello MQTT 通訊協定 tooconnect tooan IoT 中樞透過 hello 文件庫中 hello [Azure IoT Sdk] [ lnk-device-sdks]或直接使用 hello MQTT 通訊協定。

## <a name="using-hello-device-sdks"></a>使用 hello 裝置 Sdk

[裝置 Sdk] [ lnk-device-sdks]該支援 hello MQTT 通訊協定可供 Java、 Node.js、 C、 C# 和 Python。 hello 裝置 Sdk 使用 hello 標準 IoT 中樞連接字串 tooestablish 連接 tooan IoT 中樞。 toouse hello MQTT 通訊協定 hello 用戶端通訊協定參數必須設定太**MQTT**。 根據預設，hello 裝置 Sdk 連線 tooan IoT 中樞與 hello **CleanSession**旗標設定得**0**並用**QoS 1**與 hello IoT 中樞的訊息交換。

當裝置連線的 tooan IoT 中樞時，hello 裝置 Sdk 會提供方法讓 hello 裝置 toosend 訊息 tooand 從 IoT 中心接收訊息。

hello 下表包含連結 toocode 範例對每個支援的語言指定 hello 參數 toouse tooestablish 連接 tooIoT 集線器使用 hello MQTT 通訊協定。

| 語言 | 通訊協定參數 |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>從 AMQP tooMQTT 移轉裝置應用程式

如果您使用 hello[裝置 Sdk][lnk-device-sdks]，從使用 AMQP 切換 tooMQTT 需要變更 hello 用戶端初始化在 hello 通訊協定參數，如先前所述。

當此情況下，請確定 toocheck hello 下列項目：

* AMQP 會傳回錯誤，以取得多個條件，而 MQTT 終止 hello 連線。 因此，可能需要稍微變更您的例外狀況處理邏輯。
* MQTT 不支援 hello*拒絕*作業接收時[雲端到裝置訊息][lnk-messaging]。 如果您的後端應用程式需要 tooreceive hello 裝置應用程式的回應，請考慮使用[直接方法][lnk-methods]。

## <a name="using-hello-mqtt-protocol-directly"></a>直接使用 hello MQTT 通訊協定
如果裝置無法使用 hello 裝置 Sdk，它仍可連線 hello MQTT 通訊協定使用連接埠 8883 toohello 公用裝置端點。 在 hello**連接**封包 hello 裝置應使用下列值的 hello:

* Hello **ClientId**欄位中，使用 hello **deviceId**。
* Hello **Username**欄位中，使用`{iothubhostname}/{device_id}/api-version=2016-11-14`，其中 {iothubhostname} 是 hello hello IoT 中樞的完整 CName。

    例如，如果 hello IoT 中樞的名稱是**contoso.azure devices.net** ，而且如果您的裝置 hello 名稱是**MyDevice01**，hello 完整**Username**欄位應包含`contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Hello**密碼**欄位中，使用 SAS 權杖。 hello 的 SAS token hello 格式 hello 相同 hello HTTP 和 AMQP 通訊協定：<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`。

    如需有關如何 toogenerate SAS 權杖，請參閱 hello 裝置一節[使用 IoT 中樞安全性語彙基元][lnk-sas-tokens]。

    測試時，您也可以使用 hello[裝置總管][ lnk-device-explorer]工具 tooquickly 產生 SAS 權杖，您可以複製並貼到您自己的程式碼：

  1. 移 toohello**管理**索引標籤中**裝置總管**。
  2. 按一下 [SAS 權杖]  \(右上角)。
  3. 在**SASTokenForm**，選取您的裝置在 hello **DeviceID**下拉式清單。 設定您的 **TTL**。
  4. 按一下**產生**toocreate 您的權杖。

     hello SAS 權杖，而會產生具有這個結構： `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。

     hello hello 為這個語彙基元 toouse 一部分**密碼**欄位 tooconnect 使用 MQTT 是： `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。

對於 MQTT 連線和中斷連線的封包，IoT 中樞發出 hello 事件**作業監視**通道的其他資訊可幫助您 tootroubleshoot 連線問題。

### <a name="sending-device-to-cloud-messages"></a>傳送裝置到雲端訊息

成功連接後，裝置可以傳送訊息 tooIoT 集線器使用`devices/{device_id}/messages/events/`或`devices/{device_id}/messages/events/{property_bag}`為**主題名稱**。 hello`{property_bag}`項目可讓 hello 裝置 toosend 訊息以 url 編碼格式的額外屬性。 例如：

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> 這`{property_bag}`項目使用 hello 相同的編碼方式與 hello HTTP 通訊協定中的查詢字串一樣。
>
>

hello 裝置應用程式也可以使用`devices/{device_id}/messages/events/{property_bag}`為 hello**將主題名稱**toodefine*將訊息*toobe 以遙測訊息轉送。

- 「IoT 中樞」不支援 QoS 2 訊息。 如果裝置應用程式發佈的訊息**QoS 2**，IoT 中樞關閉 hello 網路連接。
- 「IoT 中樞」不會保存「保留」訊息。 如果裝置傳送 hello 訊息**保留**旗標設定 too1、 IoT 中樞將 hello **x-opt-保留**應用程式屬性 toohello 訊息。 在此情況下，而不是保存的 hello 保留的訊息，IoT 中樞將它傳遞至 toohello 後端應用程式。
- IoT 中樞僅支援每個裝置有一個作用中 MQTT 連接。 任何新 MQTT 連線 hello 代表相同的裝置識別碼會導致 IoT 中樞 toodrop hello 現有的連接。

如需詳細資訊，請參閱[傳訊開發人員指南][lnk-messaging]。

### <a name="receiving-cloud-to-device-messages"></a>接收雲端到裝置訊息

從 IoT 中樞 tooreceive 郵件，裝置應該使用訂閱`devices/{device_id}/messages/devicebound/#`為**主題篩選**。 hello 多層級的萬用字元 **#** 在 hello 主題篩選器會使用僅 tooallow hello 裝置 hello 主題名稱中的 tooreceive 其他屬性。 IoT 中樞不允許的 hello hello 使用量 **#** 或**嗎？** 萬用字元來篩選副主題。 IoT 中樞不是一般用途 pub 子訊息代理人，因為它只支援 hello 記載的主題名稱和主題篩選條件。

hello 裝置未收到任何訊息從 IoT 中樞，直到它已成功訂閱 tooits 裝置特定端點，由 hello`devices/{device_id}/messages/devicebound/#`主題篩選器。 在建立成功的訂用帳戶之後，hello 裝置就會開始接收僅雲端到裝置訊息已傳送 tooit hello 訂用帳戶的 hello 時間之後。 如果 hello 裝置連線與**CleanSession**旗標設定得**0**，hello 訂用帳戶會在不同的工作階段之間保存。 在此情況下，hello 與連接的下一次**CleanSession 0** hello 裝置接收到未處理的訊息已傳送 tooit 時已中斷連線。 如果使用 hello 裝置**CleanSession**旗標設定得**1**但未收到任何訊息從 IoT 中樞直到它訂閱 tooits 裝置端點。

IoT 中樞傳送 hello 訊息**主題名稱** `devices/{device_id}/messages/devicebound/`，或`devices/{device_id}/messages/devicebound/{property_bag}`是否有任何訊息屬性。 `{property_bag}` 包含訊息屬性的 url 編碼索引鍵/值組。 只有應用程式內容和使用者可設定系統屬性 (例如**messageId**或**correlationId**) 隨附的 hello 屬性包。 系統屬性名稱有 hello 前置詞 **$** ，應用程式屬性沒有前置詞使用 hello 原始屬性的名稱。

當裝置應用程式會訂閱具有 tooa 主題**QoS 2**，IoT 中樞授與最大 QoS 層級 1 中 hello **SUBACK**封包。 IoT 中樞之後，會傳遞訊息 toohello 裝置使用 QoS 1。

### <a name="retrieving-a-device-twins-properties"></a>擷取裝置對應項屬性

首先，裝置訂閱太`$iothub/twin/res/#`，tooreceive hello 作業的回應。 然後，它會傳送空白訊息 tootopic `$iothub/twin/GET/?$rid={request id}`，使用已填入的值為**要求識別碼**。 hello 服務然後會傳送回應訊息，其中包含主題上的 hello 裝置兩個資料`$iothub/twin/res/{status}/?$rid={request id}`，使用 hello 相同**要求識別碼**與 hello 要求。

根據 [IoT 中樞傳訊開發人員指南][lnk-messaging]，要求識別碼可以是任何有效的訊息屬性值，而狀態會驗證為整數。
hello 回應主體會包含 hello 屬性 hello 裝置兩個區段：

hello 主體 hello 識別登錄項目有限制 toohello 「 屬性 」 成員，例如：

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

hello 可能的狀態碼如下：

|狀態 | 說明 |
| ----- | ----------- |
| 200 | 成功 |
| 429 | 要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas] |
| 5** | 伺服器錯誤 |

如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。

### <a name="update-device-twins-reported-properties"></a>更新裝置對應項的報告屬性

hello 下列順序說明裝置 hello 的更新方式回報 hello 裝置的兩個在 IoT 中樞中的屬性：

1. 裝置必須先訂閱 toohello`$iothub/twin/res/#`主題 tooreceive hello 作業的回應，或從 IoT 中樞。

1. 裝置傳送訊息，將包含 hello 裝置兩個更新 toohello`$iothub/twin/PATCH/properties/reported/?$rid={request id}`主題。 此訊息包含 **request id** 值。

1. hello 服務，然後傳送回應訊息包含 hello 新 ETag 值 hello 主題上的報告的屬性集合`$iothub/twin/res/{status}/?$rid={request id}`。 此回應訊息，會使用 hello 相同**要求識別碼**與 hello 要求。

hello 要求訊息主體包含 JSON 文件，提供新的值 （沒有其他屬性或中繼資料可進行修改） 的報告屬性。
Hello JSON 文件中的每個成員會更新，或將 hello 裝置兩個的文件中的 hello 相對應的成員。 成員設定得`null`，刪除 hello 從 hello 包含物件的成員。 例如：

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

hello 可能的狀態碼如下：

|狀態 | 說明 |
| ----- | ----------- |
| 200 | 成功 |
| 400 | 不正確的要求。 JSON 格式錯誤 |
| 429 | 要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas] |
| 5** | 伺服器錯誤 |

如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。

### <a name="receiving-desired-properties-update-notifications"></a>接收所需屬性更新通知

IoT 中樞連接裝置之後，傳送通知 toohello 主題`$iothub/twin/PATCH/properties/desired/?$version={new version}`，其中包含 hello hello hello 方案後端所執行的更新內容。 例如：

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

內容更新與`null`hello JSON 的值表示物件正在刪除成員。


> [!IMPORTANT] 
> IoT 中樞只會在連接裝置時產生變更通知。 請確定 tooimplement hello[裝置重新連線流程][ lnk-devguide-twin-reconnection] tookeep hello 所需的 IoT 中樞與 hello 裝置應用程式之間的同步處理的屬性。

如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。

### <a name="respond-tooa-direct-method"></a>回應 tooa 直接方法

首先，裝置必須 toosubscribe 太`$iothub/methods/POST/#`。 IoT 中樞傳送方法要求 toohello 主題`$iothub/methods/POST/{method name}/?$rid={request id}`、 具有有效的 JSON 或空的本文。

toorespond，hello 裝置傳送訊息，其中的有效的 JSON 或空本文 toohello 主題`$iothub/methods/res/{status}/?$rid={request id}`，其中**要求識別碼**具有 toomatch hello 中 hello 要求訊息，和**狀態**具有 toobe 整數.

如需詳細資訊，請參閱[直接方法開發人員指南][lnk-methods]。

### <a name="additional-considerations"></a>其他考量

做為最後的考量，如果您需要 toocustomize hello MQTT 通訊協定的行為在 hello 雲端端，您應該檢視 hello [Azure IoT 通訊協定閘道][ lnk-azure-protocol-gateway] ，可讓您 toodeploy 高效能IoT 中樞直接與介面的自訂通訊協定閘道。 hello Azure IoT 通訊協定閘道可讓您 toocustomize hello 裝置通訊協定 tooaccommodate brownfield MQTT 部署或其他自訂通訊協定。 不過，這種方法會要求您執行及操作自訂通訊協定閘道。

## <a name="next-steps"></a>後續步驟

toolearn hello MQTT 通訊協定，詳細資料，請參閱 「 hello [MQTT 文件][lnk-mqtt-docs]。

toolearn 有關規劃您的 IoT 中樞部署的詳細資訊，請參閱：

* [Azure IoT 認證裝置目錄][lnk-devices]
* [支援其他通訊協定][lnk-protocols]
* [與事件中樞比較][lnk-compare]
* [縮放、HA 及 DR][lnk-scaling]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
