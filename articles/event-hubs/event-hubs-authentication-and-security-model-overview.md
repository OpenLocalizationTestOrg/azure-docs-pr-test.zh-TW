---
title: "Azure 事件中樞驗證和安全性模型概觀 | Microsoft Docs"
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
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="7aed0-103">事件中樞驗證和安全性模型概觀</span><span class="sxs-lookup"><span data-stu-id="7aed0-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="7aed0-104">Azure 事件中樞安全性模型符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="7aed0-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="7aed0-105">只有出示有效認證的用戶端才能將資料傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7aed0-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="7aed0-106">一個用戶端無法模擬另一個用戶端。</span><span class="sxs-lookup"><span data-stu-id="7aed0-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="7aed0-107">可封鎖惡意用戶端，讓它無法將資料傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7aed0-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="7aed0-108">用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="7aed0-108">Client authentication</span></span>
<span data-ttu-id="7aed0-109">事件中樞安全性模型是以 [共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md) 權杖和「事件發行者」的組合為基礎。</span><span class="sxs-lookup"><span data-stu-id="7aed0-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="7aed0-110">事件發行者會定義事件中樞的虛擬端點。</span><span class="sxs-lookup"><span data-stu-id="7aed0-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="7aed0-111">發行者只能用來將訊息傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7aed0-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="7aed0-112">您無法接收來自發佈者的訊息。</span><span class="sxs-lookup"><span data-stu-id="7aed0-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="7aed0-113">一般而言，事件中樞會針對每個用戶端採用一個發行者。</span><span class="sxs-lookup"><span data-stu-id="7aed0-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="7aed0-114">系統會將傳送到事件中樞之任何發行者的所有訊息，排入該事件中樞內的佇列中。</span><span class="sxs-lookup"><span data-stu-id="7aed0-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="7aed0-115">發行者會啟用更細緻的存取控制和節流。</span><span class="sxs-lookup"><span data-stu-id="7aed0-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="7aed0-116">系統會為每個「事件中樞」用戶端指派一個唯一權杖，該權杖會上傳到用戶端。</span><span class="sxs-lookup"><span data-stu-id="7aed0-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="7aed0-117">權杖的產生機制讓每個唯一權杖都能授與相異唯一發佈者的存取權限。</span><span class="sxs-lookup"><span data-stu-id="7aed0-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="7aed0-118">擁有權杖的用戶端只能傳送到一個發行者，無法再傳送到任何其他發行者。</span><span class="sxs-lookup"><span data-stu-id="7aed0-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="7aed0-119">如果多個用戶端共用同一個權杖，它們每一個就會共用一個發行者。</span><span class="sxs-lookup"><span data-stu-id="7aed0-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="7aed0-120">您可以讓裝置具備可授與事件中樞直接存取權的權杖，不過並不建議這樣做。</span><span class="sxs-lookup"><span data-stu-id="7aed0-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="7aed0-121">任何擁有此權杖的裝置都可以將訊息直接傳送到該事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7aed0-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="7aed0-122">這類裝置將不受節流所約束。</span><span class="sxs-lookup"><span data-stu-id="7aed0-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="7aed0-123">此外，您也無法將這類裝置加入黑名單，以禁止其傳送到該事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7aed0-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="7aed0-124">所有權杖都經過 SAS 金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="7aed0-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="7aed0-125">一般而言，所有權杖都會經過同一個金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="7aed0-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="7aed0-126">用戶端並不知道該金鑰；這可避免其他用戶端製造權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="7aed0-127">建立 SAS 金鑰</span><span class="sxs-lookup"><span data-stu-id="7aed0-127">Create the SAS key</span></span>

<span data-ttu-id="7aed0-128">建立事件中樞命名空間時，此服務會產生名為 **RootManageSharedAccessKey** 的 256 位元 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7aed0-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="7aed0-129">這個金鑰能授與命名空間的傳送、聆聽及管理權限。</span><span class="sxs-lookup"><span data-stu-id="7aed0-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="7aed0-130">您也可以建立額外的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7aed0-130">You can also create additional keys.</span></span> <span data-ttu-id="7aed0-131">建議您產生一個可授與對特定事件中樞之傳送權限的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7aed0-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="7aed0-132">在本主題的其餘部分，假設您將此金鑰命名為 **EventHubSendKey**。</span><span class="sxs-lookup"><span data-stu-id="7aed0-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="7aed0-133">以下範例會在建立事件中樞時，建立一個僅限傳送的金鑰：</span><span class="sxs-lookup"><span data-stu-id="7aed0-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="7aed0-134">產生權杖</span><span class="sxs-lookup"><span data-stu-id="7aed0-134">Generate tokens</span></span>

