---
title: "了解 Azure IoT 中樞內建端點 | Microsoft Docs"
description: "開發人員指南 - 說明如何將內建且與事件中樞相容的端點用於讀取裝置到雲端訊息。"
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="86629-103">從內建端點讀取裝置對雲端訊息</span><span class="sxs-lookup"><span data-stu-id="86629-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="86629-104">根據預設，系統會將訊息路由至內建的服務面向端點 (**messages/events**)，此端點與[事件中樞][lnk-event-hubs]相容。</span><span class="sxs-lookup"><span data-stu-id="86629-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="86629-105">此端點目前只公開使用連接埠 5671 上的 [AMQP][lnk-amqp] 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="86629-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="86629-106">IoT 中樞會公開下列屬性，讓您控制與事件中樞相容的內建訊息端點 **messages/events**。</span><span class="sxs-lookup"><span data-stu-id="86629-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="86629-107">屬性</span><span class="sxs-lookup"><span data-stu-id="86629-107">Property</span></span>            | <span data-ttu-id="86629-108">說明</span><span class="sxs-lookup"><span data-stu-id="86629-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="86629-109">**分割計數**</span><span class="sxs-lookup"><span data-stu-id="86629-109">**Partition count**</span></span> | <span data-ttu-id="86629-110">在建立時設定此屬性，以定義裝置對雲端事件擷取的[資料分割][lnk-event-hub-partitions]數目。</span><span class="sxs-lookup"><span data-stu-id="86629-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="86629-111">**保留時間**</span><span class="sxs-lookup"><span data-stu-id="86629-111">**Retention time**</span></span>  | <span data-ttu-id="86629-112">此屬性可指定 IoT 中樞保留訊息的天數。</span><span class="sxs-lookup"><span data-stu-id="86629-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="86629-113">預設值是一天，但它可以增加到七天。</span><span class="sxs-lookup"><span data-stu-id="86629-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="86629-114">IoT 中樞也可讓您管理內建裝置對雲端接收端點上的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="86629-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="86629-115">根據預設，所有未明確符合訊息路由規則的訊息，均會寫入至內建端點。</span><span class="sxs-lookup"><span data-stu-id="86629-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="86629-116">如果您停用此後援路由，則會捨棄未明確符合任何訊息路由規則的訊息。</span><span class="sxs-lookup"><span data-stu-id="86629-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="86629-117">您可以透過 [IoT 中樞資源提供者 REST API][lnk-resource-provider-apis] 以程式設計方式來修改保留時間，或使用 [Azure 入口網站][lnk-management-portal]來修改。</span><span class="sxs-lookup"><span data-stu-id="86629-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="86629-118">IoT 中樞會公開您後端服務的 **messages/events** 內建端點，以讀取您的中樞收到的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="86629-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="86629-119">此端點與事件中樞相容，可讓您使用事件中樞服務支援的任何機制讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="86629-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="86629-120">從內建端點讀取</span><span class="sxs-lookup"><span data-stu-id="86629-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="86629-121">使用[適用於 .NET 的 Azure 服務匯流排 SDK][lnk-servicebus-sdk] 或[事件中樞 - 事件處理器主機][lnk-eventprocessorhost]時，您可以使用任何 IoT 中樞連接字串搭配正確的權限。</span><span class="sxs-lookup"><span data-stu-id="86629-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="86629-122">然後使用 **messages/events** 做為事件中樞名稱</span><span class="sxs-lookup"><span data-stu-id="86629-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="86629-123">當您使用未能察覺 IoT 中樞的 SDK (或產品整合) 時，必須從 [Azure 入口網站][lnk-management-portal]的 IoT 中樞設定中，擷取事件中樞相容端點和事件中樞相容名稱︰</span><span class="sxs-lookup"><span data-stu-id="86629-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="86629-124">在 IoT 中樞刀鋒視窗中，按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="86629-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="86629-125">在 [內建端點] 區段中，按一下 [事件]。</span><span class="sxs-lookup"><span data-stu-id="86629-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="86629-126">刀鋒視窗包含下列值：[事件中樞相容端點]、[事件中樞相容名稱]、[資料分割]、[保留時間] 和 [取用者群組]。</span><span class="sxs-lookup"><span data-stu-id="86629-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![裝置到雲端設定][img-eventhubcompatible]

<span data-ttu-id="86629-128">IoT 中樞 SDK 需要 IoT 中樞端點名稱，也就是 [端點] 刀鋒視窗中顯示的 **messages/events**。</span><span class="sxs-lookup"><span data-stu-id="86629-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="86629-129">如果您正在使用的 SDK 需要**主機名稱**或**命名空間**值，請從 [事件中樞相容端點] 中移除配置。</span><span class="sxs-lookup"><span data-stu-id="86629-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="86629-130">例如，如果您的事件中樞相容端點為 **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**，**主機名稱**會是 **iothub-ns-myiothub-1234.servicebus.windows.net**，而**命名空間**會是 **iothub-ns-myiothub-1234**。</span><span class="sxs-lookup"><span data-stu-id="86629-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="86629-131">然後，您可以使用具有 **ServiceConnect** 權限的任何共用存取原則，連接至指定的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="86629-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="86629-132">如果您需要使用先前資訊來建置事件中樞連接字串，請使用下列模式：</span><span class="sxs-lookup"><span data-stu-id="86629-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="86629-133">您可以搭配 IoT 中樞公開之事件中樞相容端點使用的 SDK 和整合項目包含下列清單中的項目：</span><span class="sxs-lookup"><span data-stu-id="86629-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="86629-134">[Java 事件中樞用戶端](https://github.com/hdinsight/eventhubs-client)。</span><span class="sxs-lookup"><span data-stu-id="86629-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="86629-135">[Apache Storm Spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="86629-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="86629-136">您可以檢視 GitHub 上的 [Spout 原始檔](https://github.com/apache/storm/tree/master/external/storm-eventhubs) 。</span><span class="sxs-lookup"><span data-stu-id="86629-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="86629-137">[Apache Spark 整合](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)。</span><span class="sxs-lookup"><span data-stu-id="86629-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86629-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86629-138">Next steps</span></span>

<span data-ttu-id="86629-139">如需有關 IoT 中樞端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="86629-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="86629-140">[開始使用][lnk-get-started]教學課程會示範如何從模擬裝置傳送裝置到雲端訊息和從內建端點讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="86629-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="86629-141">如需詳細資訊，請參閱[使用路由處理 IoT 中樞裝置到雲端訊息][lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="86629-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="86629-142">如果您想要將裝置到雲端訊息路由至自訂端點，請參閱[針對裝置到雲端訊息使用訊息路由和自訂端點][lnk-custom]。</span><span class="sxs-lookup"><span data-stu-id="86629-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
