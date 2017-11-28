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
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="008fc-104">與您使用 hello MQTT 通訊協定的 IoT 中樞通訊</span><span class="sxs-lookup"><span data-stu-id="008fc-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="008fc-105">IoT 中樞讓裝置 toocommunicate hello IoT 中樞裝置端點使用 hello [MQTT v3.1.1] [ lnk-mqtt-org]連接埠 8883 或 MQTT v3.1.1 透過 WebSocket 通訊協定連接埠 443 上的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="008fc-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="008fc-106">IoT 中樞需要使用 TLS/SSL 來保護所有裝置通訊 toobe （因此，IoT 中樞不支援非安全連線透過連接埠 1883年）。</span><span class="sxs-lookup"><span data-stu-id="008fc-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="008fc-107">連接 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="008fc-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="008fc-108">裝置可以使用 hello MQTT 通訊協定 tooconnect tooan IoT 中樞透過 hello 文件庫中 hello [Azure IoT Sdk] [ lnk-device-sdks]或直接使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="008fc-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="008fc-109">使用 hello 裝置 Sdk</span><span class="sxs-lookup"><span data-stu-id="008fc-109">Using hello device SDKs</span></span>

<span data-ttu-id="008fc-110">[裝置 Sdk] [ lnk-device-sdks]該支援 hello MQTT 通訊協定可供 Java、 Node.js、 C、 C# 和 Python。</span><span class="sxs-lookup"><span data-stu-id="008fc-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="008fc-111">hello 裝置 Sdk 使用 hello 標準 IoT 中樞連接字串 tooestablish 連接 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="008fc-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="008fc-112">toouse hello MQTT 通訊協定 hello 用戶端通訊協定參數必須設定太**MQTT**。</span><span class="sxs-lookup"><span data-stu-id="008fc-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="008fc-113">根據預設，hello 裝置 Sdk 連線 tooan IoT 中樞與 hello **CleanSession**旗標設定得**0**並用**QoS 1**與 hello IoT 中樞的訊息交換。</span><span class="sxs-lookup"><span data-stu-id="008fc-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="008fc-114">當裝置連線的 tooan IoT 中樞時，hello 裝置 Sdk 會提供方法讓 hello 裝置 toosend 訊息 tooand 從 IoT 中心接收訊息。</span><span class="sxs-lookup"><span data-stu-id="008fc-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="008fc-115">hello 下表包含連結 toocode 範例對每個支援的語言指定 hello 參數 toouse tooestablish 連接 tooIoT 集線器使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="008fc-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="008fc-116">語言</span><span class="sxs-lookup"><span data-stu-id="008fc-116">Language</span></span> | <span data-ttu-id="008fc-117">通訊協定參數</span><span class="sxs-lookup"><span data-stu-id="008fc-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="008fc-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="008fc-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="008fc-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="008fc-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="008fc-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="008fc-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="008fc-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="008fc-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="008fc-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="008fc-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="008fc-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="008fc-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="008fc-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="008fc-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="008fc-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="008fc-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="008fc-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="008fc-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="008fc-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="008fc-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="008fc-128">從 AMQP tooMQTT 移轉裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="008fc-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="008fc-129">如果您使用 hello[裝置 Sdk][lnk-device-sdks]，從使用 AMQP 切換 tooMQTT 需要變更 hello 用戶端初始化在 hello 通訊協定參數，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="008fc-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="008fc-130">當此情況下，請確定 toocheck hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="008fc-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="008fc-131">AMQP 會傳回錯誤，以取得多個條件，而 MQTT 終止 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="008fc-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="008fc-132">因此，可能需要稍微變更您的例外狀況處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="008fc-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="008fc-133">MQTT 不支援 hello*拒絕*作業接收時[雲端到裝置訊息][lnk-messaging]。</span><span class="sxs-lookup"><span data-stu-id="008fc-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="008fc-134">如果您的後端應用程式需要 tooreceive hello 裝置應用程式的回應，請考慮使用[直接方法][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="008fc-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="008fc-135">直接使用 hello MQTT 通訊協定</span><span class="sxs-lookup"><span data-stu-id="008fc-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="008fc-136">如果裝置無法使用 hello 裝置 Sdk，它仍可連線 hello MQTT 通訊協定使用連接埠 8883 toohello 公用裝置端點。</span><span class="sxs-lookup"><span data-stu-id="008fc-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="008fc-137">在 hello**連接**封包 hello 裝置應使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="008fc-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="008fc-138">Hello **ClientId**欄位中，使用 hello **deviceId**。</span><span class="sxs-lookup"><span data-stu-id="008fc-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="008fc-139">Hello **Username**欄位中，使用`{iothubhostname}/{device_id}/api-version=2016-11-14`，其中 {iothubhostname} 是 hello hello IoT 中樞的完整 CName。</span><span class="sxs-lookup"><span data-stu-id="008fc-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="008fc-140">例如，如果 hello IoT 中樞的名稱是**contoso.azure devices.net** ，而且如果您的裝置 hello 名稱是**MyDevice01**，hello 完整**Username**欄位應包含`contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="008fc-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="008fc-141">Hello**密碼**欄位中，使用 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="008fc-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="008fc-142">hello 的 SAS token hello 格式 hello 相同 hello HTTP 和 AMQP 通訊協定：</span><span class="sxs-lookup"><span data-stu-id="008fc-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="008fc-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`。</span><span class="sxs-lookup"><span data-stu-id="008fc-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="008fc-144">如需有關如何 toogenerate SAS 權杖，請參閱 hello 裝置一節[使用 IoT 中樞安全性語彙基元][lnk-sas-tokens]。</span><span class="sxs-lookup"><span data-stu-id="008fc-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="008fc-145">測試時，您也可以使用 hello[裝置總管][ lnk-device-explorer]工具 tooquickly 產生 SAS 權杖，您可以複製並貼到您自己的程式碼：</span><span class="sxs-lookup"><span data-stu-id="008fc-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="008fc-146">移 toohello**管理**索引標籤中**裝置總管**。</span><span class="sxs-lookup"><span data-stu-id="008fc-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="008fc-147">按一下 [SAS 權杖]  \(右上角)。</span><span class="sxs-lookup"><span data-stu-id="008fc-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="008fc-148">在**SASTokenForm**，選取您的裝置在 hello **DeviceID**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="008fc-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="008fc-149">設定您的 **TTL**。</span><span class="sxs-lookup"><span data-stu-id="008fc-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="008fc-150">按一下**產生**toocreate 您的權杖。</span><span class="sxs-lookup"><span data-stu-id="008fc-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="008fc-151">hello SAS 權杖，而會產生具有這個結構： `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。</span><span class="sxs-lookup"><span data-stu-id="008fc-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="008fc-152">hello hello 為這個語彙基元 toouse 一部分**密碼**欄位 tooconnect 使用 MQTT 是： `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。</span><span class="sxs-lookup"><span data-stu-id="008fc-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="008fc-153">對於 MQTT 連線和中斷連線的封包，IoT 中樞發出 hello 事件**作業監視**通道的其他資訊可幫助您 tootroubleshoot 連線問題。</span><span class="sxs-lookup"><span data-stu-id="008fc-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="008fc-154">傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="008fc-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="008fc-155">成功連接後，裝置可以傳送訊息 tooIoT 集線器使用`devices/{device_id}/messages/events/`或`devices/{device_id}/messages/events/{property_bag}`為**主題名稱**。</span><span class="sxs-lookup"><span data-stu-id="008fc-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="008fc-156">hello`{property_bag}`項目可讓 hello 裝置 toosend 訊息以 url 編碼格式的額外屬性。</span><span class="sxs-lookup"><span data-stu-id="008fc-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="008fc-157">例如：</span><span class="sxs-lookup"><span data-stu-id="008fc-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="008fc-158">這`{property_bag}`項目使用 hello 相同的編碼方式與 hello HTTP 通訊協定中的查詢字串一樣。</span><span class="sxs-lookup"><span data-stu-id="008fc-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="008fc-159">hello 裝置應用程式也可以使用`devices/{device_id}/messages/events/{property_bag}`為 hello**將主題名稱**toodefine*將訊息*toobe 以遙測訊息轉送。</span><span class="sxs-lookup"><span data-stu-id="008fc-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="008fc-160">「IoT 中樞」不支援 QoS 2 訊息。</span><span class="sxs-lookup"><span data-stu-id="008fc-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="008fc-161">如果裝置應用程式發佈的訊息**QoS 2**，IoT 中樞關閉 hello 網路連接。</span><span class="sxs-lookup"><span data-stu-id="008fc-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="008fc-162">「IoT 中樞」不會保存「保留」訊息。</span><span class="sxs-lookup"><span data-stu-id="008fc-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="008fc-163">如果裝置傳送 hello 訊息**保留**旗標設定 too1、 IoT 中樞將 hello **x-opt-保留**應用程式屬性 toohello 訊息。</span><span class="sxs-lookup"><span data-stu-id="008fc-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="008fc-164">在此情況下，而不是保存的 hello 保留的訊息，IoT 中樞將它傳遞至 toohello 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="008fc-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="008fc-165">IoT 中樞僅支援每個裝置有一個作用中 MQTT 連接。</span><span class="sxs-lookup"><span data-stu-id="008fc-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="008fc-166">任何新 MQTT 連線 hello 代表相同的裝置識別碼會導致 IoT 中樞 toodrop hello 現有的連接。</span><span class="sxs-lookup"><span data-stu-id="008fc-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="008fc-167">如需詳細資訊，請參閱[傳訊開發人員指南][lnk-messaging]。</span><span class="sxs-lookup"><span data-stu-id="008fc-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="008fc-168">接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="008fc-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="008fc-169">從 IoT 中樞 tooreceive 郵件，裝置應該使用訂閱`devices/{device_id}/messages/devicebound/#`為**主題篩選**。</span><span class="sxs-lookup"><span data-stu-id="008fc-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="008fc-170">hello 多層級的萬用字元 **#** 在 hello 主題篩選器會使用僅 tooallow hello 裝置 hello 主題名稱中的 tooreceive 其他屬性。</span><span class="sxs-lookup"><span data-stu-id="008fc-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="008fc-171">IoT 中樞不允許的 hello hello 使用量 **#** 或**嗎？**</span><span class="sxs-lookup"><span data-stu-id="008fc-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="008fc-172">萬用字元來篩選副主題。</span><span class="sxs-lookup"><span data-stu-id="008fc-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="008fc-173">IoT 中樞不是一般用途 pub 子訊息代理人，因為它只支援 hello 記載的主題名稱和主題篩選條件。</span><span class="sxs-lookup"><span data-stu-id="008fc-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="008fc-174">hello 裝置未收到任何訊息從 IoT 中樞，直到它已成功訂閱 tooits 裝置特定端點，由 hello`devices/{device_id}/messages/devicebound/#`主題篩選器。</span><span class="sxs-lookup"><span data-stu-id="008fc-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="008fc-175">在建立成功的訂用帳戶之後，hello 裝置就會開始接收僅雲端到裝置訊息已傳送 tooit hello 訂用帳戶的 hello 時間之後。</span><span class="sxs-lookup"><span data-stu-id="008fc-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="008fc-176">如果 hello 裝置連線與**CleanSession**旗標設定得**0**，hello 訂用帳戶會在不同的工作階段之間保存。</span><span class="sxs-lookup"><span data-stu-id="008fc-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="008fc-177">在此情況下，hello 與連接的下一次**CleanSession 0** hello 裝置接收到未處理的訊息已傳送 tooit 時已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="008fc-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="008fc-178">如果使用 hello 裝置**CleanSession**旗標設定得**1**但未收到任何訊息從 IoT 中樞直到它訂閱 tooits 裝置端點。</span><span class="sxs-lookup"><span data-stu-id="008fc-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="008fc-179">IoT 中樞傳送 hello 訊息**主題名稱** `devices/{device_id}/messages/devicebound/`，或`devices/{device_id}/messages/devicebound/{property_bag}`是否有任何訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="008fc-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="008fc-180">`{property_bag}` 包含訊息屬性的 url 編碼索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="008fc-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="008fc-181">只有應用程式內容和使用者可設定系統屬性 (例如**messageId**或**correlationId**) 隨附的 hello 屬性包。</span><span class="sxs-lookup"><span data-stu-id="008fc-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="008fc-182">系統屬性名稱有 hello 前置詞 **$** ，應用程式屬性沒有前置詞使用 hello 原始屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="008fc-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="008fc-183">當裝置應用程式會訂閱具有 tooa 主題**QoS 2**，IoT 中樞授與最大 QoS 層級 1 中 hello **SUBACK**封包。</span><span class="sxs-lookup"><span data-stu-id="008fc-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="008fc-184">IoT 中樞之後，會傳遞訊息 toohello 裝置使用 QoS 1。</span><span class="sxs-lookup"><span data-stu-id="008fc-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="008fc-185">擷取裝置對應項屬性</span><span class="sxs-lookup"><span data-stu-id="008fc-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="008fc-186">首先，裝置訂閱太`$iothub/twin/res/#`，tooreceive hello 作業的回應。</span><span class="sxs-lookup"><span data-stu-id="008fc-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="008fc-187">然後，它會傳送空白訊息 tootopic `$iothub/twin/GET/?$rid={request id}`，使用已填入的值為**要求識別碼**。 hello 服務然後會傳送回應訊息，其中包含主題上的 hello 裝置兩個資料`$iothub/twin/res/{status}/?$rid={request id}`，使用 hello 相同**要求識別碼**與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="008fc-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="008fc-188">根據 [IoT 中樞傳訊開發人員指南][lnk-messaging]，要求識別碼可以是任何有效的訊息屬性值，而狀態會驗證為整數。</span><span class="sxs-lookup"><span data-stu-id="008fc-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="008fc-189">hello 回應主體會包含 hello 屬性 hello 裝置兩個區段：</span><span class="sxs-lookup"><span data-stu-id="008fc-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="008fc-190">hello 主體 hello 識別登錄項目有限制 toohello 「 屬性 」 成員，例如：</span><span class="sxs-lookup"><span data-stu-id="008fc-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

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

