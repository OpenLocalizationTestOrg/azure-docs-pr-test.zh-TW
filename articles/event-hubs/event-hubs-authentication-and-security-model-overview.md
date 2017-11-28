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
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="979a3-103">事件中樞驗證和安全性模型概觀</span><span class="sxs-lookup"><span data-stu-id="979a3-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="979a3-104">hello Azure 事件中心的安全性模型符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="979a3-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="979a3-105">出示有效認證的唯一用戶端可以傳送資料 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="979a3-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="979a3-106">一個用戶端無法模擬另一個用戶端。</span><span class="sxs-lookup"><span data-stu-id="979a3-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="979a3-107">惡意用戶端可以傳送資料 tooan 事件中樞被封鎖。</span><span class="sxs-lookup"><span data-stu-id="979a3-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="979a3-108">用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="979a3-108">Client authentication</span></span>
<span data-ttu-id="979a3-109">hello 事件中心的安全性模型為基礎的組合[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md)語彙基元和*事件發行者*。</span><span class="sxs-lookup"><span data-stu-id="979a3-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="979a3-110">事件發行者會定義事件中樞的虛擬端點。</span><span class="sxs-lookup"><span data-stu-id="979a3-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="979a3-111">hello 發行者只能使用的 toosend 訊息 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="979a3-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="979a3-112">不可能 tooreceive 從 「 發行者 」 的訊息。</span><span class="sxs-lookup"><span data-stu-id="979a3-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="979a3-113">一般而言，事件中樞會針對每個用戶端採用一個發行者。</span><span class="sxs-lookup"><span data-stu-id="979a3-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="979a3-114">傳送的事件中心的 hello 發行者 tooany 的所有訊息都的佇列該事件中心內。</span><span class="sxs-lookup"><span data-stu-id="979a3-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="979a3-115">發行者會啟用更細緻的存取控制和節流。</span><span class="sxs-lookup"><span data-stu-id="979a3-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="979a3-116">每個事件中心用戶端會指派唯一的語彙基元，是上傳的 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="979a3-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="979a3-117">hello 語彙基元所產生的每個唯一的權杖會授與存取 tooa 不同的唯一發行者。</span><span class="sxs-lookup"><span data-stu-id="979a3-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="979a3-118">擁有權杖的用戶端只能傳送 tooone 發行者上，但沒有其他 「 發行者 」。</span><span class="sxs-lookup"><span data-stu-id="979a3-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="979a3-119">如果多個用戶端共用 hello 相同語彙基元，則每個共用發行者。</span><span class="sxs-lookup"><span data-stu-id="979a3-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="979a3-120">雖然不建議，很可能 tooequip 裝置權杖來授與直接存取 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="979a3-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="979a3-121">任何擁有此權杖的裝置都可以將訊息直接傳送到該事件中樞。</span><span class="sxs-lookup"><span data-stu-id="979a3-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="979a3-122">這類裝置將無法主旨 toothrottling。</span><span class="sxs-lookup"><span data-stu-id="979a3-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="979a3-123">此外，hello 裝置無法列入黑名單中而無法傳送 toothat 事件中心。</span><span class="sxs-lookup"><span data-stu-id="979a3-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="979a3-124">所有權杖都經過 SAS 金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="979a3-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="979a3-125">一般而言，所有權杖都簽署以 hello 相同索引鍵。</span><span class="sxs-lookup"><span data-stu-id="979a3-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="979a3-126">用戶端不會察覺 hello 機碼。這可防止其他用戶端製造權杖。</span><span class="sxs-lookup"><span data-stu-id="979a3-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="979a3-127">建立 hello SAS 金鑰</span><span class="sxs-lookup"><span data-stu-id="979a3-127">Create hello SAS key</span></span>

<span data-ttu-id="979a3-128">Hello 服務時建立事件中樞命名空間，會產生名為 256 位元 SAS 金鑰**RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="979a3-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="979a3-129">這個金鑰授傳送、 接聽及管理 rights toohello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="979a3-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="979a3-130">您也可以建立額外的金鑰。</span><span class="sxs-lookup"><span data-stu-id="979a3-130">You can also create additional keys.</span></span> <span data-ttu-id="979a3-131">建議您產生授權傳送權限 toohello 特定事件中心的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="979a3-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="979a3-132">本主題的 hello 其餘部分，會假設名為此金鑰**EventHubSendKey**。</span><span class="sxs-lookup"><span data-stu-id="979a3-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="979a3-133">下列範例中的 hello 建立 hello 事件中樞時，會建立僅傳送金鑰：</span><span class="sxs-lookup"><span data-stu-id="979a3-133">hello following example creates a send-only key when creating hello event hub:</span></span>

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

### <a name="generate-tokens"></a><span data-ttu-id="979a3-134">產生權杖</span><span class="sxs-lookup"><span data-stu-id="979a3-134">Generate tokens</span></span>

