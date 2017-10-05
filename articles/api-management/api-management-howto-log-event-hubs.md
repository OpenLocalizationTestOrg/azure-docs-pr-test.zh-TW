---
title: "如何將事件記錄到 Azure API 管理中的 Azure 事件中樞 | Microsoft Docs"
description: "了解如何將事件記錄到 Azure API 管理中的 Azure 事件中樞。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="a153d-103">如何將事件記錄到 Azure API 管理中的 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="a153d-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="a153d-104">事件中樞是可高度調整的資料輸入服務，每秒可擷取數百萬個事件，可讓您處理和分析連接的裝置和應用程式所產生的大量資料。</span><span class="sxs-lookup"><span data-stu-id="a153d-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a153d-105">事件中樞能做為事件管線的「大門」，一旦收集的資料進入事件中樞，它可以使用任何即時分析提供者或批次/儲存配接器轉換及儲存資料。</span><span class="sxs-lookup"><span data-stu-id="a153d-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="a153d-106">事件中樞能分隔事件串流的生產與這些事件的使用，讓事件消費者依照自己的排程存取事件。</span><span class="sxs-lookup"><span data-stu-id="a153d-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="a153d-107">這篇文章附隨於 [整合 Azure API 管理與事件中樞](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) 視訊並說明如何使用 Azure 事件中樞記錄 API 管理事件。</span><span class="sxs-lookup"><span data-stu-id="a153d-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="a153d-108">建立 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="a153d-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="a153d-109">若要建立新的事件中樞，請登入 [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 [新增] -> [應用程式服務] -> [服務匯流排] -> [事件中樞] -> [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="a153d-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="a153d-110">輸入事件中樞名稱、區域，選取訂用帳戶，然後選取命名空間。</span><span class="sxs-lookup"><span data-stu-id="a153d-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="a153d-111">如果您先前尚未建立命名空間，可以在 [命名空間]  文字方塊中輸入名稱加以建立。</span><span class="sxs-lookup"><span data-stu-id="a153d-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="a153d-112">設定好所有屬性後，按一下 [建立新的事件中樞]  建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a153d-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![建立事件中樞][create-event-hub]

<span data-ttu-id="a153d-114">接下來，瀏覽至新事件中樞的 [設定] 索引標籤，建立兩個**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="a153d-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="a153d-115">將第一個原則命名為 **Sending**，並授與 [傳送] 權限。</span><span class="sxs-lookup"><span data-stu-id="a153d-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Sending 原則][sending-policy]

<span data-ttu-id="a153d-117">將第二個原則命名為 **Receiving**，並授與 [接聽] 權限，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a153d-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Receiving 原則][receiving-policy]

<span data-ttu-id="a153d-119">每個共用存取原則都可讓應用程式傳送事件至事件中樞和接收來自事件中樞的事件。</span><span class="sxs-lookup"><span data-stu-id="a153d-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="a153d-120">若要存取這些原則的連接字串，請瀏覽至事件中樞的 [儀表板] 索引標籤，然後按一下 [連接資訊]。</span><span class="sxs-lookup"><span data-stu-id="a153d-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Connection string][event-hub-dashboard]