<span data-ttu-id="008fc-191">hello 可能的狀態碼如下：</span><span class="sxs-lookup"><span data-stu-id="008fc-191">hello possible status codes are:</span></span>

|<span data-ttu-id="008fc-192">狀態</span><span class="sxs-lookup"><span data-stu-id="008fc-192">Status</span></span> | <span data-ttu-id="008fc-193">說明</span><span class="sxs-lookup"><span data-stu-id="008fc-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="008fc-194">200</span><span class="sxs-lookup"><span data-stu-id="008fc-194">200</span></span> | <span data-ttu-id="008fc-195">成功</span><span class="sxs-lookup"><span data-stu-id="008fc-195">Success</span></span> |
| <span data-ttu-id="008fc-196">429</span><span class="sxs-lookup"><span data-stu-id="008fc-196">429</span></span> | <span data-ttu-id="008fc-197">要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="008fc-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="008fc-198">5**</span><span class="sxs-lookup"><span data-stu-id="008fc-198">5**</span></span> | <span data-ttu-id="008fc-199">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="008fc-199">Server errors</span></span> |

<span data-ttu-id="008fc-200">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="008fc-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="008fc-201">更新裝置對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="008fc-201">Update device twin's reported properties</span></span>

<span data-ttu-id="008fc-202">hello 下列順序說明裝置 hello 的更新方式回報 hello 裝置的兩個在 IoT 中樞中的屬性：</span><span class="sxs-lookup"><span data-stu-id="008fc-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="008fc-203">裝置必須先訂閱 toohello`$iothub/twin/res/#`主題 tooreceive hello 作業的回應，或從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="008fc-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="008fc-204">裝置傳送訊息，將包含 hello 裝置兩個更新 toohello`$iothub/twin/PATCH/properties/reported/?$rid={request id}`主題。</span><span class="sxs-lookup"><span data-stu-id="008fc-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="008fc-205">此訊息包含 **request id** 值。</span><span class="sxs-lookup"><span data-stu-id="008fc-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="008fc-206">hello 服務，然後傳送回應訊息包含 hello 新 ETag 值 hello 主題上的報告的屬性集合`$iothub/twin/res/{status}/?$rid={request id}`。</span><span class="sxs-lookup"><span data-stu-id="008fc-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="008fc-207">此回應訊息，會使用 hello 相同**要求識別碼**與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="008fc-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="008fc-208">hello 要求訊息主體包含 JSON 文件，提供新的值 （沒有其他屬性或中繼資料可進行修改） 的報告屬性。</span><span class="sxs-lookup"><span data-stu-id="008fc-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="008fc-209">Hello JSON 文件中的每個成員會更新，或將 hello 裝置兩個的文件中的 hello 相對應的成員。</span><span class="sxs-lookup"><span data-stu-id="008fc-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="008fc-210">成員設定得`null`，刪除 hello 從 hello 包含物件的成員。</span><span class="sxs-lookup"><span data-stu-id="008fc-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="008fc-211">例如：</span><span class="sxs-lookup"><span data-stu-id="008fc-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="008fc-212">hello 可能的狀態碼如下：</span><span class="sxs-lookup"><span data-stu-id="008fc-212">hello possible status codes are:</span></span>

