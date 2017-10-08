---
title: "aaaUnderstand hello Azure IoT 中樞內建端點 |Microsoft 文件"
description: "開發人員指南-描述 toouse hello 內建的事件中樞相容端點 toread 裝置到雲端訊息的方式。"
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="54a9f-103">讀取 hello 內建端點的裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="54a9f-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="54a9f-104">根據預設，訊息會路由的 toohello 內建的服務對向端點 (**事件訊息/**)，也就是與相容[事件中心][lnk-event-hubs]。</span><span class="sxs-lookup"><span data-stu-id="54a9f-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="54a9f-105">這個端點是目前只使用 hello 公開[AMQP] [ lnk-amqp]通訊協定連接埠 5671。</span><span class="sxs-lookup"><span data-stu-id="54a9f-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="54a9f-106">IoT 中樞公開 hello 下列屬性 tooenable 您 toocontrol hello 內建事件中樞相容傳訊端點**事件訊息/**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="54a9f-107">屬性</span><span class="sxs-lookup"><span data-stu-id="54a9f-107">Property</span></span>            | <span data-ttu-id="54a9f-108">說明</span><span class="sxs-lookup"><span data-stu-id="54a9f-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="54a9f-109">**分割計數**</span><span class="sxs-lookup"><span data-stu-id="54a9f-109">**Partition count**</span></span> | <span data-ttu-id="54a9f-110">設定這個屬性在建立 toodefine hello 的[分割][ lnk-event-hub-partitions]裝置到雲端事件擷取。</span><span class="sxs-lookup"><span data-stu-id="54a9f-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="54a9f-111">**保留時間**</span><span class="sxs-lookup"><span data-stu-id="54a9f-111">**Retention time**</span></span>  | <span data-ttu-id="54a9f-112">此屬性可指定 IoT 中樞保留訊息的天數。</span><span class="sxs-lookup"><span data-stu-id="54a9f-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="54a9f-113">hello 預設值為一天，但它可能需要增加的 tooseven 天。</span><span class="sxs-lookup"><span data-stu-id="54a9f-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="54a9f-114">IoT 中樞也可讓您 toomanage hello 內建裝置到雲端的取用者群組接收端點。</span><span class="sxs-lookup"><span data-stu-id="54a9f-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="54a9f-115">根據預設，明確地不符合訊息的路由規則的所有訊息都會都寫入 toohello 內建端點。</span><span class="sxs-lookup"><span data-stu-id="54a9f-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="54a9f-116">如果您停用此後援路由，則會捨棄未明確符合任何訊息路由規則的訊息。</span><span class="sxs-lookup"><span data-stu-id="54a9f-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="54a9f-117">您可以修改 hello 保留時間，以程式設計方式透過 hello [IoT 中樞資源提供者 REST Api][lnk-resource-provider-apis]，或使用 hello [Azure 入口網站][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="54a9f-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="54a9f-118">IoT 中樞公開 hello**事件訊息/**內建端點的後端服務接收的網路集線器 tooread hello 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="54a9f-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="54a9f-119">這個端點是事件中樞相容，可讓您 toouse hello 機制 hello 事件中心服務的任何讀取訊息的支援。</span><span class="sxs-lookup"><span data-stu-id="54a9f-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="54a9f-120">讀取 hello 內建端點</span><span class="sxs-lookup"><span data-stu-id="54a9f-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="54a9f-121">當您使用 hello[適用於.NET 的 Azure 服務匯流排 SDK] [ lnk-servicebus-sdk]或 hello[事件中心的事件處理器主機][lnk-eventprocessorhost]，您可以使用任何 IoT 中樞連接字串與 hello 正確的權限。</span><span class="sxs-lookup"><span data-stu-id="54a9f-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="54a9f-122">然後使用**事件訊息/**做為 hello 事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="54a9f-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="54a9f-123">當您使用 Sdk （或產品整合） 不會察覺 IoT 中樞，您必須從 hello IoT 中樞設定中 hello 擷取的事件中樞相容端點及事件中樞相容名稱[Azure 入口網站][ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="54a9f-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="54a9f-124">在 hello IoT 中樞刀鋒視窗中，按一下 **端點**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="54a9f-125">在 hello**內建端點**區段中，按一下**事件**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="54a9f-126">hello 刀鋒視窗包含下列值的 hello:**事件中樞相容端點**，**事件中樞相容名稱**，**分割**，**保留時間**，和**取用者群組**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![裝置到雲端設定][img-eventhubcompatible]

<span data-ttu-id="54a9f-128">hello IoT 中樞 SDK 需要 hello IoT 中樞端點名稱，亦即**事件訊息/** hello 中所示**端點**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="54a9f-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="54a9f-129">如果您使用的 SDK hello 需要**Hostname**或**命名空間**值，請移除 hello hello 配置**事件中樞相容端點**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="54a9f-130">例如，如果您的事件中樞相容端點**sb://iothub-ns-myiothub-1234.servicebus.windows.net/**，hello **Hostname**會**iot 中樞 ns-myiothub 1234.servicebus.windows.net**，和 hello**命名空間**會**iot 中樞-ns-myiothub-1234年**。</span><span class="sxs-lookup"><span data-stu-id="54a9f-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="54a9f-131">然後，您可以使用任何具有 hello 的共用的存取原則**ServiceConnect**權限 tooconnect toohello 指定事件中心。</span><span class="sxs-lookup"><span data-stu-id="54a9f-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="54a9f-132">如果您需要 toobuild 事件中樞連接字串使用 hello 先前的資訊，請使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="54a9f-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="54a9f-133">hello Sdk 和整合可讓您與 IoT 中樞會公開的事件中樞相容端點還包含下列清單中的 hello hello 項目：</span><span class="sxs-lookup"><span data-stu-id="54a9f-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="54a9f-134">[Java 事件中樞用戶端](https://github.com/hdinsight/eventhubs-client)。</span><span class="sxs-lookup"><span data-stu-id="54a9f-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="54a9f-135">[Apache Storm Spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="54a9f-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="54a9f-136">您可以檢視 hello [spout 來源](https://github.com/apache/storm/tree/master/external/storm-eventhubs)GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="54a9f-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="54a9f-137">[Apache Spark 整合](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)。</span><span class="sxs-lookup"><span data-stu-id="54a9f-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54a9f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54a9f-138">Next steps</span></span>

<span data-ttu-id="54a9f-139">如需 IoT 中樞端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="54a9f-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="54a9f-140">hello[開始][ lnk-get-started]教學課程示範如何從 toosend 裝置到雲端訊息模擬裝置及讀取 hello 內建端點的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="54a9f-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="54a9f-141">如需詳細資訊，請參閱 hello[使用路由的處理序 IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="54a9f-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="54a9f-142">如果您想 tooroute 您裝置到雲端訊息 toocustom 端點，請參閱[用於裝置到雲端訊息的訊息路由和自訂端點][lnk-custom]。</span><span class="sxs-lookup"><span data-stu-id="54a9f-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