<span data-ttu-id="a153d-122">**Sending** 連接字串用於記錄事件，**Receiving** 連接字串則用於從事件中樞下載事件時。</span><span class="sxs-lookup"><span data-stu-id="a153d-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Connection string][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="a153d-124">建立 API 管理記錄器</span><span class="sxs-lookup"><span data-stu-id="a153d-124">Create an API Management logger</span></span>
<span data-ttu-id="a153d-125">現在您已經有事件中樞，下一步是在 API 管理服務中設定 [記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) ，以將事件記錄至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a153d-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="a153d-126">可使用 [API 管理 REST API](http://aka.ms/smapi)來設定 API 管理記錄器。</span><span class="sxs-lookup"><span data-stu-id="a153d-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="a153d-127">在第一次使用 REST API 之前，請先檢閱[必要條件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites)，確定您已[啟用 REST API 的存取](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI)。</span><span class="sxs-lookup"><span data-stu-id="a153d-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="a153d-128">若要建立記錄器，請使用下列 URL 範本提出 HTTP PUT 要求。</span><span class="sxs-lookup"><span data-stu-id="a153d-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="a153d-129">以 API 管理服務執行個體的名稱取代 `{your service}` 。</span><span class="sxs-lookup"><span data-stu-id="a153d-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="a153d-130">以您想要的新記錄器名稱取代 `{new logger name}` 。</span><span class="sxs-lookup"><span data-stu-id="a153d-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="a153d-131">當您設定 [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) 原則時，將會參考此名稱。</span><span class="sxs-lookup"><span data-stu-id="a153d-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="a153d-132">將下列標頭加到要求中。</span><span class="sxs-lookup"><span data-stu-id="a153d-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="a153d-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="a153d-133">Content-Type : application/json</span></span>
* <span data-ttu-id="a153d-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="a153d-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="a153d-135">如需產生 `SharedAccessSignature` 的相關指示，請參閱 [Azure API 管理 REST API 驗證](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication)。</span><span class="sxs-lookup"><span data-stu-id="a153d-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="a153d-136">使用下列範本指定要求本文。</span><span class="sxs-lookup"><span data-stu-id="a153d-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="a153d-137">`type` 必須設為 `AzureEventHub`。</span><span class="sxs-lookup"><span data-stu-id="a153d-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="a153d-138">`description` 提供記錄器的選擇性描述，如有需要，可以是零長度字串。</span><span class="sxs-lookup"><span data-stu-id="a153d-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="a153d-139">`credentials` 包含 Azure 事件中樞的 `name` 和 `connectionString`。</span><span class="sxs-lookup"><span data-stu-id="a153d-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="a153d-140">當您提出要求時，如果記錄器已建立，會傳回狀態碼 `201 Created` 。</span><span class="sxs-lookup"><span data-stu-id="a153d-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="a153d-141">如需其他可能的傳回碼和其原因，請參閱 [建立記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT)。</span><span class="sxs-lookup"><span data-stu-id="a153d-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="a153d-142">若要查看如何執行其他作業，例如列出、更新和刪除，請參閱 [記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) 實體文件。</span><span class="sxs-lookup"><span data-stu-id="a153d-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="a153d-143">設定 log-to-eventhubs 原則</span><span class="sxs-lookup"><span data-stu-id="a153d-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="a153d-144">您在 API 管理中設定好記錄器後，便可設定 log-to-eventhubs 原則來記錄所需的事件。</span><span class="sxs-lookup"><span data-stu-id="a153d-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="a153d-145">log-to-eventhubs 原則可用於輸入原則區段或輸出原則區段。</span><span class="sxs-lookup"><span data-stu-id="a153d-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="a153d-146">若要設定原則，請登入 [Azure 入口網站](https://portal.azure.com)，瀏覽至您的「API 管理」服務，然後按一下 [發行者入口網站] 以存取發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="a153d-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![發行者入口網站][publisher-portal]

<span data-ttu-id="a153d-148">按一下左側 [API 管理] 功能表中的 [原則]，選取所需產品和 API，然後按一下 [新增原則]。</span><span class="sxs-lookup"><span data-stu-id="a153d-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="a153d-149">在此範例中，我們將原則新增至 [無限制] 產品中的 [Echo API]。</span><span class="sxs-lookup"><span data-stu-id="a153d-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="a153d-151">請將游標放置在 `inbound` 原則區段中，按一下 [Log to EventHub] 原則，插入 `log-to-eventhub` 原則陳述式範本。</span><span class="sxs-lookup"><span data-stu-id="a153d-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="a153d-153">以您在上一個步驟中所設定的 API 管理記錄器名稱取代 `logger-id` 。</span><span class="sxs-lookup"><span data-stu-id="a153d-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="a153d-154">您可以使用任何能傳回字串做為 `log-to-eventhub` 項目之值的運算式。</span><span class="sxs-lookup"><span data-stu-id="a153d-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="a153d-155">在此範例中，將記錄包含日期和時間、服務名稱、要求 ID、 要求的 IP 位址和作業名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="a153d-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="a153d-156">按一下 [儲存]  ，儲存更新的原則組態。</span><span class="sxs-lookup"><span data-stu-id="a153d-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="a153d-157">儲存完成後，原則便會啟用，事件會記錄至指定的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a153d-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a153d-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a153d-158">Next steps</span></span>
* <span data-ttu-id="a153d-159">深入了解 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="a153d-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="a153d-160">開始使用 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="a153d-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="a153d-161">使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="a153d-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="a153d-162">事件中樞程式設計指南</span><span class="sxs-lookup"><span data-stu-id="a153d-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="a153d-163">深入了解 API 管理和事件中樞的整合</span><span class="sxs-lookup"><span data-stu-id="a153d-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="a153d-164">記錄器實體參考</span><span class="sxs-lookup"><span data-stu-id="a153d-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="a153d-165">log-to-eventhub 原則參考</span><span class="sxs-lookup"><span data-stu-id="a153d-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="a153d-166">利用 Azure API 管理、事件中樞及 Runscope 監視您的 API</span><span class="sxs-lookup"><span data-stu-id="a153d-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="a153d-167">觀看影片逐步解說</span><span class="sxs-lookup"><span data-stu-id="a153d-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