|<span data-ttu-id="008fc-213">狀態</span><span class="sxs-lookup"><span data-stu-id="008fc-213">Status</span></span> | <span data-ttu-id="008fc-214">說明</span><span class="sxs-lookup"><span data-stu-id="008fc-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="008fc-215">200</span><span class="sxs-lookup"><span data-stu-id="008fc-215">200</span></span> | <span data-ttu-id="008fc-216">成功</span><span class="sxs-lookup"><span data-stu-id="008fc-216">Success</span></span> |
| <span data-ttu-id="008fc-217">400</span><span class="sxs-lookup"><span data-stu-id="008fc-217">400</span></span> | <span data-ttu-id="008fc-218">不正確的要求。</span><span class="sxs-lookup"><span data-stu-id="008fc-218">Bad Request.</span></span> <span data-ttu-id="008fc-219">JSON 格式錯誤</span><span class="sxs-lookup"><span data-stu-id="008fc-219">Malformed JSON</span></span> |
| <span data-ttu-id="008fc-220">429</span><span class="sxs-lookup"><span data-stu-id="008fc-220">429</span></span> | <span data-ttu-id="008fc-221">要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="008fc-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="008fc-222">5**</span><span class="sxs-lookup"><span data-stu-id="008fc-222">5**</span></span> | <span data-ttu-id="008fc-223">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="008fc-223">Server errors</span></span> |

