---
title: "aaaAzure Service Bus 驗證與共用存取簽章 |Microsoft 文件"
description: "使用共用存取簽章的服務匯流排驗證概觀，詳細說明搭配 Azure 服務匯流排的 SAS 驗證資訊。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>使用共用存取簽章的服務匯流排驗證

*共用存取簽章*(SAS) 是服務匯流排傳訊 hello 主要安全性機制。 這篇文章討論 SAS，其運作方式以及 toouse 它們無從驗證平台的方式。

SAS 驗證可讓應用程式 tooauthenticate tooService 匯流排使用傳訊實體 （佇列或主題） 的特定權限相關聯的 hello 或 hello 命名空間上設定的存取金鑰。 然後，您可以使用此索引鍵 toogenerate 用戶端可以接著使用 tooauthenticate tooService 匯流排 SAS 權杖。

SAS 驗證支援包含在 hello Azure SDK 2.0 或更新版本。

## <a name="overview-of-sas"></a>SAS 的概觀

共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。 SAS 是所有服務匯流排服務使用的非常強大的機制。 在實際使用中，SAS 有兩個元件：「共用存取原則」和「共用存取簽章」(通常稱為「權杖」)。

服務匯流排中的 SAS 驗證包括 hello 組態與服務匯流排資源上的權限相關聯的密碼編譯金鑰。 用戶端的宣告存取 tooService 匯流排資源所呈現 SAS 權杖。 這個語彙基元組成 hello 資源所存取的 URI，以 hello 簽章的到期設定索引鍵。

您可以在服務匯流排[轉送](service-bus-fundamentals-hybrid-solutions.md#relays)、[佇列](service-bus-fundamentals-hybrid-solutions.md#queues)和[主題](service-bus-fundamentals-hybrid-solutions.md#topics)上設定共用存取簽章授權規則。

SAS 驗證會使用下列項目 hello:

* [共用存取授權規則](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)︰Base64 表示法中的 256 位元主要密碼編譯金鑰、選用的次要金鑰以及金鑰名稱和相關權限 (接聽、傳送或管理權限的集合)。
* [共用存取簽章](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider)語彙基元： 產生 hello hmac-sha256 的資源，所組成的字串 hello hello 所存取之資源的 URI、 過期以及使用 hello 密碼編譯金鑰。 hello 簽章與 hello 下列各節中所述的其他項目會被格式化成字串 tooform hello SAS 權杖。

## <a name="shared-access-policy"></a>共用存取原則

需 SAS 的重點 toounderstand 是啟動與原則。 針對每個原則，您會決定三段資訊：**名稱**、**範圍**和**權限**。 hello**名稱**僅是; 該範圍內的唯一名稱。 hello 範圍也很簡單： 其 hello hello 資源有問題的 URI。 服務匯流排命名空間 hello 範圍是 hello 完整的網域名稱 (FQDN)，例如`https://<yournamespace>.servicebus.windows.net/`。

大部分一目了然 hello 可用權限的原則︰

* 傳送
* 接聽
* 管理

建立 hello 原則之後，它指派*主索引鍵*和*次要金鑰*。 這些是密碼編譯增強式金鑰。 不會失去它們，或遺漏它們-它們永遠都可在 hello [Azure 入口網站][Azure portal]。 您可以使用其中一個 hello 產生金鑰，您可以隨時重新產生它們。 不過，如果您重新產生，或變更 hello hello 原則中的主索引鍵，從它建立任何共用存取簽章將會失效。

當您建立服務匯流排命名空間時，稱為 hello 整個命名空間會自動建立的原則**RootManageSharedAccessKey**，而且此原則有所有的權限。 您未以 **root** 登入，所以除非有適合的理由，請勿使用此原則。 您可以建立額外的原則中 hello**設定**hello hello 入口網站中的命名空間的索引標籤。 向上 too12 附加 tooit 只能有單一樹狀結構中的層級 （命名空間、 佇列等） 的服務匯流排的重要 toonote 它。

## <a name="configuration-for-shared-access-signature-authentication"></a>共用存取簽章驗證的設定
您可以設定 hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)服務匯流排命名空間、 佇列或主題上的規則。 設定[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)服務匯流排訂用帳戶目前不支援，但是您可以使用命名空間或主題 toosecure 存取 toosubscriptions 上設定的規則。 說明此程序的工作範例，請參閱 hello[搭配 Servicebus 訂閱使用共用存取簽章 (SAS) 驗證](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c)範例。

