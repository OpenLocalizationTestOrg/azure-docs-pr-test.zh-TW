---
title: "了解 Azure IoT 中樞 MQTT 支援 | Microsoft Docs"
description: "開發人員指南 - 支援裝置使用 MQTT 通訊協定連接至 IoT 中樞對向端點。 包含 Azure IoT 裝置 SDK 內建的 MQTT 支援的相關資訊。"
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
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="abb7c-104">使用 MQTT 通訊協定來與 IoT 中樞通訊</span><span class="sxs-lookup"><span data-stu-id="abb7c-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="abb7c-105">「IoT 中樞」可讓裝置在連接埠 8883 使用 [MQTT v3.1.1][lnk-mqtt-org] 通訊協定，或在連接埠 443 使用「透過 WebSocket 的 MQTT v3.1.1」通訊協定，來與「IoT 中樞」裝置端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="abb7c-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="abb7c-106">「IoT 中樞」要求使用 TLS/SSL 保護所有裝置通訊的安全 (因此，「IoT 中樞」並不支援透過連接埠 1883 的非安全連線)。</span><span class="sxs-lookup"><span data-stu-id="abb7c-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="abb7c-107">連接到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="abb7c-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="abb7c-108">裝置可以使用 MQTT 通訊協定連接到 IoT 中樞，方法是使用 [Azure IoT SDK][lnk-device-sdks] 中的程式庫或直接使用 MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="abb7c-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="abb7c-109">使用裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="abb7c-109">Using the device SDKs</span></span>

