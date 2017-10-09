---
title: "您的 Azure 程式碼在 Visual Studio 中的 aaaOptimizing |Microsoft 文件"
description: "了解 Visual Studio 中的 Azure 程式碼最佳化工具如何協助讓程式碼更穩定且有更好的效能。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>最佳化您的 Azure 程式碼
您正在設計程式時使用 Microsoft Azure 的應用程式，有一些編碼方式，您應該遵循 toohelp 避免發生問題的應用程式延展性、 行為和雲端環境中的效能。 Microsoft 有提供 Azure Code Analysis 工具，可辨識並找出許多常見問題，並幫助您解決這些問題。 您可以下載 Visual Studio 中透過 NuGet 中的 hello 工具。

## <a name="azure-code-analysis-rules"></a>Azure Code Analysis 規則
hello Azure 程式碼分析工具會使用下列規則 tooautomatically 旗標 Azure 程式碼，並且在找到效能影響的已知的問題的 hello。 偵測到的問題會顯示為警告或編譯器錯誤。 通常透過燈泡圖示提供程式碼修正或建議 tooresolve hello 警告或錯誤。

## <a name="avoid-using-default-in-process-session-state-mode"></a>避免使用預設 (同處理序) 工作階段狀態模式
### <a name="id"></a>ID
AP0000

### <a name="description"></a>說明
如果您的雲端應用程式使用 hello 預設 （同處理序） 工作階段狀態模式，您可能會遺失工作階段狀態。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
根據預設，hello hello web.config 檔案中指定的工作階段狀態模式是同處理序。 此外，如果沒有 hello 組態檔中指定的項目，hello 工作階段狀態模式會預設 tooin 程序。 hello 同處理序模式會將工作階段狀態儲存在 hello web 伺服器上的記憶體。 當重新啟動執行個體或負載平衡或容錯移轉支援使用新的執行個體時，不會儲存 hello 工作階段狀態儲存在 hello web 伺服器上的記憶體。 這種情況下，防止 hello 從 hello 雲端上可擴充的應用程式。

