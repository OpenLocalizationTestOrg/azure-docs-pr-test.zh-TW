---
title: "Azure API 管理、 事件中樞與 Runscope Api aaaMonitor |Microsoft 文件"
description: "示範連接的 Azure API 管理、 Azure 事件中樞與 http 記錄與監控 Runscope hello 記錄到事件中樞原則的範例應用程式"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>利用 Azure API 管理、事件中樞及 Runscope 監視您的 API
hello [API 管理服務](api-management-key-concepts.md)提供許多功能 tooenhance hello 處理 HTTP 要求傳送 tooyour HTTP API。 不過，hello 存在的 hello 要求和回應是暫時性。 hello 要求，其流經 hello API 管理服務 tooyour 後端應用程式開發介面。 您的 API 處理 hello 要求和回應回流經 toohello API 取用者。 hello API 管理服務可供顯示 hello 應用程式開發介面的相關的一些重要統計資料 hello 發行者入口網站儀表板中，但除此之外、 hello 詳細資料都已消失。

使用 hello[記錄-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [原則](api-management-howto-policies.md)hello API 管理服務中您可以傳送任何詳細資料，從 hello 要求和回應 tooan [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)。 有各種為什麼您可能想要 toogenerate 來自傳送 tooyour Api HTTP 訊息的原因。 範例包括更新稽核線索、使用量分析、例外狀況警示和協力廠商整合。   

本文示範如何 toocapture hello 整個 HTTP 要求和回應訊息，傳送 tooan 事件中心資料，然後轉送該訊息 tooa 協力廠商服務提供 HTTP 記錄和監視 windows 服務。

## <a name="why-send-from-api-management-service"></a>為什麼要從 API 管理服務傳送？
很可能 toowrite HTTP 中介軟體，可以插入 HTTP API 架構 toocapture HTTP 要求和回應和送入記錄和監視系統。 hello 缺點 toothis 方法是 hello HTTP 中介軟體需要 toobe 整合至 hello 後端應用程式開發介面，而且必須符合 hello API hello 平台。 如果有多個 Api 每個必須部署 hello 中介軟體。 後端 API 無法升級通常有一些原因。

Hello Azure API 管理服務 toointegrate 使用記錄基礎結構提供集中式且平台無關的解決方案。 它也是可擴充的因為部分 toohello[地理複寫](api-management-howto-deploy-multi-region.md)Azure API 管理的功能。

## <a name="why-send-tooan-azure-event-hub"></a>為什麼要傳送 tooan Azure 事件中心？
它是合理的 tooask，為什麼要建立特定 tooAzure 事件中心的原則嗎？ 有許多不同的地方，我想要 toolog 我的要求。 為什麼不只傳送 hello 直接要求 toohello 最終目的地？  這是一個選項。 不過，當進行記錄要求從 API 管理服務，它會需要 tooconsider 記錄訊息會如何影響 hello API hello 效能。 增加系統元件的可用執行個體或利用異地複寫功能，可以處理逐漸增加的負載。 不過，簡短的流量尖峰，可能會造成要求 toobe 大幅延遲如果要求 toologging 基礎結構啟動 tooslow 負載。

hello Azure 事件中心設計的 tooingress 龐大資料磁碟區，與容量，以處理遠編號的事件高於 hello 數目的 HTTP 要求大部分的應用程式開發介面處理程序。 事件中心 hello 做為一種您 API 管理服務和 hello 基礎結構將會儲存及處理 hello 訊息之間有複雜的緩衝區。 這可確保不會因為 toohello 記錄基礎結構降低您的應用程式開發介面效能。  

一旦 hello 資料已傳送 tooan 事件中心，它會持續保留，並將等候事件中樞取用者 tooprocess 它。 事件中心 hello 不在意如何處理，它只重視並確定將會成功傳送 hello 訊息。     

事件中心有 hello 能力 toostream 事件 toomultiple 取用者群組。 這可讓事件 toobe 完全不同的系統所處理。 這可讓支援不需將加入延遲放在只有一個事件需求產生 toobe hello 處理 hello API 管理服務中的 hello API 要求的許多整合案例。

## <a name="a-policy-toosend-applicationhttp-messages"></a>原則 toosend http 應用程式/訊息
事件中樞接受簡單字串形式的事件資料。 該字串 hello 內容都已完全啟動 tooyou。 toobe 無法 toopackage HTTP 要求和傳送關閉 tooEvent 集線器我們需要 tooformat hello 字串 hello 要求或回應資訊。 在這種情況下，如果沒有現有的格式，我們可以重複使用，然後我們可能不需要 toowrite 自己剖析的程式碼。 一開始我視為使用 hello [HAR](http://www.softwareishard.com/blog/har-12-spec/)傳送 HTTP 要求和回應。 不過，這種格式最適合用於儲存 JSON 格式的一連串 HTTP 要求。 它包含必要的項目加入不必要的複雜性 hello 案例中的 hello wire 上傳送 hello HTTP 訊息數。  

可用的替代選項是 toouse hello`application/http`媒體類型 hello HTTP 規格中所述[RFC 7230](http://tools.ietf.org/html/rfc7230)。 這個媒體類型會使用完全相同格式也就是使用的 tooactually 傳送 HTTP 訊息上 hello 傳輸，但 hello 整個訊息可以放置 hello 另一個的 HTTP 要求主體中的 hello。 在我們的案例只我們 toouse hello 主體為我們訊息 toosend tooEvent 集線器。 為了方便起見，已存在於的剖析器[Microsoft ASP.NET Web API 2.2 用戶端](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)程式庫可以剖析此格式，並將它轉換成 hello 原生`HttpRequestMessage`和`HttpResponseMessage`物件。

toobe 無法 toocreate 這則訊息，我們需要 tootake 利用 C# 基礎[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)在 Azure API 管理。 以下是將傳送 HTTP 要求訊息 tooAzure 事件中心 hello 原則。

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>原則宣告
此原則運算式有一些值得一提的特別之處。 hello 記錄到事件中樞原則都有稱為記錄器識別碼指的是 toohello 未 hello API 管理服務中建立的記錄器名稱的屬性。 詳細資料的方式 toosetup hello API 管理服務中的事件中樞記錄器可以找到 hello 文件中的 hello[如何 toolog 事件 tooAzure Azure API 管理中的事件中樞](api-management-howto-log-event-hubs.md)。 hello 第二個屬性是選擇性參數，指示事件中心中的資料分割 toostore hello 訊息。 事件中心使用資料分割 tooenable scalabilty，而且需要至少有兩個。 依序傳遞訊息的 hello 只保證在資料分割中。 如果我們無法執行指示事件中心，資料分割 tooplace hello 訊息，則會使用循環配置資源演算法 toodistribute hello 負載。 但是，可能會導致某些不按順序處理我們訊息 toobe。  

### <a name="partitions"></a>分割數
tooensure tooconsumers 會依序傳遞訊息，並利用 hello 負載散發功能的資料分割，我選擇 toosend HTTP 要求訊息 tooone 磁碟分割及 HTTP 回應訊息 tooa 第二個資料分割。 如此可確保負載平均分散，而且我們可以保證所有要求和所有回應都會依序取用。 很可能讓取用 hello 對應的要求，再回應 toobe 但，並不是問題，因為我們有不同的機制，相互關聯的要求 tooresponses 以及我們已經知道要求一律前面回應。

### <a name="http-payloads"></a>HTTP 裝載
在建置 hello 之後`requestLine`我們檢查 toosee hello 要求主體應該會被截斷。 hello 要求主體是被截斷的 tooonly 1024。 這可能會增加，個別的事件中樞訊息不過是有限的 too256KB，因此很可能在某些 HTTP 訊息委員將未納入單一訊息。 進行記錄和分析大量的資訊時，都可以衍生自剛 hello HTTP 要求行和標頭。 此外，許多應用程式開發介面要求只會傳回小型的內文和 hello 遺失的資訊值，藉由截斷大型主體是相當基本比較 toohello 減少在傳送中，因此處理和儲存體成本 tookeep 所有本文內容。 最後一個處理 hello 本文的相關注意事項是，我們需要 toopass`true`為 toohello<string>（） 方法因為我們會閱讀 hello 本文內容，但卻是也想 hello 後端 API toobe 無法 tooread hello 主體。 藉由傳遞 true toothis 方法，我們會導致 hello 主體 toobe 緩衝處理，使它能夠讀取第二次的內容。 這是重要 toobe 注意如果您有未上傳的極大型的檔案，或使用長輪詢的 API。 在這些情況下將最佳 tooavoid 讀取 hello 主體。   

### <a name="http-headers"></a>HTTP 標頭
HTTP 標頭可以只透過傳送 hello 訊息格式，以簡單的索引鍵/值組格式。 我們已選擇特定安全性 toostrip 機密欄位，tooavoid 不必要地洩漏認證資訊。 API 金鑰及其他認證不太可能用於分析。 如果我們想 toodo 分析 hello 使用者和特定產品的 hello 他們使用，則我們無法取得從 hello`context`物件，並將該 toohello 訊息。     

### <a name="message-metadata"></a>訊息中繼資料
建置時 hello 完整訊息 toosend toohello 事件中樞，hello 第一行不是實際的部份 hello`application/http`訊息。 hello 第一行會組成 hello 訊息是否為要求或回應訊息的其他中繼資料，以及訊息識別碼是使用的 toocorrelate 要求 tooresponses。 建立 hello 訊息識別碼並使用另一個原則，看起來像這樣：

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

我們無法建立儲存在變數中，直到 hello 回應，已傳回並在然後只要 hello 要求和回應以傳送單一訊息的 hello 要求訊息。 不過，透過獨立地傳送 hello 要求和回應，並使用訊息識別碼 toocorrelate hello 兩個，我們得到更多的彈性 hello 訊息大小、 hello 能力 tootake 利用多個資料分割維護訊息順序和 hello 儘管要求會出現在記錄儀表板更快。 也可能會有某些情況下，有效的回應永遠不會傳送 toohello 事件中樞，可能是因為 hello API 管理服務，tooa 嚴重的要求發生錯誤，但我們仍會有 hello 要求的記錄。

hello 原則 toosend hello 回應 HTTP 訊息看起來非常類似 toohello 要求，並讓 hello 完成原則組態看起來像這樣：

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

hello`set-variable`原則會建立值，可以存取這兩個 hello`log-to-eventhub`中 hello 原則`<inbound>`區段和 hello `<outbound>` > 一節。  

## <a name="receiving-events-from-event-hubs"></a>從事件中樞接收事件
從 Azure 事件中心的事件接收使用 hello [AMQP 通訊協定](http://www.amqp.org/)。 hello Microsoft 服務匯流排團隊已進行用戶端程式庫可用 toomake hello 取用事件更容易。 有兩種不同的方法，支援，其中一個正在*直接取用者*且 hello 其他使用 hello`EventProcessorHost`類別。 這兩種方法的範例可以在 hello[事件中心程式設計指南](../event-hubs/event-hubs-programming-guide.md)。 hello 簡短版本 hello 差異是，`Direct Consumer`可讓您完全控制與 hello`EventProcessorHost`沒有某些 hello 配管工作，但可以讓假設您將處理這些事件的方式。  

### <a name="eventprocessorhost"></a>EventProcessorHost
在此範例中，我們將使用 hello`EventProcessorHost`為了簡單起見，不過它可能不 hello 這個特定案例的最佳選擇。 `EventProcessorHost`沒有 hello 費力並確定您沒有 tooworry 關於執行緒特定的事件處理器類別內的問題。 不過，在我們的案例中，我們會直接轉換 hello 訊息 tooanother 格式和傳遞 tooanother 服務使用的非同步方法。 不需要更新共用狀態，因此沒有執行緒問題的風險。 大部分情況下，`EventProcessorHost`很可能是 hello 最佳選擇，而且很近 hello 更容易選項。     

### <a name="ieventprocessor"></a>IEventProcessor
當使用 hello 中心概念`EventProcessorHost`是 toocreate hello 的實作`IEventProcessor`包含 hello 方法介面`ProcessEventAsync`。 該方法的 hello 本質如下所示：

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

EventData 物件清單會傳遞至 hello 方法，並且我們逐一該清單。 hello 位元組，每個方法會剖析成 HttpMessage 物件，該物件會傳遞 IHttpMessageProcessor tooan 執行個體。

### <a name="httpmessage"></a>HttpMessage
hello`HttpMessage`執行個體包含三個資料片段：

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

hello`HttpMessage`執行個體會包含`MessageId`tooconnect hello HTTP 要求 toohello 對應的 HTTP 回應和布林值，可讓我們的 GUID 識別如果 hello 物件包含執行個體的 HttpRequestMessage，HttpResponseMessage。 使用 HTTP 類別，從內建的 hello `System.Net.Http`，已無法 tootake 優點 hello`application/http`剖析程式碼中包含`System.Net.Http.Formatting`。  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
hello`HttpMessage`執行個體然後轉送的 tooimplementation`IHttpMessageProcessor`這是我建立 toodecouple hello 接收和解譯的 hello 事件從 Azure 事件中樞與 hello 實際處理它的介面。

## <a name="forwarding-hello-http-message"></a>轉送 hello HTTP 訊息
此範例中，我決定很有趣 toopush hello HTTP 要求透過太[Runscope](http://www.runscope.com)。 Runscope 是專門從事 HTTP 偵錯、記錄和監視的雲端架構服務。 它們有免費層次中，因此容易 tootry 且它可讓我們 toosee hello HTTP 要求中即時流經我們的 API 管理服務。

hello`IHttpMessageProcessor`實作看起來像這樣，

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

我已能 tootake 利用[Runscope 現有用戶端程式庫](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha)，能讓您輕鬆 toopush`HttpRequestMessage`和`HttpResponseMessage`到他們的服務執行個體上。 順序 tooaccess hello Runscope API，您將需要帳戶和 API 金鑰。 取得 API 金鑰可指示 hello[建立應用程式 tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api)錄影畫面。

## <a name="complete-sample"></a>完整範例
hello[原始程式碼](https://github.com/darrelmiller/ApimEventProcessor)而 hello 範例的測試是在 GitHub 上。 您將需要[API 管理服務](api-management-get-started.md)，[連接的事件中樞](api-management-howto-log-event-hubs.md)，和[儲存體帳戶](../storage/common/storage-create-storage-account.md)自行 toorun hello 範例。   

hello 範例是只是簡單主控台應用程式所接聽的事件來自事件中心，將轉換到`HttpRequestMessage`和`HttpResponseMessage`物件，然後再將它們轉送 toohello Runscope 應用程式開發介面上。

在 hello 下列動畫的影像，您可以看到提出的要求正在進行 tooan API 在 hello 開發人員入口網站，hello 主控台應用程式顯示 hello 訊息接收、 處理和轉送，然後 hello 要求和回應 hello Runscope 流量中顯示偵測器。

![要求正在轉送 tooRunscope 的示範](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>摘要
Azure API 管理服務會提供從您的應用程式開發介面移動 tooand 好 toocapture hello HTTP 流量。 Azure 事件中樞是一個可高度擴充、低成本的解決方案，用來擷取該流量並將它饋送到次要處理系統中，以便進行記錄、監視和其他複雜的分析。 連接 too3rd 合作對象流量監視系統，例如 Runscope 數十種少量的程式碼做為簡單。

## <a name="next-steps"></a>後續步驟
* 深入了解 Azure 事件中樞
  * [開始使用 Azure 事件中樞](../event-hubs/event-hubs-c-getstarted-send.md)
  * [使用 EventProcessorHost 接收訊息](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [事件中樞程式設計指南](../event-hubs/event-hubs-programming-guide.md)
* 深入了解 API 管理和事件中樞的整合
  * [如何 toolog 事件 tooAzure Azure API 管理中的事件中樞](api-management-howto-log-event-hubs.md)
  * [記錄器實體參考](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [log-to-eventhub 原則參考](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
