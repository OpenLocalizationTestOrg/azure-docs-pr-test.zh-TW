---
title: "Azure 事件中心驗證和安全性模型的 aaaOverview |Microsoft 文件"
description: "事件中樞驗證和安全性模型概觀。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>事件中樞驗證和安全性模型概觀
hello Azure 事件中心的安全性模型符合下列需求的 hello:

* 出示有效認證的唯一用戶端可以傳送資料 tooan 事件中心。
* 一個用戶端無法模擬另一個用戶端。
* 惡意用戶端可以傳送資料 tooan 事件中樞被封鎖。

## <a name="client-authentication"></a>用戶端驗證
hello 事件中心的安全性模型為基礎的組合[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md)語彙基元和*事件發行者*。 事件發行者會定義事件中樞的虛擬端點。 hello 發行者只能使用的 toosend 訊息 tooan 事件中心。 不可能 tooreceive 從 「 發行者 」 的訊息。

一般而言，事件中樞會針對每個用戶端採用一個發行者。 傳送的事件中心的 hello 發行者 tooany 的所有訊息都的佇列該事件中心內。 發行者會啟用更細緻的存取控制和節流。

每個事件中心用戶端會指派唯一的語彙基元，是上傳的 toohello 用戶端。 hello 語彙基元所產生的每個唯一的權杖會授與存取 tooa 不同的唯一發行者。 擁有權杖的用戶端只能傳送 tooone 發行者上，但沒有其他 「 發行者 」。 如果多個用戶端共用 hello 相同語彙基元，則每個共用發行者。

雖然不建議，很可能 tooequip 裝置權杖來授與直接存取 tooan 事件中心。 任何擁有此權杖的裝置都可以將訊息直接傳送到該事件中樞。 這類裝置將無法主旨 toothrottling。 此外，hello 裝置無法列入黑名單中而無法傳送 toothat 事件中心。

所有權杖都經過 SAS 金鑰簽署。 一般而言，所有權杖都簽署以 hello 相同索引鍵。 用戶端不會察覺 hello 機碼。這可防止其他用戶端製造權杖。

### <a name="create-hello-sas-key"></a>建立 hello SAS 金鑰

Hello 服務時建立事件中樞命名空間，會產生名為 256 位元 SAS 金鑰**RootManageSharedAccessKey**。 這個金鑰授傳送、 接聽及管理 rights toohello 命名空間。 您也可以建立額外的金鑰。 建議您產生授權傳送權限 toohello 特定事件中心的索引鍵。 本主題的 hello 其餘部分，會假設名為此金鑰**EventHubSendKey**。

下列範例中的 hello 建立 hello 事件中樞時，會建立僅傳送金鑰：

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>產生權杖

您可以產生語彙基元使用 hello SAS 金鑰。 您只能為每個用戶端產生一個權杖。 語彙基元然後可使用下列方法 hello 來產生。 所有語彙基元使用產生的 hello **EventHubSendKey**索引鍵。 每個權杖均有一個指派的唯一 URI。

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Hello URI 呼叫此方法時，應該指定為`//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`。 所有權杖 hello URI 為相同的 hello 例外`PUBLISHER_NAME`，應該針對每個權杖不同。 在理想情況下，`PUBLISHER_NAME`代表 hello hello 用戶端會接收該語彙基元的識別碼。

這個方法會產生的語彙基元以 hello 下列結構：

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

指定 hello 權杖到期時間的秒數從 1970 年 1 月 1 日。 hello 以下是語彙基元的範例：

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

一般來說，hello 權杖具有類似或超過 hello 用戶端 hello 壽命的使用期限。 如果 hello 用戶端 hello 功能 tooobtain 新的權杖，可以使用具有較短使用期限的權杖。

### <a name="sending-data"></a>傳送資料
一旦已建立 hello 語彙基元，每個用戶端的佈建與它自己唯一的權杖。

當 hello 用戶端會將資料傳送到事件中心時，它會標記其傳送要求和 hello 語彙基元。 tooprevent 攻擊者竊聽並竊取權杖 hello、 hello hello 用戶端與 hello 事件中心之間的通訊必須透過加密通道進行。

### <a name="blacklisting-clients"></a>將用戶端列入黑名單
如果攻擊者竊取權杖，hello 攻擊者可以模擬 hello 用戶端遭到竊取的語彙基元。 將用戶端列入黑名單可讓用戶端變成無法使用，直到它收到使用不同發行者的新權杖為止。

## <a name="authentication-of-back-end-applications"></a>後端應用程式的驗證

使用事件中心用戶端，事件中心所產生的 hello 資料 tooauthenticate 後端應用程式採用是用於服務匯流排主題類似 toohello 模型的安全性模型。 事件中心取用者群組是相等的 tooa 訂用帳戶 tooa 服務匯流排主題。 如果 hello 要求 toocreate hello 取用者群組伴隨著授與管理 hello 事件中心的權限，或如 hello 命名空間 toowhich hello 事件中心所屬的語彙基元，用戶端可以建立取用者群組。 Tooconsume 資料取用者群組從如果 hello 接收要求伴隨著權杖，授權接收該取用者群組上的權限，hello 事件中心或 hello 命名空間 toowhich hello 事件中心所屬允許用戶端。

hello 的服務匯流排的目前版本不支援個別訂閱的 SAS 規則。 hello 同樣適用於事件中樞取用者群組。 這兩個功能中 hello 未來將加入 SAS 支援。

在 hello 沒有個別取用者群組的 SAS 驗證，您可以使用 SAS 金鑰 toosecure 所有取用者群組具有共同索引鍵。 這個方法可讓應用程式 tooconsume 資料，從任何 hello 事件中心取用者群組。

## <a name="next-steps"></a>後續步驟
深入了解事件中心 toolearn 造訪 hello 下列主題：

* [事件中樞概觀]
* [共用存取簽章的概觀]
* [使用事件中樞的範例應用程式]

[事件中樞概觀]: event-hubs-what-is-event-hubs.md
[使用事件中樞的範例應用程式]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[共用存取簽章的概觀]: ../service-bus-messaging/service-bus-sas.md