<span data-ttu-id="008fc-224">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="008fc-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="008fc-225">接收所需屬性更新通知</span><span class="sxs-lookup"><span data-stu-id="008fc-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="008fc-226">IoT 中樞連接裝置之後，傳送通知 toohello 主題`$iothub/twin/PATCH/properties/desired/?$version={new version}`，其中包含 hello hello hello 方案後端所執行的更新內容。</span><span class="sxs-lookup"><span data-stu-id="008fc-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="008fc-227">例如：</span><span class="sxs-lookup"><span data-stu-id="008fc-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="008fc-228">內容更新與`null`hello JSON 的值表示物件正在刪除成員。</span><span class="sxs-lookup"><span data-stu-id="008fc-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="008fc-229">IoT 中樞只會在連接裝置時產生變更通知。</span><span class="sxs-lookup"><span data-stu-id="008fc-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="008fc-230">請確定 tooimplement hello[裝置重新連線流程][ lnk-devguide-twin-reconnection] tookeep hello 所需的 IoT 中樞與 hello 裝置應用程式之間的同步處理的屬性。</span><span class="sxs-lookup"><span data-stu-id="008fc-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="008fc-231">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="008fc-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="008fc-232">回應 tooa 直接方法</span><span class="sxs-lookup"><span data-stu-id="008fc-232">Respond tooa direct method</span></span>

