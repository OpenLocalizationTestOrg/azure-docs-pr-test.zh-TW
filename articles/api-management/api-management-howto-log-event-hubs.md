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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>如何 toolog 事件 tooAzure Azure API 管理中的事件中樞
Azure 事件中心是可以內嵌包含數百萬個每秒的事件，以便您可以處理及分析 hello 連接的裝置和應用程式所產生的資料量很大的高度可調整的資料輸入服務。 事件中心做為 hello 「 前端 」 是事件管線，而一旦資料收集到事件中心時，它可以轉換，並儲存使用即時分析的任何提供者或批次處理/儲存體介面卡。 事件中心，讓事件取用者可以存取自己的排程上的 hello 事件，以減少 hello 生產環境的 hello 耗用量的那些事件的事件資料流。

本文是附屬 toohello[整合 Azure API 管理事件中心](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/)視訊，並說明如何使用 Azure 事件中心 toolog API 管理事件。

## <a name="create-an-azure-event-hub"></a>建立 Azure 事件中樞
新的事件中樞，登入 toohello toocreate [Azure 傳統入口網站](https://manage.windowsazure.com)按一下**新增**->**應用程式服務**->**服務匯流排** ->**事件中心**->**快速建立**。 輸入事件中樞名稱、區域，選取訂用帳戶，然後選取命名空間。 如果先前尚未建立命名空間可以建立一個輸入的名稱在 hello**命名空間**文字方塊。 一旦設定所有屬性，按一下**建立新的事件中樞**toocreate hello 事件中心。

![建立事件中樞][create-event-hub]

接下來，瀏覽 toohello**設定**新的事件中樞 索引標籤，並建立兩個**共用存取原則**。 第一個命名 hello**傳送**並為它提供**傳送**權限。

![Sending 原則][sending-policy]

第二個名稱 hello**接收**，不妨**接聽**權限，然後按一下**儲存**。

![Receiving 原則][receiving-policy]

每個共用的存取原則可讓應用程式 toosend 和事件 tooand 收到 hello 事件中心。 tooaccess hello 連接字串，這些原則中，瀏覽 toohello**儀表板**hello 事件中樞，然後按一下索引標籤**連接資訊**。

![連接字串][event-hub-dashboard]

hello**傳送**登入事件時，會使用連接字串和 hello**接收**從 hello 事件中心下載事件時，會使用連接字串。

![連接字串][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>建立 API 管理記錄器
現在您有事件中心，hello 下一個步驟是 tooconfigure[記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity)在 API 管理服務，讓它可以記錄事件 toohello 事件中心。

API 管理記錄器已設定使用 hello [API 管理 REST API](http://aka.ms/smapi)。 使用 REST API hello hello 的第一次之前, 檢閱 hello[必要條件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites)並確定您有[啟用存取 toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI)。

toocreate 記錄器，請使用下列 URL 範本 hello HTTP PUT 要求。

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* 取代`{your service}`hello 您 API 管理服務執行個體名稱。
* 取代`{new logger name}`與 hello 需要新的記錄器的名稱。 您將會參考此名稱，當您設定 hello[記錄-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)原則

新增下列標頭 toohello 要求 hello。

* Content-Type : application/json
* Authorization : SharedAccessSignature 58...
  * 如需有關產生 hello 指示`SharedAccessSignature`看到[Azure API 管理 REST API 驗證](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication)。

指定使用下列範本的 hello hello 要求主體。

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

* `type`必須設定得`AzureEventHub`。
* `description`提供 hello 記錄器的選擇性描述，並視需要，可以是零長度字串。
* `credentials`包含 hello`name`和`connectionString`的 Azure 事件中樞。

當您建立 hello 要求如果 hello 記錄器建立狀態碼`201 Created`傳回。

> [!NOTE]
> 如需其他可能的傳回碼和其原因，請參閱 [建立記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT)。 toosee 如何執行其他作業，例如清單、 更新和刪除，請參閱 hello[記錄器](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity)實體文件。
>
>

## <a name="configure-log-to-eventhubs-policies"></a>設定 log-to-eventhubs 原則
一旦您記錄器設定 API 管理中，您可以設定您的記錄檔-eventhubs 原則 toolog hello 預期事件。 hello 記錄-eventhubs 原則可用於任一 hello 輸入的原則區段或 hello 輸出原則 > 一節。

tooconfigure 原則，登入 toohello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour API 管理服務，然後按一下**發行者入口網站**tooaccess hello 發行者入口網站。

![發行者入口網站][publisher-portal]

按一下**原則**在 hello 左側 hello API 管理功能表上，選取 hello 所需的產品和 API，然後按一下**新增原則**。 在此範例中所新增的原則 toohello **Echo API**在 hello **Unlimited**產品。

![Add policy][add-policy]

將游標置於 hello`inbound`原則區段，然後按一下 hello**記錄 tooEventHub**原則 tooinsert hello`log-to-eventhub`原則陳述式的範本。

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

取代`logger-id`hello hello 先前步驟中設定的 hello API 管理記錄器名稱。

您可以使用任何運算式會傳回字串 hello 的 hello 值`log-to-eventhub`項目。 在此範例中會記錄包含 hello 日期和時間、 服務名稱、 要求識別碼、 要求的 ip 位址和作業名稱的字串。

按一下**儲存**toosave hello 更新原則設定。 它會儲存為 hello 原則是作用中和事件會記錄的 toohello 指定事件中心。

## <a name="next-steps"></a>後續步驟
* 深入了解 Azure 事件中樞
  * [開始使用 Azure 事件中樞](../event-hubs/event-hubs-c-getstarted-send.md)
  * [使用 EventProcessorHost 接收訊息](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [事件中樞程式設計指南](../event-hubs/event-hubs-programming-guide.md)
* 深入了解 API 管理和事件中樞的整合
  * [記錄器實體參考](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [log-to-eventhub 原則參考](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [利用 Azure API 管理、事件中樞及 Runscope 監視您的 API](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>觀看影片逐步解說
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