<span data-ttu-id="7aed0-135">您可以使用 SAS 金鑰來產生權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="7aed0-136">您只能為每個用戶端產生一個權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-136">You must produce only one token per client.</span></span> <span data-ttu-id="7aed0-137">您可以使用下列方法來產生權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="7aed0-138">所有權杖都是以 **EventHubSendKey** 金鑰產生。</span><span class="sxs-lookup"><span data-stu-id="7aed0-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="7aed0-139">每個權杖均有一個指派的唯一 URI。</span><span class="sxs-lookup"><span data-stu-id="7aed0-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="7aed0-140">在呼叫這個方法時，您應該將 URI 指定為 `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`。</span><span class="sxs-lookup"><span data-stu-id="7aed0-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="7aed0-141">此 URI 對所有權杖來說是完全相同的，但 `PUBLISHER_NAME`除外，每個權杖的該項目應該是不同的。</span><span class="sxs-lookup"><span data-stu-id="7aed0-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="7aed0-142">在理想的情況下，`PUBLISHER_NAME` 代表收到該權杖之用戶端的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7aed0-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="7aed0-143">這個方法會產生具有下列結構的權杖：</span><span class="sxs-lookup"><span data-stu-id="7aed0-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="7aed0-144">以秒數為單位指定的權杖到期 (從 1970 年 1 月 1 日 開始)。</span><span class="sxs-lookup"><span data-stu-id="7aed0-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="7aed0-145">以下是權杖的範例：</span><span class="sxs-lookup"><span data-stu-id="7aed0-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="7aed0-146">一般而言，權杖的週期與用戶端的週期相近或更長。</span><span class="sxs-lookup"><span data-stu-id="7aed0-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="7aed0-147">如果用戶端能夠取得新的權杖，就可以使用週期較短的權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="7aed0-148">傳送資料</span><span class="sxs-lookup"><span data-stu-id="7aed0-148">Sending data</span></span>
<span data-ttu-id="7aed0-149">建立權杖之後，系統就會為每個用戶端佈建其自己的唯一權杖。</span><span class="sxs-lookup"><span data-stu-id="7aed0-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="7aed0-150">當用戶端將資料傳送到事件中樞時，會使用權杖標記自己傳送的要求。</span><span class="sxs-lookup"><span data-stu-id="7aed0-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="7aed0-151">為了防止攻擊者竊聽及竊取權杖，用戶端與事件中樞之間的通訊必須透過已加密的通道進行。</span><span class="sxs-lookup"><span data-stu-id="7aed0-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="7aed0-152">將用戶端列入黑名單</span><span class="sxs-lookup"><span data-stu-id="7aed0-152">Blacklisting clients</span></span>
<span data-ttu-id="7aed0-153">如果權杖遭攻擊者竊取，攻擊者便可以模擬權杖遭竊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="7aed0-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="7aed0-154">將用戶端列入黑名單可讓用戶端變成無法使用，直到它收到使用不同發行者的新權杖為止。</span><span class="sxs-lookup"><span data-stu-id="7aed0-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="7aed0-155">後端應用程式的驗證</span><span class="sxs-lookup"><span data-stu-id="7aed0-155">Authentication of back-end applications</span></span>

<span data-ttu-id="7aed0-156">為了驗證取用「事件中樞」用戶端所產生之資料的後端應用程式，「事件中樞」採用一個與「服務匯流排」主題所用模型相似的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="7aed0-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="7aed0-157">事件中樞取用者群組等同於服務匯流排主題的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7aed0-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="7aed0-158">如果建立取用者群組的要求有附帶權杖，而該權杖可授與事件中樞或事件中樞所屬之命名空間的管理權限，用戶端便可以建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="7aed0-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="7aed0-159">如果接收要求有附帶權杖，而該權杖可授與該取用者群組、事件中樞或事件中樞所屬之命名空間的接收權限，用戶端便可以取用來自取用者群組的資料。</span><span class="sxs-lookup"><span data-stu-id="7aed0-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="7aed0-160">目前版本的服務匯流排不支援個別訂用帳戶的 SAS 規則。</span><span class="sxs-lookup"><span data-stu-id="7aed0-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="7aed0-161">相同情況亦適用於事件中樞取用者群組。</span><span class="sxs-lookup"><span data-stu-id="7aed0-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="7aed0-162">我們會在日後將這兩項功能加入 SAS 支援。</span><span class="sxs-lookup"><span data-stu-id="7aed0-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="7aed0-163">由於個別取用者群組的 SAS 驗證不存在，因此您可以使用 SAS 金鑰來保護所有使用相同金鑰的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="7aed0-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="7aed0-164">這個方法可讓應用程式取用來自事件中樞之任何取用者群組的資料。</span><span class="sxs-lookup"><span data-stu-id="7aed0-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7aed0-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7aed0-165">Next steps</span></span>
<span data-ttu-id="7aed0-166">若要深入了解事件中樞，請造訪下列主題：</span><span class="sxs-lookup"><span data-stu-id="7aed0-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="7aed0-167">[事件中樞概觀]</span><span class="sxs-lookup"><span data-stu-id="7aed0-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="7aed0-168">[共用存取簽章的概觀]</span><span class="sxs-lookup"><span data-stu-id="7aed0-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="7aed0-169">[使用事件中樞的範例應用程式]</span><span class="sxs-lookup"><span data-stu-id="7aed0-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="7aed0-170">[事件中樞概觀]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="7aed0-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="7aed0-171">[使用事件中樞的範例應用程式]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="7aed0-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="7aed0-172">[共用存取簽章的概觀]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="7aed0-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

