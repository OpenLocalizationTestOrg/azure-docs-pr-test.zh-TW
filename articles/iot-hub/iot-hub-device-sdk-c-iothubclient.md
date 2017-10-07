---
title: "c-IoTHubClient aaaAzure IoT 裝置 SDK |Microsoft 文件"
description: "如何在 C toocreate 裝置應用程式的 hello Azure IoT 裝置 SDK toouse hello IoTHubClient 程式庫進行通訊的與 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>適用於 C 的 Azure IoT 裝置 SDK - 深入了解 IoTHubClient
hello[先文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**。該文章已說明 SDK 中有兩個架構層。 在 [hello 基底 hello **IoTHubClient**可直接管理與 IoT 中樞通訊的程式庫。 另外還有 hello**序列化程式**在該組建 tooprovide 序列化服務的程式庫。 本文章中我們將提供其他詳細資料上 hello **IoTHubClient**程式庫。

hello 前一篇文章所述方式 toouse hello **IoTHubClient**文件庫 toosend 事件 tooIoT 中樞和接收訊息。 這篇文章解釋 toomore 精確地管理已延伸，討論*時*您傳送和接收資料，引入您 toohello**較低層級 Api**。 我們也將說明如何 tooattach 屬性 tooevents （和擷取訊息） 使用 hello 屬性處理 hello 的功能**IoTHubClient**程式庫。 最後，我們將提供詳細說明不同的方式 toohandle 從 IoT 中樞接收的訊息。

hello 文章結束時，會涵蓋數個其他的主題，包括裝置認證有關的詳細資訊和如何 toochange hello 行為 hello **IoTHubClient**透過組態選項。

我們將使用 hello **IoTHubClient** SDK 範例 tooexplain 這些主題。 如果您想沿著 toofollow，請參閱 hello **iot 中樞\_用戶端\_範例\_http**和**iot 中樞\_用戶端\_範例\_amqp** hello Azure IoT 裝置 SDK 中包含的這些範例會示範 c 的所有項目 hello 下列各節中所述的應用程式。

您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。

## <a name="hello-lower-level-apis"></a>hello 較低層級應用程式開發介面
hello 前一篇文章所述的 hello hello 基本作業**IotHubClient** hello hello 內容中**iot 中樞\_用戶端\_範例\_amqp**應用程式。 比方說，它會說明如何 tooinitialize hello 使用此程式碼的程式庫。

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

它也說明如何使用這個 toosend 事件函式呼叫。

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

hello 同時也說明 tooreceive 藉由註冊回呼函式的訊息。

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

hello 發行項也會示範使用 toofree 資源 hello 如下的程式碼。

```
IoTHubClient_Destroy(iotHubClientHandle);
```

但是有附屬的這些 Api 的函式 tooeach:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

所有這些函式 hello API 名稱中包含"LL"。 除此之外，其他每一個這些函式的 hello 參數都是相同 tootheir 非 LL 對應項目。 不過，這些函式的 hello 行為不相同，有一項重要的。

當您呼叫**IoTHubClient\_CreateFromConnectionString**，hello 基礎程式庫建立新的執行緒 hello 背景中執行。 此執行緒會將事件傳送到 IoT 中樞以及接收其訊息。 使用 hello"LL"應用程式開發介面時，會建立沒有這類執行緒。 hello 建立 hello 背景執行緒是方便 toohello 開發人員。 您不需要明確地將事件傳送和接收訊息從 IoT 中樞-它在 hello 背景中自動進行有關 tooworry。 相反地，hello"LL"應用程式開發介面可讓您明確掌控與 IoT 中樞通訊如有需要。

toounderstand 這個較好，讓我們來看一個範例：

當您呼叫**IoTHubClient\_SendEventAsync**，您正在實際做什麼 hello 事件放在緩衝區中。 hello 背景執行緒呼叫時建立**IoTHubClient\_CreateFromConnectionString**持續監視這個緩衝區，並傳送任何資料，它包含 tooIoT 中樞。 發生這種情況在 hello hello 背景中相同時間該 hello 主執行緒所執行的其他工作。

同樣地，當您註冊的回呼函式，以訊息**IoTHubClient\_SetMessageCallback**，您要指示 hello SDK toohave hello 背景執行緒會將訊息時，叫用 hello 回呼函式接收獨立的 hello 主執行緒。

背景執行緒時，請勿建立 hello"LL"應用程式開發介面。 相反地，新的 API，必須先呼叫 tooexplicitly 傳送和接收來自 IoT 中樞的資料。 Hello 下列範例所示。

hello **iot 中樞\_用戶端\_範例\_http** hello 示範 SDK 中隨附的應用程式 hello 較低層級應用程式開發介面。 在該範例中，我們會傳送事件 tooIoT 集線器與 hello 如下的程式碼：

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

hello 前三行建立 hello 訊息和 hello 最後一行會傳送 hello 事件。 不過，如先前所述，「 傳送 」 hello 事件表示 hello 資料只會置於緩衝區。 執行任何動作會當我們呼叫 hello 網路上傳輸**IoTHubClient\_LL\_SendEventAsync**。 在訂單 tooactually 輸入 hello 資料 tooIoT 中樞，您必須呼叫**IoTHubClient\_LL\_DoWork**，如這個範例所示：

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

此程式碼 (從 hello **iot 中樞\_用戶端\_範例\_http**應用程式) 重複呼叫**IoTHubClient\_LL\_DoWork**. 每次**IoTHubClient\_LL\_DoWork**是呼叫，從 hello 緩衝區 tooIoT 中樞傳送某些事件，而且它會擷取佇列的訊息傳送 toohello 裝置。 hello 後者的情況下表示，如果我們註冊回呼函式的訊息，然後 hello 會叫用回呼 （假設任何訊息的佇列）。 我們會註冊這類的回呼函式與 hello 如下的程式碼：

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

hello 原因**IoTHubClient\_LL\_DoWork**通常稱為迴圈是每次呼叫時，它會傳送*某些*緩衝事件 tooIoT 中樞並擷取*接下來 hello*訊息佇列中等待 hello 裝置。 每個呼叫不保證 toosend 所有經過緩衝處理的事件或 tooretrieve 所有排入佇列的訊息。 如果您想的 toosend hello 中的所有事件緩衝區，然後繼續執行上其他處理此迴圈可以取代 hello 如下的程式碼：

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

此程式碼會呼叫**IoTHubClient\_LL\_DoWork**之前已傳送嗨緩衝區中的所有事件 tooIoT 中樞。 請注意，這並未一併暗示已收到所有佇列的訊息。 部分 hello 這個錯誤是原因的，檢查 「 全部 」 的訊息不會為具決定性的動作。 如果您擷取"all"hello 訊息，但另一個然後傳送 toohello 裝置，會發生什麼情況之後立即？ 與更好的方式 toodeal 是經過程式設計逾時。 例如，hello 訊息回呼函式無法重設的計時器，每次叫用它。 然後您可以撰寫邏輯 toocontinue 處理，例如，沒有訊息所收到的 hello 上次*X*秒。

當您在完成的 ingressing 事件，並接收訊息，是確定 toocall hello 對應函式 tooclean 資源。

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

基本上是只有一組 Api toosend 利用背景執行緒與另一組 Api，並 hello hello 背景執行緒沒有相同的動作和接收資料。 許多開發人員可能偏好使用 hello 非-LL Api，但 hello 較低層級 Api 時很有用 hello 開發人員想要明確控制網路傳輸。 例如，有些裝置會隨時間收集資料，並且只在指定的時間間隔輸入事件 (例如，每小時一次或一天一次)。 hello 較低層級應用程式開發介面提供當您傳送和接收資料，或從 IoT 中樞時，hello 能力 tooexplicitly 控制項。 其他人只會偏好 hello 簡化較低層級 Api，提供該 hello。 Hello 主執行緒，而不是在 hello 背景某些工作發生的所有項目會發生。

您選擇，無論模型是確定 toobe 一致的應用程式開發介面中使用。 如果您藉由呼叫啟動**IoTHubClient\_LL\_CreateFromConnectionString**，確定您只使用 hello 對應較低層級 Api，任何後續追蹤的工作：

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

相反的 hello 也是如此。 如果您開始使用**IoTHubClient\_CreateFromConnectionString**，然後使用 hello 非-LL Api 進行任何其他處理。

在 [hello Azure IoT 裝置 SDK c，請參閱 hello **iot 中樞\_用戶端\_範例\_http** hello 的完整範例應用程式較低層級應用程式開發介面。 hello **iot 中樞\_用戶端\_範例\_amqp**應用程式可以如需完整範例的 hello 非-LL 應用程式開發介面參考。

## <a name="property-handling"></a>屬性處理
到目前為止我們已說明傳送資料，我們已被參照 toohello hello 訊息本文。 例如，請思考下列程式碼：

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

這個範例會傳送訊息 tooIoT 集線器與 hello 文字"Hello World"。 不過，IoT 中樞也可讓屬性 toobe 附加的 tooeach 訊息。 屬性是可附加的 toohello 訊息的名稱/值組。 例如，我們可以修改前一個程式碼 tooattach hello 屬性 toohello 訊息：

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

我們一開始呼叫**IoTHubMessage\_屬性**並將其傳遞訊息的 hello 控制代碼。 我們會得到回**對應\_處理**可讓我們 toostart 加入屬性的參考。 後者的 hello 伴隨著呼叫**對應\_AddOrUpdate**，其可接受參考 tooa 對應\_控制代碼、 hello 屬性名稱，以及 hello 屬性值。 利用此 API，我們可以依意願新增應用程式。

從讀取 hello 事件時**事件中心**，hello 接收者可以列舉 hello 屬性並擷取其對應的值。 例如，在.NET 中達成這點會藉由存取 hello [hello EventData 物件上的屬性集合](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx)。

在 hello 前一個範例中，我們正在將附加我們傳送給 tooIoT 中樞屬性 tooan 事件。 屬性也可以附加的 toomessages 接收從 IoT 中樞。 如果我們想要從訊息 tooretrieve 屬性，我們可以使用我們訊息回呼函式中的 hello 如下的程式碼：

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

太 hello 呼叫**IoTHubMessage\_屬性**傳回 hello**對應\_處理**參考。 我們再傳遞該參考太**對應\_GetInternals** tooobtain hello 名稱/值的參考 tooan 陣列配對 （以及 hello 屬性的計數）。 此時，它是列舉 hello 屬性 tooget toohello 值我們想要的簡單方式。

在您的應用程式中，您不需要 toouse 屬性。 不過，如果您需要 tooset 這些事件或擷取這些訊息，從 hello **IoTHubClient**程式庫可讓您輕鬆。

## <a name="message-handling"></a>訊息處理
如先前所述，當訊息抵達從 IoT 中樞 hello **IoTHubClient**回應叫用註冊的回呼函式的程式庫。 此函式有一個傳回參數值得額外說明。 以下是在 hello hello 回呼函式的摘錄**iot 中樞\_用戶端\_範例\_http**範例應用程式：

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

請注意，hello 傳回型別是**IOTHUBMESSAGE\_配置\_結果**，在這個特定案例，我們決定傳回**IOTHUBMESSAGE\_接受**。 有其他值，我們可以從這個函式傳回變更如何 hello **IoTHubClient**程式庫會做出反應 toohello 訊息回呼。 以下是 hello 選項。

* **IOTHUBMESSAGE\_接受**– hello 訊息已成功處理。 hello **IoTHubClient**程式庫不會叫用一次以 hello hello 回呼函式相同的訊息。
* **IOTHUBMESSAGE\_已拒絕**– hello 訊息尚未處理，而且沒有任何 desire toodo 動作 hello 未來。 hello **IoTHubClient**程式庫不叫用一次以 hello hello 回呼函式相同的訊息。
* **IOTHUBMESSAGE\_已放棄**– hello 訊息尚未處理成功，但 hello **IoTHubClient**程式庫應該要叫用一次以 hello hello 回呼函式相同的訊息。

Hello 前兩個傳回碼，hello **IoTHubClient**程式庫會傳送訊息 tooIoT 中樞 hello 訊息，指出應該從 hello 裝置佇列中刪除，並不會傳遞一次。 hello 淨效果為 hello 相同 （hello 訊息從佇列中刪除 hello 裝置），但仍會記錄 hello 訊息是否已接受或拒絕。  錄製區別這兩者是有用的 hello 訊息 toosenders 可以接聽的意見反應和了解，是否裝置已接受或拒絕特定的訊息。

在最後一個案例中 hello 訊息也會傳送 tooIoT 集線器，但它會指出該 hello 訊息應重新傳遞。 通常您會放棄的訊息，如果您遇到某些錯誤，但想 tootry tooprocess hello 訊息一次。 相較之下，拒絕的訊息適合，當您遇到無法復原的錯誤 （或如果您只需決定您不要 tooprocess hello 訊息）。

在任何情況下，請留意 hello 不同傳回碼，讓您可以引發您想要從 hello 的 hello 行為**IoTHubClient**程式庫。

## <a name="alternate-device-credentials"></a>替代裝置認證
如先前所述，hello 首先 toodo 時使用 hello **IoTHubClient**程式庫是 tooobtain **iot 中樞\_用戶端\_處理**例如 hello 呼叫下列：

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

hello 引數太**IoTHubClient\_CreateFromConnectionString** hello 裝置連接字串和表示我們使用 toocommunicate 與 IoT 中樞的 hello 通訊協定的參數。 hello 裝置連接字串的格式顯示，如下所示：

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

這個字串中包含四項資訊：IoT 中樞名稱、IoT 中樞尾碼、裝置識別碼和共用存取金鑰。 Hello Azure 入口網站中建立您的 IoT 中樞執行個體時，取得的 IoT 中樞的 hello 完整的網域名稱 (FQDN)，這可讓您 hello IoT 中樞名稱 （hello 第一部份 hello FQDN） 和 hello IoT 中樞後置詞 (hello rest 的 hello FQDN)。 當您註冊您的裝置與 IoT 中樞時，取得 hello 裝置識別碼和 hello 共用的存取金鑰 (hello 中所述[前一篇文章](iot-hub-device-sdk-c-intro.md))。

**IoTHubClient\_CreateFromConnectionString**可讓您其中一種方式 tooinitialize hello 程式庫。 如果您想要的話，您可以建立新**iot 中樞\_用戶端\_處理**使用這些個別的參數，而不是 hello 裝置連接字串。 這是以下列程式碼的 hello 來達成：

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

這可達成 hello 相同的動作**IoTHubClient\_CreateFromConnectionString**。

很明顯，您會想 toouse **IoTHubClient\_CreateFromConnectionString**而不是這個更多詳細資料的初始化方法。 但請記住，當您在 IoT 中樞註冊裝置時，您得到的是裝置識別碼和裝置金鑰 (不是連接字串)。 hello*裝置總管*hello 中導入的 SDK 工具[前一篇文章](iot-hub-device-sdk-c-intro.md)使用文件庫中 hello **Azure IoT 服務 SDK** toocreate hello 裝置中的連接字串hello 裝置識別碼、 裝置識別碼和 IoT 中樞的主機名稱。 因此呼叫**IoTHubClient\_LL\_建立**可能是更理想，因為它可以節省 hello 步驟產生連接字串。 使用任何方法都很方便。

## <a name="configuration-options"></a>組態選項
到目前為止的所有項目所述有關 hello 方式 hello **IoTHubClient**程式庫的運作方式會反映其預設行為。 不過，有一些您可以設定的 toochange hello 程式庫的運作方式的選項。 這會透過利用 hello **IoTHubClient\_LL\_SetOption**應用程式開發介面。 請思考此範例：

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

有一些常用的選項：

* **SetBatching** (bool) – 如果**true**，再傳送資料 tooIoT 中樞傳送批次中。 如果為 **false**，就表示訊息會個別傳送。 hello 預設值是**false**。 請注意該 hello **SetBatching**選項只適用於 toohello HTTP 通訊協定和不 toohello MQTT 或 AMQP 通訊協定。
* **Timeout** (unsigned int) - 這個值會以毫秒為單位表示。 如果要傳送的 HTTP 要求或接收回應使用超過這個時間，hello 連接逾時。

批次處理選項的 hello 很重要。 根據預設，hello 庫 ingresses 事件個別 (單一事件是任何您傳遞太**IoTHubClient\_LL\_SendEventAsync**)。 如果批次處理選項的 hello **true**，hello 程式庫會收集會從 hello 緩衝區 （向上 toohello IoT 中樞將會接受最大訊息大小） 的事件數目。  hello 事件批次傳送 tooIoT 中樞在單一 HTTP 呼叫 （hello 個別事件會配套到 JSON 陣列）。 啟用批次處理通常會導致效能大幅提升，因為網路來回行程正在減少。 它也會大幅減少頻寬，因為您正利用事件批次傳送一組 HTTP 標頭，而不是針對每個個別事件傳送一組標頭。 除非有特定原因 toodo，否則您通常會想 tooenable 批次處理。

## <a name="next-steps"></a>後續步驟
本文說明中的 hello 詳細 hello 行為**IoTHubClient** hello 中找到程式庫**C 的 Azure IoT 裝置 SDK**。利用此資訊，您應該深入了解的 hello hello 功能**IoTHubClient**程式庫。 hello[下一篇文章](iot-hub-device-sdk-c-serializer.md)hello 會類似的詳細說明**序列化程式**程式庫。

toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
