---
title: "aaaHow toolog 事件 tooAzure Azure API 管理中的事件中心 |Microsoft 文件"
description: "深入了解如何 toolog 事件 tooAzure Azure API 管理中的事件中樞。"
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
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="441cc-103">如何 toolog 事件 tooAzure Azure API 管理中的事件中樞</span><span class="sxs-lookup"><span data-stu-id="441cc-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="441cc-104">Azure 事件中心是可以內嵌包含數百萬個每秒的事件，以便您可以處理及分析 hello 連接的裝置和應用程式所產生的資料量很大的高度可調整的資料輸入服務。</span><span class="sxs-lookup"><span data-stu-id="441cc-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="441cc-105">事件中心做為 hello 「 前端 」 是事件管線，而一旦資料收集到事件中心時，它可以轉換，並儲存使用即時分析的任何提供者或批次處理/儲存體介面卡。</span><span class="sxs-lookup"><span data-stu-id="441cc-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="441cc-106">事件中心，讓事件取用者可以存取自己的排程上的 hello 事件，以減少 hello 生產環境的 hello 耗用量的那些事件的事件資料流。</span><span class="sxs-lookup"><span data-stu-id="441cc-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="441cc-107">本文是附屬 toohello[整合 Azure API 管理事件中心](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/)視訊，並說明如何使用 Azure 事件中心 toolog API 管理事件。</span><span class="sxs-lookup"><span data-stu-id="441cc-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="441cc-108">建立 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="441cc-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="441cc-109">新的事件中樞，登入 toohello toocreate [Azure 傳統入口網站](https://manage.windowsazure.com)按一下**新增**->**應用程式服務**->**服務匯流排** ->**事件中心**->**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="441cc-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="441cc-110">輸入事件中樞名稱、區域，選取訂用帳戶，然後選取命名空間。</span><span class="sxs-lookup"><span data-stu-id="441cc-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="441cc-111">如果先前尚未建立命名空間可以建立一個輸入的名稱在 hello**命名空間**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="441cc-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="441cc-112">一旦設定所有屬性，按一下**建立新的事件中樞**toocreate hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="441cc-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![建立事件中樞][create-event-hub]

<span data-ttu-id="441cc-114">接下來，瀏覽 toohello**設定**新的事件中樞 索引標籤，並建立兩個**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="441cc-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="441cc-115">第一個命名 hello**傳送**並為它提供**傳送**權限。</span><span class="sxs-lookup"><span data-stu-id="441cc-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Sending 原則][sending-policy]

<span data-ttu-id="441cc-117">第二個名稱 hello**接收**，不妨**接聽**權限，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="441cc-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Receiving 原則][receiving-policy]

<span data-ttu-id="441cc-119">每個共用的存取原則可讓應用程式 toosend 和事件 tooand 收到 hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="441cc-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="441cc-120">tooaccess hello 連接字串，這些原則中，瀏覽 toohello**儀表板**hello 事件中樞，然後按一下索引標籤**連接資訊**。</span><span class="sxs-lookup"><span data-stu-id="441cc-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![連接字串][event-hub-dashboard]