<span data-ttu-id="abb7c-110">支援 MQTT 通訊協定的[裝置 SDK][lnk-device-sdks] 有提供 Java、Node.js、C、C# 和 Python 等版本。</span><span class="sxs-lookup"><span data-stu-id="abb7c-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="abb7c-111">裝置 SDK 會使用標準的 IoT 中樞連接字串來連接到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="abb7c-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="abb7c-112">若要使用 MQTT 通訊協定，用戶端通訊協定參數必須設定為 **MQTT**。</span><span class="sxs-lookup"><span data-stu-id="abb7c-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="abb7c-113">根據預設，裝置 SDK 會連接到 **CleanSession** 旗標設為 **0** 的 IoT 中樞，並使用 **QoS 1** 來與 IoT 中樞交換訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="abb7c-114">當裝置連接到 IoT 中樞時，裝置 SDK 會提供方法讓裝置在 IoT 中樞傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="abb7c-115">下表包含每一種支援語言的程式碼範例連結，並指出要用來以 MQTT 通訊協定連接到 IoT 中樞的參數。</span><span class="sxs-lookup"><span data-stu-id="abb7c-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="abb7c-116">語言</span><span class="sxs-lookup"><span data-stu-id="abb7c-116">Language</span></span> | <span data-ttu-id="abb7c-117">通訊協定參數</span><span class="sxs-lookup"><span data-stu-id="abb7c-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="abb7c-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="abb7c-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="abb7c-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="abb7c-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="abb7c-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="abb7c-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="abb7c-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="abb7c-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="abb7c-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="abb7c-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="abb7c-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="abb7c-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="abb7c-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="abb7c-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="abb7c-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="abb7c-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="abb7c-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="abb7c-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="abb7c-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="abb7c-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="abb7c-128">將裝置應用程式從 AMQP 移轉至 MQTT</span><span class="sxs-lookup"><span data-stu-id="abb7c-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="abb7c-129">如果您使用[裝置 SDK][lnk-device-sdks]，則需要在用戶端初始化中變更通訊協定參數 (如上所述)，才能從 AMQP 切換為使用 MQTT。</span><span class="sxs-lookup"><span data-stu-id="abb7c-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="abb7c-130">這麼做時，請務必檢查下列項目︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="abb7c-131">AMQP 在許多情況下會傳回錯誤，而 MQTT 會終止連線。</span><span class="sxs-lookup"><span data-stu-id="abb7c-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="abb7c-132">因此，可能需要稍微變更您的例外狀況處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="abb7c-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="abb7c-133">MQTT 在接收[雲端到裝置訊息][lnk-messaging]時不支援「拒絕」作業。</span><span class="sxs-lookup"><span data-stu-id="abb7c-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="abb7c-134">如果您的後端應用程式需要接收來自裝置應用程式的回應，請考慮使用[直接方法][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="abb7c-135">直接使用 MQTT 通訊協定</span><span class="sxs-lookup"><span data-stu-id="abb7c-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="abb7c-136">如果裝置無法使用裝置 SDK，它仍可使用連接埠 8883 上的 MQTT 通訊協定連線到公用裝置端點。</span><span class="sxs-lookup"><span data-stu-id="abb7c-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="abb7c-137">在 **CONNECT** 封包中，裝置應使用下列值：</span><span class="sxs-lookup"><span data-stu-id="abb7c-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="abb7c-138">在 [ClientId] 欄位中，使用 **deviceId**。</span><span class="sxs-lookup"><span data-stu-id="abb7c-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="abb7c-139">在 [Username] 欄位中，使用 `{iothubhostname}/{device_id}/api-version=2016-11-14`，其中 {iothubhostname} 是 IoT 中樞的完整 CName。</span><span class="sxs-lookup"><span data-stu-id="abb7c-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="abb7c-140">例如，如果您的 IoT 中樞名稱是 **contoso.azure-devices.net**，而且如果您的裝置名稱是 **MyDevice01**，則完整的 **Username** 欄位應包含 `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`。</span><span class="sxs-lookup"><span data-stu-id="abb7c-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="abb7c-141">在 [Password] 欄位中，使用 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="abb7c-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="abb7c-142">SAS 權杖的格式與 HTTP 和 AMQP 通訊協定的格式相同：</span><span class="sxs-lookup"><span data-stu-id="abb7c-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="abb7c-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`。</span><span class="sxs-lookup"><span data-stu-id="abb7c-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="abb7c-144">如需如何產生 SAS 權杖的詳細資訊，請參閱[使用 IoT 中樞安全性權杖][lnk-sas-tokens]的裝置一節。</span><span class="sxs-lookup"><span data-stu-id="abb7c-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="abb7c-145">測試時，您也可以使用[裝置總管][lnk-device-explorer]工具來快速產生 SAS 權杖，方便您複製並貼到您的程式碼中︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="abb7c-146">移至 [裝置總管] 中的 [管理] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="abb7c-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="abb7c-147">按一下 [SAS 權杖]  \(右上角)。</span><span class="sxs-lookup"><span data-stu-id="abb7c-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="abb7c-148">在 [SASTokenForm] 的 [DeviceID] 下拉式清單中，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="abb7c-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="abb7c-149">設定您的 **TTL**。</span><span class="sxs-lookup"><span data-stu-id="abb7c-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="abb7c-150">按一下 [產生]  來建立您的權杖。</span><span class="sxs-lookup"><span data-stu-id="abb7c-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="abb7c-151">產生的 SAS 權杖具有此結構：`HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。</span><span class="sxs-lookup"><span data-stu-id="abb7c-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="abb7c-152">使用 MQTT 連線時，此權杖中作為 [Password] 欄位的部分是︰`SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`。</span><span class="sxs-lookup"><span data-stu-id="abb7c-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="abb7c-153">針對 MQTT 的連接和中斷連接封包，「IoT 中樞」會在「作業監視」通道發出事件，其中包含可協助您對連線問題進行疑難排解的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="abb7c-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="abb7c-154">傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="abb7c-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="abb7c-155">成功連線之後，裝置可以使用 `devices/{device_id}/messages/events/` 或 `devices/{device_id}/messages/events/{property_bag}` 作為**主題名稱**，將訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="abb7c-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="abb7c-156">`{property_bag}` 項目可讓裝置以 URL 編碼格式傳送具有其他屬性的訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="abb7c-157">例如：</span><span class="sxs-lookup"><span data-stu-id="abb7c-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="abb7c-158">此 `{property_bag}` 項目與 HTTP 通訊協定中的查詢字串使用相同的編碼。</span><span class="sxs-lookup"><span data-stu-id="abb7c-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="abb7c-159">裝置應用程式也可以使用 `devices/{device_id}/messages/events/{property_bag}` 作為 **Will 主題名稱**，以定義要當作遙測訊息轉送的「Will 訊息」。</span><span class="sxs-lookup"><span data-stu-id="abb7c-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="abb7c-160">「IoT 中樞」不支援 QoS 2 訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="abb7c-161">如果裝置應用程式發佈 **QoS 2** 的訊息，IoT 中樞會關閉網路連接。</span><span class="sxs-lookup"><span data-stu-id="abb7c-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="abb7c-162">「IoT 中樞」不會保存「保留」訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="abb7c-163">如果裝置傳送 **RETAIN** 旗標設定為 1 的訊息，「IoT 中樞」會在訊息中加入 **x-opt-retain** 應用程式屬性。</span><span class="sxs-lookup"><span data-stu-id="abb7c-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="abb7c-164">在此情況下，「IoT 中樞」不會保存保留訊息，而是會傳遞給後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="abb7c-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="abb7c-165">IoT 中樞僅支援每個裝置有一個作用中 MQTT 連接。</span><span class="sxs-lookup"><span data-stu-id="abb7c-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="abb7c-166">代表相同裝置識別碼的任何新的 MQTT 連接都會導致 IoT 中樞卸除現有的連接。</span><span class="sxs-lookup"><span data-stu-id="abb7c-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="abb7c-167">如需詳細資訊，請參閱[傳訊開發人員指南][lnk-messaging]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="abb7c-168">接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="abb7c-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="abb7c-169">若要從 IoT 中樞接收訊息，裝置應該使用 `devices/{device_id}/messages/devicebound/#` 做為**主題篩選**來進行訂閱。</span><span class="sxs-lookup"><span data-stu-id="abb7c-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="abb7c-170">「主題篩選」中的多層級萬用字元 **#** 僅供用來允許裝置接收主題名稱中的額外屬性。</span><span class="sxs-lookup"><span data-stu-id="abb7c-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="abb7c-171">「IoT 中樞」並不允許使用 **#** 或 **?**</span><span class="sxs-lookup"><span data-stu-id="abb7c-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="abb7c-172">萬用字元來篩選副主題。</span><span class="sxs-lookup"><span data-stu-id="abb7c-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="abb7c-173">由於「IoT 中樞」不是一般用途的發行/訂閱傳訊訊息代理程式，因此它只支援已記載的主題名稱和主題篩選。</span><span class="sxs-lookup"><span data-stu-id="abb7c-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="abb7c-174">裝置在成功訂閱 IoT 中樞的裝置特定端點 (由 `devices/{device_id}/messages/devicebound/#` 主題篩選代表) 之後，才會收到來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="abb7c-175">建立成功的訂閱之後，裝置將會開始接收訊息，但僅限在訂閱之後傳送給它的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="abb7c-176">如果裝置是在 **CleanSession** 旗標設定為 **0** 的情況下連線，訂閱將會跨不同的工作階段持續保留。</span><span class="sxs-lookup"><span data-stu-id="abb7c-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="abb7c-177">在此情況下，下次裝置以 **CleanSession 0** 進行連線時，就會收到在其中斷連線時傳送給它的未送訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="abb7c-178">如果裝置使用設定為 **1** 的 **CleanSession** 旗標，則必須等到訂閱 IoT 中樞的裝置端點之後，才會收到來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="abb7c-179">IoT 中樞會附上**主題名稱** `devices/{device_id}/messages/devicebound/` 或 `devices/{device_id}/messages/devicebound/{property_bag}` (如果有任何訊息屬性) 來傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="abb7c-180">`{property_bag}` 包含訊息屬性的 url 編碼索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="abb7c-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="abb7c-181">屬性包中只會包含應用程式屬性和使用者可設定的系統屬性 (例如 **messageId** 或 **correlationId**)。</span><span class="sxs-lookup"><span data-stu-id="abb7c-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="abb7c-182">系統屬性名稱具有前置詞 **$**，但應用程式屬性則會使用沒有前置詞的原始屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="abb7c-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="abb7c-183">當裝置應用程式訂閱具有 **QoS 2** 的主題時，IoT 中樞會在 **SUBACK** 封包中授與最大 QoS 層級 1。</span><span class="sxs-lookup"><span data-stu-id="abb7c-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="abb7c-184">之後，IoT 中樞會使用 QoS 1 將訊息傳遞給裝置。</span><span class="sxs-lookup"><span data-stu-id="abb7c-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="abb7c-185">擷取裝置對應項屬性</span><span class="sxs-lookup"><span data-stu-id="abb7c-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="abb7c-186">首先，裝置會訂閱 `$iothub/twin/res/#`，以接收作業的回應。</span><span class="sxs-lookup"><span data-stu-id="abb7c-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="abb7c-187">然後，它會傳送空白訊息給主題 `$iothub/twin/GET/?$rid={request id}`，其中已填入**要求識別碼**的值。</span><span class="sxs-lookup"><span data-stu-id="abb7c-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="abb7c-188">服務接著會使用和要求相同的**要求識別碼**，傳送內含關於 `$iothub/twin/res/{status}/?$rid={request id}` 主題之裝置對應項資料的回應訊息。</span><span class="sxs-lookup"><span data-stu-id="abb7c-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="abb7c-189">根據 [IoT 中樞傳訊開發人員指南][lnk-messaging]，要求識別碼可以是任何有效的訊息屬性值，而狀態會驗證為整數。</span><span class="sxs-lookup"><span data-stu-id="abb7c-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="abb7c-190">回應本文包含裝置對應項的屬性區段：</span><span class="sxs-lookup"><span data-stu-id="abb7c-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="abb7c-191">身分識別登錄項目的本文僅限於 “properties” 成員，例如：</span><span class="sxs-lookup"><span data-stu-id="abb7c-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

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