在服務匯流排命名空間、佇列或主題上最多可以設定 12 條這類規則。 服務匯流排命名空間所設定的規則適用於該命名空間中的 tooall 實體。

![SAS](./media/service-bus-sas/service-bus-namespace.png)

在此圖中，hello *manageRuleNS*， *sendRuleNS*，和*listenRuleNS*授權規則套用 tooboth 佇列 Q1 和主題 T1，而*listenRuleQ*和*sendRuleQ*套用 tooqueue Q1 和*sendRuleT*適用於 tootopic T1。

hello 的索引鍵參數[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)如下：

| 參數 | 說明 |
| --- | --- |
| *KeyName* |描述 hello 授權規則的字串。 |
| *PrimaryKey* |Base64 編碼 256 位元主要金鑰來簽署和驗證 hello SAS 權杖。 |
| *SecondaryKey* |Base64 編碼 256 位元次要金鑰來簽署和驗證 hello SAS 權杖。 |
| *AccessRights* |Hello 授權規則授與的存取權限清單。 這些權限可以是任何接聽、傳送和管理權限的集合。 |

服務匯流排命名空間是佈建， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)，與[KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName)設定得**RootManageSharedAccessKey**，預設會建立。

## <a name="generate-a-shared-access-signature-token"></a>產生共用存取簽章 (權杖)

hello 原則本身不是服務匯流排的 hello 存取權杖。 它是 hello 物件的 hello 存取權杖以產生-使用任一 hello 主要或次要金鑰。 已簽署 hello 共用的存取授權規則中指定的金鑰存取 toohello 任何用戶端可能會產生 hello SAS 權杖。 請仔細製作 hello 遵循格式字串所產生 hello 語彙基元：

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

其中`signature-string`hello hello 語彙基元範圍 hello sha-256 雜湊 (**範圍**hello 上一節中所述) CRLF，附加與到期時間 (以秒為單位 hello 新紀元以來的： `00:00:00 UTC` 1 年 1 月從 1970)。 

> [!NOTE]
> tooavoid 簡短權杖到期時間，建議您為至少為 32 位元不帶正負號的整數，或最好是長時間 （64 位元） 整數編碼 hello 到期時間值。  
> 
> 

hello 雜湊看起來類似 toohello 下列虛擬程式碼，並傳回 32 個位元組。

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

hello 非雜湊值如下所示 hello **SharedAccessSignature**以便 hello 收件者可以計算出 hello 雜湊的字串 hello 與相同的參數，確認它傳回 toobe hello 相同的結果。 hello URI 指定 hello 範圍和 hello 索引鍵名稱識別 hello 原則使用 toobe toocompute hello 雜湊。 從安全性的觀點而言，這很重要。 如果 hello 簽章不符合哪些 hello 收件者 (Service Bus) 計算的則會拒絕存取。 此時您可以確定該 hello 寄件者有存取 toohello 金鑰，應該被授與 hello hello 原則中指定的權限。

請注意，您應該使用 hello 編碼這項作業的資源 URI。 hello 資源 URI 為 hello Service Bus toowhich 存取資源的完整 URI 宣告的 hello。 例如，`http://<namespace>.servicebus.windows.net/<entityPath>` 或 `sb://<namespace>.servicebus.windows.net/<entityPath>`；也就是 `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`。

必須指定此 URI，或其中一個階層上層的 hello 實體上設定 hello 用於簽章的共用的存取授權規則。 例如，`http://contoso.servicebus.windows.net/contosoTopics/T1`或`http://contoso.servicebus.windows.net`hello 前一個範例中。

SAS 權杖的有效 hello 下所有資源`<resourceURI>`用於 hello `signature-string`。

hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName)在 hello SAS 權杖是指 toohello **keyName** hello 的共用的存取授權規則使用 toogenerate hello 語彙基元。

hello *URL 編碼 resourceURI*必須是 hello 與 hello hello 計算 hello 簽章期間用於 hello 字串簽章 URI 相同。 它應該是 [百分比編碼](https://msdn.microsoft.com/library/4fkewx0t.aspx)。

建議您定期重新產生用於 hello 的 hello 金鑰[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件。 應用程式，通常應該使用 hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate SAS 權杖。 當重新產生 hello 金鑰，您應該取代 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) hello 舊主要金鑰，並產生新的金鑰為 hello 新主索引鍵。 這可讓您 toocontinue 使用 token 簽發 hello 舊的主索引鍵和，有尚未到期的授權。

如果金鑰被盜，而且您有 toorevoke hello 索引鍵，您可以重新產生兩個 hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey)和 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey)的[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)，請將其取代為新的金鑰。 此程序會認證所有與 hello 舊金鑰簽章的權杖。

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>如何使用服務匯流排 toouse 共用存取簽章驗證

下列案例的 hello 包括授權規則的設定、 產生 SAS 權杖，以及用戶端授權。

完整的說明 hello 設定和使用 SAS 授權的服務匯流排應用程式的工作範例，請參閱[使用服務匯流排的共用存取簽章驗證](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8)。 這裡會提供相關的範例，說明如何使用命名空間或主題 toosecure 服務匯流排訂用帳戶上設定 SAS 授權規則 hello:[搭配 Servicebus 訂閱使用共用存取簽章 (SAS) 驗證](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>存取命名空間上的共用存取授權規則

Hello 服務匯流排命名空間根目錄上的作業需要憑證驗證。 您必須針對您的 Azure 訂用帳戶上傳管理憑證。 tooupload 管理憑證，請依照下列步驟 hello[這裡](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate)，使用 hello [Azure 入口網站][Azure portal]。 如需有關 Azure 管理憑證的詳細資訊，請參閱 hello [Azure 憑證概觀](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates)。

用於存取服務匯流排命名空間上的共用的存取授權規則的 hello 端點如下所示：

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件上的服務匯流排命名空間，請執行此端點上的 POST 作業具有序列化為 JSON 或 XML hello 規則資訊。 例如：

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

同樣地，使用 hello 端點 tooread hello 授權規則 hello 命名空間上設定的 「 取得 」 作業。

tooupdate 或刪除特定授權規則，請使用下列端點 hello:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>存取實體上的共用存取授權規則

您可以存取[Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件上的服務匯流排佇列或主題透過 hello 設定[AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules)中 hello 集合對應[QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription)或[TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription)。

下列程式碼的 hello 顯示佇列 tooadd 授權規則的方式。

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>使用共用存取簽章授權

使用 hello Azure.NET SDK 與 hello 服務匯流排.NET 程式庫的應用程式可以使用 SAS 授權透過 hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider)類別。 hello 下列程式碼說明如何 hello 使用 hello 權杖提供者 toosend 訊息 tooa 服務匯流排佇列。

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

應用程式在接受連接字串的方法中使用 SAS 連接字串，也可以使用 SAS 進行驗證。

請注意該 toouse SAS 授權，使用服務匯流排轉送，您可以使用設定 hello 服務匯流排命名空間的 SAS 金鑰。 如果您明確建立轉送 hello 命名空間 ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)與[RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) 物件，您可以設定該轉送的 hello SAS 規則。 具有服務匯流排訂閱 toouse SAS 授權，您可以使用服務匯流排命名空間或主題上設定的 SAS 金鑰。

## <a name="use-hello-shared-access-signature-at-http-level"></a>使用共用存取簽章 hello （在 HTTP 層級）

您現在知道 toocreate 共用存取簽章服務匯流排中的任何實體，您在準備 tooperform HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

請記住，這適用於所有項目。 您可以為佇列、主題或訂用帳戶建立 SAS。 