<span data-ttu-id="008fc-233">首先，裝置必須 toosubscribe 太`$iothub/methods/POST/#`。</span><span class="sxs-lookup"><span data-stu-id="008fc-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="008fc-234">IoT 中樞傳送方法要求 toohello 主題`$iothub/methods/POST/{method name}/?$rid={request id}`、 具有有效的 JSON 或空的本文。</span><span class="sxs-lookup"><span data-stu-id="008fc-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="008fc-235">toorespond，hello 裝置傳送訊息，其中的有效的 JSON 或空本文 toohello 主題`$iothub/methods/res/{status}/?$rid={request id}`，其中**要求識別碼**具有 toomatch hello 中 hello 要求訊息，和**狀態**具有 toobe 整數.</span><span class="sxs-lookup"><span data-stu-id="008fc-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="008fc-236">如需詳細資訊，請參閱[直接方法開發人員指南][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="008fc-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="008fc-237">其他考量</span><span class="sxs-lookup"><span data-stu-id="008fc-237">Additional considerations</span></span>

<span data-ttu-id="008fc-238">做為最後的考量，如果您需要 toocustomize hello MQTT 通訊協定的行為在 hello 雲端端，您應該檢視 hello [Azure IoT 通訊協定閘道][ lnk-azure-protocol-gateway] ，可讓您 toodeploy 高效能IoT 中樞直接與介面的自訂通訊協定閘道。</span><span class="sxs-lookup"><span data-stu-id="008fc-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="008fc-239">hello Azure IoT 通訊協定閘道可讓您 toocustomize hello 裝置通訊協定 tooaccommodate brownfield MQTT 部署或其他自訂通訊協定。</span><span class="sxs-lookup"><span data-stu-id="008fc-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="008fc-240">不過，這種方法會要求您執行及操作自訂通訊協定閘道。</span><span class="sxs-lookup"><span data-stu-id="008fc-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="008fc-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="008fc-241">Next steps</span></span>

<span data-ttu-id="008fc-242">toolearn hello MQTT 通訊協定，詳細資料，請參閱 「 hello [MQTT 文件][lnk-mqtt-docs]。</span><span class="sxs-lookup"><span data-stu-id="008fc-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="008fc-243">toolearn 有關規劃您的 IoT 中樞部署的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="008fc-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="008fc-244">[Azure IoT 認證裝置目錄][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="008fc-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="008fc-245">[支援其他通訊協定][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="008fc-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="008fc-246">[與事件中樞比較][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="008fc-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="008fc-247">[縮放、HA 及 DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="008fc-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="008fc-248">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="008fc-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="008fc-249">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="008fc-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="008fc-250">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="008fc-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