<span data-ttu-id="abb7c-192">可能的狀態碼如下︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-192">The possible status codes are:</span></span>

|<span data-ttu-id="abb7c-193">狀態</span><span class="sxs-lookup"><span data-stu-id="abb7c-193">Status</span></span> | <span data-ttu-id="abb7c-194">說明</span><span class="sxs-lookup"><span data-stu-id="abb7c-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="abb7c-195">200</span><span class="sxs-lookup"><span data-stu-id="abb7c-195">200</span></span> | <span data-ttu-id="abb7c-196">成功</span><span class="sxs-lookup"><span data-stu-id="abb7c-196">Success</span></span> |
| <span data-ttu-id="abb7c-197">429</span><span class="sxs-lookup"><span data-stu-id="abb7c-197">429</span></span> | <span data-ttu-id="abb7c-198">要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="abb7c-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="abb7c-199">5**</span><span class="sxs-lookup"><span data-stu-id="abb7c-199">5**</span></span> | <span data-ttu-id="abb7c-200">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="abb7c-200">Server errors</span></span> |

<span data-ttu-id="abb7c-201">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="abb7c-202">更新裝置對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="abb7c-202">Update device twin's reported properties</span></span>

<span data-ttu-id="abb7c-203">下列順序說明在 IoT 中樞的裝置對應項中，裝置如何更新報告的屬性︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="abb7c-204">裝置必須訂閱 `$iothub/twin/res/#` 主題，才能從 IoT 中樞接收作業的回應。</span><span class="sxs-lookup"><span data-stu-id="abb7c-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="abb7c-205">裝置會將包含裝置對應項新的訊息傳送至 `$iothub/twin/PATCH/properties/reported/?$rid={request id}` 主題。</span><span class="sxs-lookup"><span data-stu-id="abb7c-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="abb7c-206">此訊息包含 **request id** 值。</span><span class="sxs-lookup"><span data-stu-id="abb7c-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="abb7c-207">服務接著會傳送回應訊息，其中包含`$iothub/twin/res/{status}/?$rid={request id}` 主題上報告之屬性集合的新 ETag 值。</span><span class="sxs-lookup"><span data-stu-id="abb7c-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="abb7c-208">這個回應訊息使用和要求相同的 **request id**。</span><span class="sxs-lookup"><span data-stu-id="abb7c-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="abb7c-209">要求訊息本文包含一份 JSON 文件，可提供所報告屬性的新值 (其他屬性或中繼資料則不可修改)。</span><span class="sxs-lookup"><span data-stu-id="abb7c-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="abb7c-210">JSON 文件中的每個成員會在裝置對應項的文件中更新或新增對應的成員。</span><span class="sxs-lookup"><span data-stu-id="abb7c-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="abb7c-211">設定為 `null` 的成員會從包含的物件中刪除成員。</span><span class="sxs-lookup"><span data-stu-id="abb7c-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="abb7c-212">例如：</span><span class="sxs-lookup"><span data-stu-id="abb7c-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="abb7c-213">可能的狀態碼如下︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-213">The possible status codes are:</span></span>