ASP.NET 工作階段狀態支援數種不同的工作階段狀態資料儲存選項：InProc、StateServer、SQLServer、自訂和關閉。 建議您自訂模式 toohost 資料上使用外部的工作階段狀態存放區，例如[Redis 的 Azure 工作階段狀態提供者](http://go.microsoft.com/fwlink/?LinkId=401521)。

### <a name="solution"></a>方案
建議的解決方案之一，是在受管理快取服務 toostore 工作階段狀態。 深入了解如何 toouse [Redis 的 Azure 工作階段狀態提供者](http://go.microsoft.com/fwlink/?LinkId=401521)toostore 工作階段狀態。 您可以也存放區的工作階段狀態中其他地方 tooensure hello 雲端位於可擴充您的應用程式。 深入了解替代方案，請閱讀 toolearn[工作階段狀態模式](https://msdn.microsoft.com/library/ms178586)。

## <a name="run-method-should-not-be-async"></a>執行方法必須同步
### <a name="id"></a>ID
AP1000

### <a name="description"></a>說明
建立非同步方法 (例如[await](https://msdn.microsoft.com/library/hh156528.aspx)) 外部 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，然後呼叫 hello 非同步方法，從[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)。 宣告 hello [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法為非同步會導致 hello 背景工作角色 tooenter 重新啟動迴圈。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
Hello 內呼叫非同步方法[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法會導致 hello 雲端服務執行階段 toorecycle hello 背景工作角色。 所有程式執行的背景工作角色啟動時，都都在 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法。 現有的 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法會導致 hello 背景工作角色 toorestart。 當 hello 背景工作角色執行階段叫用 hello 非同步方法時，它會分派 hello 非同步方法之後的所有作業，然後傳回。 這會導致 hello 背景工作角色 tooexit 從 hello [ [ [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法並重新啟動。 Hello 下一個反覆項目中執行的再次 hello 非同步方法並重新啟動時，造成 hello 背景工作角色 toorecycle 一次也會叫用 hello 背景工作角色。

### <a name="solution"></a>方案
放置 hello 之外的所有非同步作業[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法。 然後，呼叫 hello 重構非同步方法，從內 hello [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，例如 RunAsync （).wait。 hello Azure 程式碼分析工具可協助您修正此問題。

下列程式碼片段的 hello 示範 hello 程式碼修正此問題：

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>使用服務匯流排共用存取簽章驗證
### <a name="id"></a>ID
AP2000

### <a name="description"></a>說明
使用共用存取簽章 (SAS) 進行驗證。 存取控制服務 (ACS) 將不可再用於進行服務匯流排驗證。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
為加強安全性，Azure Active Directory 將以 SAS 驗證取代 ACS 驗證。 請參閱[Azure Active Directory 是 hello ACS 的未來](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx)hello 轉換計畫的資訊。

### <a name="solution"></a>方案
在應用程式中使用 SAS 驗證。 hello 下列範例顯示如何 toouse 現有 SAS 權杖 tooaccess 服務匯流排命名空間或實體。

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

請參閱下列主題以取得詳細資訊的 hello。

* 如需概觀，請參閱 [使用服務匯流排的共用存取簽章驗證](https://msdn.microsoft.com/library/dn170477.aspx)
* [如何使用服務匯流排的共用存取簽章驗證 toouse](https://msdn.microsoft.com/library/dn205161.aspx)
* 如須專案範例，請參閱 [搭配使用共用存取簽章 (SAS) 驗證與服務匯流排訂用帳戶](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>請考慮使用 OnMessage 方法 tooavoid 「 接收迴圈 」
### <a name="id"></a>ID
AP2002

### <a name="description"></a>說明
進入 「 接收迴圈 」 tooavoid 呼叫 hello **OnMessage**方法是更好的解決方案來接收訊息比呼叫 hello**接收**方法。 不過，如果您必須使用 hello**接收**方法之外，指定非預設伺服器等待時間，請確定 hello 伺服器等待時間超過一分鐘。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
當呼叫**OnMessage**，hello 用戶端啟動內部訊息幫浦，持續地輪詢 hello 佇列或訂閱。 此訊息幫浦包含無限迴圈，發出呼叫 tooreceive 訊息。 如果 hello 呼叫逾時，它就會發出新的呼叫。 hello 逾時間隔由 hello hello 值[OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx)屬性 hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)正在使用。

hello 使用優點**OnMessage**太比較**接收**是使用者不需要輪詢訊息、 處理例外狀況、 處理多個訊息，以平行方式，和完成 hello toomanually訊息。

如果您呼叫**接收**不使用其預設值，可確定 hello *ServerWaitTime*值是一分鐘以上。 設定*ServerWaitTime*超過一分鐘 toomore 防止 hello 伺服器完全收到 hello 訊息之前逾時。

### <a name="solution"></a>方案
請 hello 遵循建議的使用方式的程式碼範例，參閱。 如需詳細資訊，請參閱 [QueueClient.OnMessage 方法 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) 和 [QueueClient.Receive 方法 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx)。

tooimprove hello 效能的 hello Azure 傳訊基礎結構，請參閱 hello 設計模式[非同步傳訊入門](https://msdn.microsoft.com/library/dn589781.aspx)。

hello 以下是示範如何使用**OnMessage** tooreceive 訊息。

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

hello 以下是示範如何使用**接收**與 hello 預設伺服器等待時間。

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

hello 以下是示範如何使用**接收**與非預設伺服器等待時間。

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>考慮使用非同步服務匯流排方法
### <a name="id"></a>ID
AP2003

### <a name="description"></a>說明
使用非同步服務匯流排方法 tooimprove 效能代理傳訊。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
使用非同步方法可讓應用程式並行存取，因為執行每個呼叫不會封鎖 hello 主要執行緒。 使用服務匯流排傳訊方法時，需要花時間執行各項作業 (傳送、接收、刪除等)。 此時根據 hello 服務匯流排服務包括 hello 處理 hello 作業的加法 toohello 延遲 hello 要求與 hello 回覆中。 tooincrease hello 數字，每次的作業，必須同時執行作業。 如需詳細資訊，請參閱太[的效能改進使用 Service Bus 代理訊息的最佳作法](https://msdn.microsoft.com/library/azure/hh528527.aspx)。

### <a name="solution"></a>方案
請參閱[QueueClient 類別 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx)有關 toouse hello 建議的非同步方法的使用。

tooimprove hello 效能的 hello Azure 傳訊基礎結構，請參閱 hello 設計模式[非同步傳訊入門](https://msdn.microsoft.com/library/dn589781.aspx)。

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>考慮分割服務匯流排佇列和主題
### <a name="id"></a>ID
AP2004

### <a name="description"></a>說明
分割服務匯流排佇列和主題以獲得更好的服務匯流排傳訊效能。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
資料分割服務匯流排佇列和主題可提升效能的輸送量和服務的可用性，因為 hello 分割的佇列或主題的整體輸送量不會再受限於單一訊息代理程式或訊息存放區的 hello 效能。 此外，即使訊息存放區暫時中斷也不會讓分割後的佇列或主題無法使用。 如需詳細資訊，請參閱 [分割訊息實體](https://msdn.microsoft.com/library/azure/dn520246.aspx)。

### <a name="solution"></a>方案
hello 下列程式碼片段會示範如何 toopartition 傳訊實體。

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

如需詳細資訊，請參閱[分割服務匯流排佇列和主題 |Microsoft Azure 部落格](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/)與簽出 hello [Microsoft Azure 服務匯流排分割的佇列](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f)範例。

## <a name="do-not-set-sharedaccessstarttime"></a>不要設定 SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>說明
您應該避免使用 SharedAccessStartTimeset toohello tooimmediately 啟動 hello 共用存取原則的目前時間。 您只需要 tooset 這個屬性如果您稍後想 toostart hello 共用存取原則。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
時鐘同步處理會讓資料中心彼此間產生些微時差。 例如，您會以邏輯方式將儲存體 SAS 原則設定 hello 開始時間視為 hello 目前的時間使用 DateTime.Now 或類似的方法會導致 hello SAS 原則 tootake 效果立即。 不過，資料中心之間的 hello 時間稍微會造成這個問題，因為某些資料中心時間可能稍微晚於 hello 開始時間，而其他則比較早。 如此一來，hello SAS 原則可能很快過期 （甚至是立即） 如果 hello 原則存留時間設定太短。

如需詳細指引 Azure 儲存體上使用共用存取簽章的詳細資訊，請參閱[簡介資料表 SAS （共用存取簽章）、 佇列 SAS 以及更新 tooBlob SAS-Microsoft Azure 儲存體團隊部落格-網站首頁-MSDN 部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)。

### <a name="solution"></a>方案
移除設定 hello hello 共用存取原則的開始時間的 hello 陳述式。 hello Azure 程式碼分析工具會提供修正此問題。 如需有關安全性管理的詳細資訊，請參閱 hello 設計模式[附屬金鑰模式](https://msdn.microsoft.com/library/dn568102.aspx)。

下列程式碼片段的 hello 示範 hello 程式碼修正此問題。

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>共用存取原則的到期時間必須超過五分鐘
### <a name="id"></a>ID
AP3002

### <a name="description"></a>說明
可以是如往常般到期 tooa 所謂 「 時鐘誤差。 」 的不同位置的資料中心之間的時鐘相差五分鐘 tooprevent hello SAS 原則權杖過期之前的已規劃、 設定 hello 到期時間 toobe 超過五分鐘。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
時脈訊號而同步化 hello 世界各地的不同位置的資料中心。 因為它需要花費一些時間時脈訊號 tootravel toodifferent 位置，可以有不同的地理位置的資料中心之間的時差雖然真地同步處理的所有項目。 這項時間差異可能會影響 hello 共用存取原則開始時間和到期間隔。 因此，tooensure 共用存取原則會立即生效，不會指定 hello 開始時間。 此外，請確定 hello 到期時間超過 5 分鐘 tooprevent 提早逾時。

如需 Azure 儲存體上使用共用存取簽章的詳細資訊，請參閱[簡介資料表 SAS （共用存取簽章）、 佇列 SAS 以及更新 tooBlob SAS-Microsoft Azure 儲存體團隊部落格-網站首頁-MSDN 部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)。

### <a name="solution"></a>方案
如需有關安全性管理的詳細資訊，請參閱 hello 設計模式[附屬金鑰模式](https://msdn.microsoft.com/library/dn568102.aspx)。

hello 以下是範例未指定共用存取原則開始時間。

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

hello 以下是範例原則到期持續時間超過五分鐘的指定共用存取原則開始時間。

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

如需詳細資訊，請參閱 [建立和使用共用存取簽章](https://msdn.microsoft.com/library/azure/jj721951.aspx)。

## <a name="use-cloudconfigurationmanager"></a>使用 CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>說明
使用 hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx)專案的類別，例如 Azure 網站和 Azure 行動服務不會產生執行階段問題。 最佳做法，不過，它是個不錯的主意 toouse 雲端[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx)做為統一的管理所有 Azure 雲端應用程式的設定方式。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
CloudConfigurationManager 讀取 hello 組態檔案適當 toohello 應用程式環境。

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>方案
重構程式碼 toouse hello [CloudConfigurationManager 類別](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)。 Hello Azure 程式碼分析工具會提供程式碼修正此問題。

下列程式碼片段的 hello 示範 hello 程式碼修正此問題。 Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

取代為

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

以下是如何 toostore hello App.config 或 Web.config 檔案中的組態設定的範例。 新增 hello 設定 toohello hello 設定檔的 appSettings 區段。 hello 以下是上述程式碼範例 hello hello Web.config 檔案。

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>避免使用硬式編碼的連接字串
### <a name="id"></a>ID
AP4001

### <a name="description"></a>說明
如果您使用硬式編碼的連接字串，您需要 tooupdate 這些更新版本中，您將有 toomake 變更 tooyour 原始程式碼並重新編譯 hello 應用程式。 不過，如果您將連接字串儲存在組態檔時，您稍後可以變更它們只要更新 hello 設定檔。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
硬式編碼的連接字串是不良作法，因為當連接字串需要 toobe 快速變更時，它會導致問題。 此外，如果 hello 專案需要 toobe 簽入 toosource 控制，硬式編碼的連接字串會造成安全性漏洞因為 hello 字串就可以在 hello 原始碼檢視。

### <a name="solution"></a>方案
連接字串儲存在 hello 設定檔或 Azure 環境。

* 對於獨立應用程式，使用 app.config toostore 連接字串設定。
* 對於 IIS 裝載的 web 應用程式，使用 web.config toostore 連接字串。
* 對於 ASP.NET vNext 應用程式，使用 configuration.json toostore 連接字串。

如需使用 web.config 或 app.config 等組態檔的相關資訊，請參閱 [ASP.NET Web 組態指導方針](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx)。 如需 Azure 環境變數運作方式的相關資訊，請參閱 [Azure 網站：應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。 如需在原始檔控制中儲存連接字串的相關資訊，請參閱 [避免將敏感資訊 (例如連接字串) 放在儲存於原始程式碼儲存機制的檔案](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)。

## <a name="use-diagnostics-configuration-file"></a>使用診斷組態檔
### <a name="id"></a>ID
AP5000

### <a name="description"></a>說明
而不是使用這類程式碼中設定診斷設定 hello Microsoft.WindowsAzure.Diagnostics 程式設計 API，您應該在 hello diagnostics.wadcfg 檔案設定診斷設定。 (或者，如果您使用 Azure SDK 2.5，則在 diagnostics.wadcfgx 中設定)。 這樣做，您可以變更診斷設定，而不需要 toorecompile 您的程式碼。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
之前使用數種不同的方法，則無法設定 Azure SDK 2.5 （這會使用 Azure 診斷 1.3），Azure 診斷 (WAD): 將它加入 toohello 組態 blob 儲存體中使用命令式程式碼、 宣告式組態或預設 hello組態設定。 不過，hello 慣用方式 tooconfigure 診斷是 toouse XML 組態檔 （diagnostics.wadcfg 或 diagnositcs.wadcfgx SDK 2.5 和更新版本） hello 應用程式專案中。 這種方法，hello diagnostics.wadcfg 檔案完整定義 hello 組態及可以更新並重新部署。 混合 hello 用 hello diagnostics.wadcfg 組態檔以 hello 以程式設計方式設定組態使用 hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)或[RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)類別可能會導致 tooconfusion。 如需詳細資訊，請參閱 [初始化或變更 Azure 診斷組態](https://msdn.microsoft.com/library/azure/hh411537.aspx) 。

從 WAD 1.3 （隨附於 Azure SDK 2.5） 開始，就無法再可能 toouse 程式碼 tooconfigure 診斷。 如此一來，您可以只提供 hello 組態時套用或更新 hello 診斷延伸模組。

### <a name="solution"></a>方案
使用 hello 診斷組態設計工具 toomove 診斷設定 toohello 診斷組態檔 （中的 diagnositcs.wadcfg 或 diagnositcs.wadcfgx SDK 2.5 和更新版本）。 也建議您安裝[Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188)使用 hello 最新的診斷功能。

1. 在 hello 想 tooconfigure hello 角色的捷徑功能表，選擇 內容，然後選擇 hello 設定 索引標籤。
2. 在 hello**診斷**區段中，請確定該 hello**啟用診斷**選取核取方塊。
3. 選擇 hello**設定** 按鈕。

   ![存取 hello 啟用診斷 選項](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   如需詳細資訊，請參閱 [為 Azure 雲端服務和虛擬機器設定診斷功能](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 。

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>避免將 DbContext 物件宣告為靜態
### <a name="id"></a>ID
AP6000

### <a name="description"></a>說明
toosave 記憶體，避免將 DBContext 物件做為靜態宣告。

請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。

### <a name="reason"></a>原因
DBContext 物件保存 hello 從每個呼叫的查詢結果。 Hello 應用程式網域卸載之前，不會處置靜態 DBContext 物件。 因此，靜態 DBContext 物件可能會耗用大量記憶體。

### <a name="solution"></a>方案
將 DBContext 宣告為區域變數或非靜態執行個體欄位、將它用於工作，然後讓它在使用後受到處置。

下列範例 MVC 控制器類別的 hello 顯示 toouse hello DBContext 物件的方式。

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>後續步驟
toolearn 深入了解最佳化和疑難排解 Azure 應用程式，請參閱[疑難排解 web 應用程式中使用 Visual Studio 的 Azure App Service](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。