<span data-ttu-id="441cc-122">hello**傳送**登入事件時，會使用連接字串和 hello**接收**從 hello 事件中心下載事件時，會使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="441cc-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![連接字串][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="441cc-124">建立 API 管理記錄器</span><span class="sxs-lookup"><span data-stu-id="441cc-124">Create an API Management logger</span></span>
<span data-ttu-id="441cc-125">現在您有事件中心，hello 下一個步驟是 tooconfigure[記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity)在 API 管理服務，讓它可以記錄事件 toohello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="441cc-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="441cc-126">API 管理記錄器已設定使用 hello [API 管理 REST API](http://aka.ms/smapi)。</span><span class="sxs-lookup"><span data-stu-id="441cc-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="441cc-127">使用 REST API hello hello 的第一次之前, 檢閱 hello[必要條件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites)並確定您有[啟用存取 toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI)。</span><span class="sxs-lookup"><span data-stu-id="441cc-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="441cc-128">toocreate 記錄器，請使用下列 URL 範本 hello HTTP PUT 要求。</span><span class="sxs-lookup"><span data-stu-id="441cc-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="441cc-129">取代`{your service}`hello 您 API 管理服務執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="441cc-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="441cc-130">取代`{new logger name}`與 hello 需要新的記錄器的名稱。</span><span class="sxs-lookup"><span data-stu-id="441cc-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="441cc-131">您將會參考此名稱，當您設定 hello[記錄-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)原則</span><span class="sxs-lookup"><span data-stu-id="441cc-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="441cc-132">新增下列標頭 toohello 要求 hello。</span><span class="sxs-lookup"><span data-stu-id="441cc-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="441cc-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="441cc-133">Content-Type : application/json</span></span>
* <span data-ttu-id="441cc-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="441cc-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="441cc-135">如需有關產生 hello 指示`SharedAccessSignature`看到[Azure API 管理 REST API 驗證](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication)。</span><span class="sxs-lookup"><span data-stu-id="441cc-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="441cc-136">指定使用下列範本的 hello hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="441cc-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="441cc-137">`type`必須設定得`AzureEventHub`。</span><span class="sxs-lookup"><span data-stu-id="441cc-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="441cc-138">`description`提供 hello 記錄器的選擇性描述，並視需要，可以是零長度字串。</span><span class="sxs-lookup"><span data-stu-id="441cc-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="441cc-139">`credentials`包含 hello`name`和`connectionString`的 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="441cc-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="441cc-140">當您建立 hello 要求如果 hello 記錄器建立狀態碼`201 Created`傳回。</span><span class="sxs-lookup"><span data-stu-id="441cc-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="441cc-141">如需其他可能的傳回碼和其原因，請參閱 [建立記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT)。</span><span class="sxs-lookup"><span data-stu-id="441cc-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="441cc-142">toosee 如何執行其他作業，例如清單、 更新和刪除，請參閱 hello[記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity)實體文件。</span><span class="sxs-lookup"><span data-stu-id="441cc-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="441cc-143">設定 log-to-eventhubs 原則</span><span class="sxs-lookup"><span data-stu-id="441cc-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="441cc-144">一旦您記錄器設定 API 管理中，您可以設定您的記錄檔-eventhubs 原則 toolog hello 預期事件。</span><span class="sxs-lookup"><span data-stu-id="441cc-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="441cc-145">hello 記錄-eventhubs 原則可用於任一 hello 輸入的原則區段或 hello 輸出原則 > 一節。</span><span class="sxs-lookup"><span data-stu-id="441cc-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="441cc-146">tooconfigure 原則，登入 toohello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour API 管理服務，然後按一下**發行者入口網站**tooaccess hello 發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="441cc-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![發行者入口網站][publisher-portal]

<span data-ttu-id="441cc-148">按一下**原則**在 hello 左側 hello API 管理功能表上，選取 hello 所需的產品和 API，然後按一下**新增原則**。</span><span class="sxs-lookup"><span data-stu-id="441cc-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="441cc-149">在此範例中所新增的原則 toohello **Echo API**在 hello **Unlimited**產品。</span><span class="sxs-lookup"><span data-stu-id="441cc-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="441cc-151">將游標置於 hello`inbound`原則區段，然後按一下 hello**記錄 tooEventHub**原則 tooinsert hello`log-to-eventhub`原則陳述式的範本。</span><span class="sxs-lookup"><span data-stu-id="441cc-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="441cc-153">取代`logger-id`hello hello 先前步驟中設定的 hello API 管理記錄器名稱。</span><span class="sxs-lookup"><span data-stu-id="441cc-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="441cc-154">您可以使用任何運算式會傳回字串 hello 的 hello 值`log-to-eventhub`項目。</span><span class="sxs-lookup"><span data-stu-id="441cc-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="441cc-155">在此範例中會記錄包含 hello 日期和時間、 服務名稱、 要求識別碼、 要求的 ip 位址和作業名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="441cc-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="441cc-156">按一下**儲存**toosave hello 更新原則設定。</span><span class="sxs-lookup"><span data-stu-id="441cc-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="441cc-157">它會儲存為 hello 原則是作用中和事件會記錄的 toohello 指定事件中心。</span><span class="sxs-lookup"><span data-stu-id="441cc-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="441cc-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="441cc-158">Next steps</span></span>
* <span data-ttu-id="441cc-159">深入了解 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="441cc-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="441cc-160">開始使用 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="441cc-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="441cc-161">使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="441cc-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="441cc-162">事件中樞程式設計指南</span><span class="sxs-lookup"><span data-stu-id="441cc-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="441cc-163">深入了解 API 管理和事件中樞的整合</span><span class="sxs-lookup"><span data-stu-id="441cc-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="441cc-164">記錄器實體參考</span><span class="sxs-lookup"><span data-stu-id="441cc-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="441cc-165">log-to-eventhub 原則參考</span><span class="sxs-lookup"><span data-stu-id="441cc-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="441cc-166">利用 Azure API 管理、事件中樞及 Runscope 監視您的 API</span><span class="sxs-lookup"><span data-stu-id="441cc-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="441cc-167">觀看影片逐步解說</span><span class="sxs-lookup"><span data-stu-id="441cc-167">Watch a video walkthrough</span></span>
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