|<span data-ttu-id="abb7c-214">狀態</span><span class="sxs-lookup"><span data-stu-id="abb7c-214">Status</span></span> | <span data-ttu-id="abb7c-215">說明</span><span class="sxs-lookup"><span data-stu-id="abb7c-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="abb7c-216">200</span><span class="sxs-lookup"><span data-stu-id="abb7c-216">200</span></span> | <span data-ttu-id="abb7c-217">成功</span><span class="sxs-lookup"><span data-stu-id="abb7c-217">Success</span></span> |
| <span data-ttu-id="abb7c-218">400</span><span class="sxs-lookup"><span data-stu-id="abb7c-218">400</span></span> | <span data-ttu-id="abb7c-219">不正確的要求。</span><span class="sxs-lookup"><span data-stu-id="abb7c-219">Bad Request.</span></span> <span data-ttu-id="abb7c-220">JSON 格式錯誤</span><span class="sxs-lookup"><span data-stu-id="abb7c-220">Malformed JSON</span></span> |
| <span data-ttu-id="abb7c-221">429</span><span class="sxs-lookup"><span data-stu-id="abb7c-221">429</span></span> | <span data-ttu-id="abb7c-222">要求過多 (已節流)，根據 [IoT 中樞節流][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="abb7c-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="abb7c-223">5**</span><span class="sxs-lookup"><span data-stu-id="abb7c-223">5**</span></span> | <span data-ttu-id="abb7c-224">伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="abb7c-224">Server errors</span></span> |

<span data-ttu-id="abb7c-225">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="abb7c-226">接收所需屬性更新通知</span><span class="sxs-lookup"><span data-stu-id="abb7c-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="abb7c-227">當連接裝置時，IoT 中樞傳送通知給主題 `$iothub/twin/PATCH/properties/desired/?$version={new version}`，其中包含解決方案後端所執行的更新內容。</span><span class="sxs-lookup"><span data-stu-id="abb7c-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="abb7c-228">例如：</span><span class="sxs-lookup"><span data-stu-id="abb7c-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="abb7c-229">和屬性更新一樣，`null` 值表示將要刪除的 JSON 物件成員。</span><span class="sxs-lookup"><span data-stu-id="abb7c-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="abb7c-230">IoT 中樞只會在連接裝置時產生變更通知。</span><span class="sxs-lookup"><span data-stu-id="abb7c-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="abb7c-231">請務必實作[裝置重新連線流程][lnk-devguide-twin-reconnection]，以便讓 IoT 中樞與裝置應用程式兩者所需的屬性保持同步。</span><span class="sxs-lookup"><span data-stu-id="abb7c-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="abb7c-232">如需詳細資訊，請參閱[裝置對應項開發人員指南][lnk-devguide-twin]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="abb7c-233">回應直接方法</span><span class="sxs-lookup"><span data-stu-id="abb7c-233">Respond to a direct method</span></span>

<span data-ttu-id="abb7c-234">首先，裝置必須訂閱 `$iothub/methods/POST/#`。</span><span class="sxs-lookup"><span data-stu-id="abb7c-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="abb7c-235">IoT 中樞會將方法要求傳送至主題 `$iothub/methods/POST/{method name}/?$rid={request id}`，其中含有有效的 JSON 或空白本文。</span><span class="sxs-lookup"><span data-stu-id="abb7c-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="abb7c-236">為了回應，裝置會將具有有效 JSON 或空白本文的訊息傳送至主題 `$iothub/methods/res/{status}/?$rid={request id}`，其中**要求識別碼**必須和要求訊息中的相符，而**狀態**則必須是整數。</span><span class="sxs-lookup"><span data-stu-id="abb7c-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="abb7c-237">如需詳細資訊，請參閱[直接方法開發人員指南][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="abb7c-238">其他考量</span><span class="sxs-lookup"><span data-stu-id="abb7c-238">Additional considerations</span></span>

<span data-ttu-id="abb7c-239">最後，如果您需要自訂雲端的 MQTT 通訊協定行為，則應該檢閱 [Azure IoT 通訊協定閘道][lnk-azure-protocol-gateway]，這可讓您部署能與「IoT 中樞」直接互動的高效能自訂通訊協定閘道。</span><span class="sxs-lookup"><span data-stu-id="abb7c-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="abb7c-240">Azure IoT 通訊協定閘道器可讓您自訂裝置通訊協定，以順應要重建的 MQTT 部署或其他自訂通訊協定。</span><span class="sxs-lookup"><span data-stu-id="abb7c-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="abb7c-241">不過，這種方法會要求您執行及操作自訂通訊協定閘道。</span><span class="sxs-lookup"><span data-stu-id="abb7c-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abb7c-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abb7c-242">Next steps</span></span>

<span data-ttu-id="abb7c-243">若要深入了解 MQTT 通訊協定，請參閱 [MQTT 文件][lnk-mqtt-docs]。</span><span class="sxs-lookup"><span data-stu-id="abb7c-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="abb7c-244">若要深入了解如何規劃 IoT 中樞部署，請參閱：</span><span class="sxs-lookup"><span data-stu-id="abb7c-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="abb7c-245">[Azure IoT 認證裝置目錄][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="abb7c-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="abb7c-246">[支援其他通訊協定][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="abb7c-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="abb7c-247">[與事件中樞比較][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="abb7c-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="abb7c-248">[縮放、HA 及 DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="abb7c-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="abb7c-249">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="abb7c-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="abb7c-250">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="abb7c-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="abb7c-251">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="abb7c-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