<span data-ttu-id="979a3-135">您可以產生語彙基元使用 hello SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="979a3-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="979a3-136">您只能為每個用戶端產生一個權杖。</span><span class="sxs-lookup"><span data-stu-id="979a3-136">You must produce only one token per client.</span></span> <span data-ttu-id="979a3-137">語彙基元然後可使用下列方法 hello 來產生。</span><span class="sxs-lookup"><span data-stu-id="979a3-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="979a3-138">所有語彙基元使用產生的 hello **EventHubSendKey**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="979a3-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="979a3-139">每個權杖均有一個指派的唯一 URI。</span><span class="sxs-lookup"><span data-stu-id="979a3-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="979a3-140">Hello URI 呼叫此方法時，應該指定為`//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`。</span><span class="sxs-lookup"><span data-stu-id="979a3-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="979a3-141">所有權杖 hello URI 為相同的 hello 例外`PUBLISHER_NAME`，應該針對每個權杖不同。</span><span class="sxs-lookup"><span data-stu-id="979a3-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="979a3-142">在理想情況下，`PUBLISHER_NAME`代表 hello hello 用戶端會接收該語彙基元的識別碼。</span><span class="sxs-lookup"><span data-stu-id="979a3-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="979a3-143">這個方法會產生的語彙基元以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="979a3-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="979a3-144">指定 hello 權杖到期時間的秒數從 1970 年 1 月 1 日。</span><span class="sxs-lookup"><span data-stu-id="979a3-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="979a3-145">hello 以下是語彙基元的範例：</span><span class="sxs-lookup"><span data-stu-id="979a3-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="979a3-146">一般來說，hello 權杖具有類似或超過 hello 用戶端 hello 壽命的使用期限。</span><span class="sxs-lookup"><span data-stu-id="979a3-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="979a3-147">如果 hello 用戶端 hello 功能 tooobtain 新的權杖，可以使用具有較短使用期限的權杖。</span><span class="sxs-lookup"><span data-stu-id="979a3-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="979a3-148">傳送資料</span><span class="sxs-lookup"><span data-stu-id="979a3-148">Sending data</span></span>
<span data-ttu-id="979a3-149">一旦已建立 hello 語彙基元，每個用戶端的佈建與它自己唯一的權杖。</span><span class="sxs-lookup"><span data-stu-id="979a3-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="979a3-150">當 hello 用戶端會將資料傳送到事件中心時，它會標記其傳送要求和 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="979a3-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="979a3-151">tooprevent 攻擊者竊聽並竊取權杖 hello、 hello hello 用戶端與 hello 事件中心之間的通訊必須透過加密通道進行。</span><span class="sxs-lookup"><span data-stu-id="979a3-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="979a3-152">將用戶端列入黑名單</span><span class="sxs-lookup"><span data-stu-id="979a3-152">Blacklisting clients</span></span>
<span data-ttu-id="979a3-153">如果攻擊者竊取權杖，hello 攻擊者可以模擬 hello 用戶端遭到竊取的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="979a3-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="979a3-154">將用戶端列入黑名單可讓用戶端變成無法使用，直到它收到使用不同發行者的新權杖為止。</span><span class="sxs-lookup"><span data-stu-id="979a3-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="979a3-155">後端應用程式的驗證</span><span class="sxs-lookup"><span data-stu-id="979a3-155">Authentication of back-end applications</span></span>

<span data-ttu-id="979a3-156">使用事件中心用戶端，事件中心所產生的 hello 資料 tooauthenticate 後端應用程式採用是用於服務匯流排主題類似 toohello 模型的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="979a3-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="979a3-157">事件中心取用者群組是相等的 tooa 訂用帳戶 tooa 服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="979a3-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="979a3-158">如果 hello 要求 toocreate hello 取用者群組伴隨著授與管理 hello 事件中心的權限，或如 hello 命名空間 toowhich hello 事件中心所屬的語彙基元，用戶端可以建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="979a3-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="979a3-159">Tooconsume 資料取用者群組從如果 hello 接收要求伴隨著權杖，授權接收該取用者群組上的權限，hello 事件中心或 hello 命名空間 toowhich hello 事件中心所屬允許用戶端。</span><span class="sxs-lookup"><span data-stu-id="979a3-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="979a3-160">hello 的服務匯流排的目前版本不支援個別訂閱的 SAS 規則。</span><span class="sxs-lookup"><span data-stu-id="979a3-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="979a3-161">hello 同樣適用於事件中樞取用者群組。</span><span class="sxs-lookup"><span data-stu-id="979a3-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="979a3-162">這兩個功能中 hello 未來將加入 SAS 支援。</span><span class="sxs-lookup"><span data-stu-id="979a3-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="979a3-163">在 hello 沒有個別取用者群組的 SAS 驗證，您可以使用 SAS 金鑰 toosecure 所有取用者群組具有共同索引鍵。</span><span class="sxs-lookup"><span data-stu-id="979a3-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="979a3-164">這個方法可讓應用程式 tooconsume 資料，從任何 hello 事件中心取用者群組。</span><span class="sxs-lookup"><span data-stu-id="979a3-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="979a3-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="979a3-165">Next steps</span></span>
<span data-ttu-id="979a3-166">深入了解事件中心 toolearn 造訪 hello 下列主題：</span><span class="sxs-lookup"><span data-stu-id="979a3-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="979a3-167">[事件中樞概觀]</span><span class="sxs-lookup"><span data-stu-id="979a3-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="979a3-168">[共用存取簽章的概觀]</span><span class="sxs-lookup"><span data-stu-id="979a3-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="979a3-169">[使用事件中樞的範例應用程式]</span><span class="sxs-lookup"><span data-stu-id="979a3-169">[Sample applications that use Event Hubs]</span></span>

[事件中樞概觀]: event-hubs-what-is-event-hubs.md
[使用事件中樞的範例應用程式]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[共用存取簽章的概觀]: ../service-bus-messaging/service-bus-sas.md