如果您提供的寄件者或用戶端的 SAS 權杖，不會直接管理，擁有 hello 索引鍵，而且它們無法回復 hello 雜湊 tooobtain 它。 因此，您可以控制他們可以存取的項目，以及時間長度。 重要的事情 tooremember 是，如果您變更 hello hello 原則中的主索引鍵，從它建立任何共用存取簽章將失效。

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>使用共用存取簽章 hello （在 AMQP 層級）

Hello 上一節，在您已看到如何 toouse hello 與 HTTP POST 要求來傳送資料 toohello 服務匯流排 SAS 權杖。 您知道，您可以存取 Service Bus 使用 hello 進階訊息佇列通訊協定 (AMQP) 是基於效能考量，在許多案例中的 hello 慣用通訊協定 toouse。 hello SAS 權杖的用法與 AMQP 述 hello 文件[AMQP Claim-Based Security 版本 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc)也就是在工作草稿自今天 2013 但完善 azure 支援。

開始之前 toosend 資料 tooService 匯流排，hello 發行者必須傳送 hello SAS 權杖，節點的內部 AMQP 訊息 tooa 完善 AMQP 名為**$cbs** （您可以將它視為 hello 服務 tooacquire 所使用的 「 特殊 」 佇列並驗證所有hello SAS 權杖）。 hello 發行者必須指定 hello **ReplyTo**欄位內 hello AMQP 訊息; 這是 hello 節點中的 hello 服務回覆 toohello 發行者與 hello token 的驗證 （簡單要求/回覆模式之間的 hello 結果發行者和服務）。 會建立此回覆節點 hello 動態，」 講述 hello AMQP 1.0 規格所描述的 「 動態建立的遠端節點 」。 在檢查該 hello SAS 權杖有效的之後, 可以向前 hello 發行者，並將其啟動 toosend 資料 toohello 服務中。

hello 下列步驟顯示如何 toosend hello 使用 AMQP 通訊協定使用 hello 的 SAS 權杖[AMQP.Net Lite](https://github.com/Azure/amqpnetlite)程式庫。 這非常有用，如果您無法使用 hello 官方服務匯流排 SDK (例如在 WinRT，.Net Compact Framework、.Net 微架構和單聲道) 在 C 中開發\#。 當然，此程式庫是有用 toohelp 了解如何以宣告為基礎的安全性層級 hello AMQP，運作方式，如同在 hello HTTP 層級 （使用 HTTP POST 要求和 hello SAS 權杖內傳送的嗨 「 授權 」 標頭中） 的運作方式。 如果您不需要這類 AMQP 深度的知識，您可以使用 hello 官方服務匯流排 SDK 與.Net Framework 應用程式，將會替您完成。

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

hello`PutCbsToken()`方法會接收 hello*連接*(AMQP 連接類別執行個體所提供 hello [AMQP.NET Lite 程式庫](https://github.com/Azure/amqpnetlite)) 表示 hello TCP 連線 toohello 服務和 hello*sasToken* hello SAS 權杖 toosend 參數。 

> [!NOTE]
> 請務必 hello 連線會透過**SASL 驗證機制設定 tooEXTERNAL** （和不 hello 使用者名稱和密碼，您不需要 toosend hello SAS 權杖時使用的預設純）。
> 
> 

接下來，hello 「 發行者 」 會建立兩個 AMQP 連結來傳送 hello SAS 權杖，以及從 hello 服務收到 hello 回覆 （hello 權杖驗證結果）。

hello AMQP 訊息包含一組屬性，以及比簡單訊息的詳細資訊。 hello SAS 權杖是 hello 主體 hello 訊息 （使用其建構函式）。 hello **"ReplyTo"**屬性設定為接收 hello hello 接收者連結 （您可以變更其名稱，而且它將會自動建立 hello 服務如果） 上的驗證結果 toohello 節點名稱。 hello 最後三個應用程式/自訂屬性由 hello 服務 tooindicate 何種類型的作業，它有 tooexecute。 如同 hello CBS 草稿規格所述，它們必須是 hello**作業名稱**（「 put-權杖 」），hello**權杖的型別**（在這個情況下，「 servicebus.windows.net:sastoken")，和 hello **"名稱"hello 觀眾**toowhich hello 語彙基元適用於 （hello 整個實體）。

Hello 寄件者連結傳送 hello SAS 權杖後, hello 發行者必須讀取 hello 回應 hello 接收者連結。 hello 回覆是名為應用程式屬性的簡單 AMQP 訊息**」 狀態碼 「**可以容納的 hello 相同值，則為 HTTP 狀態碼。

## <a name="rights-required-for-service-bus-operations"></a>服務匯流排作業所需的權限

hello 下表顯示 hello 所需的各項作業上服務匯流排資源的存取權限。

| 作業 | 所需的宣告 | 宣告範圍 |
| --- | --- | --- |
| **命名空間** | | |
| 在命名空間上設定授權規則 |管理 |任何命名空間位址 |
| **服務登錄** | | |
| 列舉私人原則 |管理 |任何命名空間位址 |
| 開始在命名空間上接聽 |接聽 |任何命名空間位址 |
| 在命名空間中傳送訊息 tooa 接聽程式 |傳送 |任何命名空間位址 |
| **佇列** | | |
| 建立佇列 |管理 |任何命名空間位址 |
| 刪除佇列 |管理 |任何有效的佇列位址 |
| 列舉佇列 |管理 |/$Resources/Queues |
| 取得 hello 佇列描述 |管理 |任何有效的佇列位址 |
| 設定佇列的授權規則 |管理 |任何有效的佇列位址 |
| 傳送到 toohello 佇列 |傳送 |任何有效的佇列位址 |
| 從佇列接收訊息 |接聽 |任何有效的佇列位址 |
| 放棄或完成訊息接收 hello 訊息，以查看並鎖定模式之後 |接聽 |任何有效的佇列位址 |
| 延遲訊息以便稍後擷取 |接聽 |任何有效的佇列位址 |
| 讓訊息寄不出去 |接聽 |任何有效的佇列位址 |
| 取得與訊息佇列工作階段相關聯的 hello 狀態 |接聽 |任何有效的佇列位址 |
| 設定訊息佇列工作階段相關聯的 hello 狀態 |接聽 |任何有效的佇列位址 |
| **主題** | | |
| 建立主題 |管理 |任何命名空間位址 |
| 刪除主題 |管理 |任何有效的主題位址 |
| 列舉主題 |管理 |/$Resources/Topics |
| 取得 hello 主題描述 |管理 |任何有效的主題位址 |
| 設定主題的授權規則 |管理 |任何有效的主題位址 |
| 傳送 toohello 主題 |傳送 |任何有效的主題位址 |
| **訂用帳戶** | | |
| 建立訂閱 |管理 |任何命名空間位址 |
| 刪除訂用帳戶 |管理 |../myTopic/Subscriptions/mySubscription |
| 列舉訂用帳戶 |管理 |../myTopic/Subscriptions |
| 取得訂用帳戶描述 |管理 |../myTopic/Subscriptions/mySubscription |
| 放棄或完成訊息接收 hello 訊息，以查看並鎖定模式之後 |接聽 |../myTopic/Subscriptions/mySubscription |
| 延遲訊息以便稍後擷取 |接聽 |../myTopic/Subscriptions/mySubscription |
| 讓訊息寄不出去 |接聽 |../myTopic/Subscriptions/mySubscription |
| 取得與主題工作階段相關聯的 hello 狀態 |接聽 |../myTopic/Subscriptions/mySubscription |
| 與主題工作階段相關聯的設定 hello 狀態 |接聽 |../myTopic/Subscriptions/mySubscription |
| **規則** | | |
| 建立規則 |管理 |../myTopic/Subscriptions/mySubscription |
| 刪除規則 |管理 |../myTopic/Subscriptions/mySubscription |
| 列舉規則 |管理或接聽 |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>後續步驟

toolearn 有關服務匯流排傳訊的詳細資訊，請參閱下列主題中的 hello。

* [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
* [服務匯流排佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)
* [如何 toouse 服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [如何 toouse Service Bus 主題和訂閱](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com