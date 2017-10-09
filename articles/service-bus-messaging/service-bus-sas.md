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
# <a name="service-bus-authentication-with-shared-access-signatures"></a><span data-ttu-id="997ec-103">使用共用存取簽章的服務匯流排驗證</span><span class="sxs-lookup"><span data-stu-id="997ec-103">Service Bus authentication with Shared Access Signatures</span></span>

<span data-ttu-id="997ec-104">*共用存取簽章*(SAS) 是服務匯流排傳訊 hello 主要安全性機制。</span><span class="sxs-lookup"><span data-stu-id="997ec-104">*Shared Access Signatures* (SAS) are hello primary security mechanism for Service Bus messaging.</span></span> <span data-ttu-id="997ec-105">這篇文章討論 SAS，其運作方式以及 toouse 它們無從驗證平台的方式。</span><span class="sxs-lookup"><span data-stu-id="997ec-105">This article discusses SAS, how they work, and how toouse them in a platform-agnostic way.</span></span>

<span data-ttu-id="997ec-106">SAS 驗證可讓應用程式 tooauthenticate tooService 匯流排使用傳訊實體 （佇列或主題） 的特定權限相關聯的 hello 或 hello 命名空間上設定的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-106">SAS authentication enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="997ec-107">然後，您可以使用此索引鍵 toogenerate 用戶端可以接著使用 tooauthenticate tooService 匯流排 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-107">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="997ec-108">SAS 驗證支援包含在 hello Azure SDK 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="997ec-108">SAS authentication support is included in hello Azure SDK version 2.0 and later.</span></span>

## <a name="overview-of-sas"></a><span data-ttu-id="997ec-109">SAS 的概觀</span><span class="sxs-lookup"><span data-stu-id="997ec-109">Overview of SAS</span></span>

<span data-ttu-id="997ec-110">共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="997ec-110">Shared Access Signatures are an authentication mechanism based on SHA-256 secure hashes or URIs.</span></span> <span data-ttu-id="997ec-111">SAS 是所有服務匯流排服務使用的非常強大的機制。</span><span class="sxs-lookup"><span data-stu-id="997ec-111">SAS is an extremely powerful mechanism that is used by all Service Bus services.</span></span> <span data-ttu-id="997ec-112">在實際使用中，SAS 有兩個元件：「共用存取原則」和「共用存取簽章」(通常稱為「權杖」)。</span><span class="sxs-lookup"><span data-stu-id="997ec-112">In actual use, SAS has two components: a *shared access policy* and a *Shared Access Signature* (often called a *token*).</span></span>

<span data-ttu-id="997ec-113">服務匯流排中的 SAS 驗證包括 hello 組態與服務匯流排資源上的權限相關聯的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-113">SAS authentication in Service Bus involves hello configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="997ec-114">用戶端的宣告存取 tooService 匯流排資源所呈現 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-114">Clients claim access tooService Bus resources by presenting a SAS token.</span></span> <span data-ttu-id="997ec-115">這個語彙基元組成 hello 資源所存取的 URI，以 hello 簽章的到期設定索引鍵。</span><span class="sxs-lookup"><span data-stu-id="997ec-115">This token consists of hello resource URI being accessed, and an expiry signed with hello configured key.</span></span>

<span data-ttu-id="997ec-116">您可以在服務匯流排[轉送](service-bus-fundamentals-hybrid-solutions.md#relays)、[佇列](service-bus-fundamentals-hybrid-solutions.md#queues)和[主題](service-bus-fundamentals-hybrid-solutions.md#topics)上設定共用存取簽章授權規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-116">You can configure Shared Access Signature authorization rules on Service Bus [relays](service-bus-fundamentals-hybrid-solutions.md#relays), [queues](service-bus-fundamentals-hybrid-solutions.md#queues), and [topics](service-bus-fundamentals-hybrid-solutions.md#topics).</span></span>

<span data-ttu-id="997ec-117">SAS 驗證會使用下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="997ec-117">SAS authentication uses hello following elements:</span></span>

* <span data-ttu-id="997ec-118">[共用存取授權規則](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)︰Base64 表示法中的 256 位元主要密碼編譯金鑰、選用的次要金鑰以及金鑰名稱和相關權限 (接聽、傳送或管理權限的集合)。</span><span class="sxs-lookup"><span data-stu-id="997ec-118">[Shared Access authorization rule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256-bit primary cryptographic key in Base64 representation, an optional secondary key, and a key name and associated rights (a collection of *Listen*, *Send*, or *Manage* rights).</span></span>
* <span data-ttu-id="997ec-119">[共用存取簽章](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider)語彙基元： 產生 hello hmac-sha256 的資源，所組成的字串 hello hello 所存取之資源的 URI、 過期以及使用 hello 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-119">[Shared Access Signature](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: Generated using hello HMAC-SHA256 of a resource string, consisting of hello URI of hello resource that is accessed and an expiry, with hello cryptographic key.</span></span> <span data-ttu-id="997ec-120">hello 簽章與 hello 下列各節中所述的其他項目會被格式化成字串 tooform hello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-120">hello signature and other elements described in hello following sections are formatted into a string tooform hello SAS token.</span></span>

## <a name="shared-access-policy"></a><span data-ttu-id="997ec-121">共用存取原則</span><span class="sxs-lookup"><span data-stu-id="997ec-121">Shared access policy</span></span>

<span data-ttu-id="997ec-122">需 SAS 的重點 toounderstand 是啟動與原則。</span><span class="sxs-lookup"><span data-stu-id="997ec-122">An important thing toounderstand about SAS is that it starts with a policy.</span></span> <span data-ttu-id="997ec-123">針對每個原則，您會決定三段資訊：**名稱**、**範圍**和**權限**。</span><span class="sxs-lookup"><span data-stu-id="997ec-123">For each policy, you decide on three pieces of information: **name**, **scope**, and **permissions**.</span></span> <span data-ttu-id="997ec-124">hello**名稱**僅是; 該範圍內的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="997ec-124">hello **name** is just that; a unique name within that scope.</span></span> <span data-ttu-id="997ec-125">hello 範圍也很簡單： 其 hello hello 資源有問題的 URI。</span><span class="sxs-lookup"><span data-stu-id="997ec-125">hello scope is easy enough: it's hello URI of hello resource in question.</span></span> <span data-ttu-id="997ec-126">服務匯流排命名空間 hello 範圍是 hello 完整的網域名稱 (FQDN)，例如`https://<yournamespace>.servicebus.windows.net/`。</span><span class="sxs-lookup"><span data-stu-id="997ec-126">For a Service Bus namespace, hello scope is hello fully qualified domain name (FQDN), such as `https://<yournamespace>.servicebus.windows.net/`.</span></span>

<span data-ttu-id="997ec-127">大部分一目了然 hello 可用權限的原則︰</span><span class="sxs-lookup"><span data-stu-id="997ec-127">hello available permissions for a policy are largely self-explanatory:</span></span>

* <span data-ttu-id="997ec-128">傳送</span><span class="sxs-lookup"><span data-stu-id="997ec-128">Send</span></span>
* <span data-ttu-id="997ec-129">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-129">Listen</span></span>
* <span data-ttu-id="997ec-130">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-130">Manage</span></span>

<span data-ttu-id="997ec-131">建立 hello 原則之後，它指派*主索引鍵*和*次要金鑰*。</span><span class="sxs-lookup"><span data-stu-id="997ec-131">After you create hello policy, it is assigned a *Primary Key* and a *Secondary Key*.</span></span> <span data-ttu-id="997ec-132">這些是密碼編譯增強式金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-132">These are cryptographically strong keys.</span></span> <span data-ttu-id="997ec-133">不會失去它們，或遺漏它們-它們永遠都可在 hello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="997ec-133">Don't lose them or leak them - they'll always be available in hello [Azure portal][Azure portal].</span></span> <span data-ttu-id="997ec-134">您可以使用其中一個 hello 產生金鑰，您可以隨時重新產生它們。</span><span class="sxs-lookup"><span data-stu-id="997ec-134">You can use either of hello generated keys, and you can regenerate them at any time.</span></span> <span data-ttu-id="997ec-135">不過，如果您重新產生，或變更 hello hello 原則中的主索引鍵，從它建立任何共用存取簽章將會失效。</span><span class="sxs-lookup"><span data-stu-id="997ec-135">However, if you regenerate or change hello primary key in hello policy, any Shared Access Signatures created from it will be invalidated.</span></span>

<span data-ttu-id="997ec-136">當您建立服務匯流排命名空間時，稱為 hello 整個命名空間會自動建立的原則**RootManageSharedAccessKey**，而且此原則有所有的權限。</span><span class="sxs-lookup"><span data-stu-id="997ec-136">When you create a Service Bus namespace, a policy is automatically created for hello entire namespace called **RootManageSharedAccessKey**, and this policy has all permissions.</span></span> <span data-ttu-id="997ec-137">您未以 **root** 登入，所以除非有適合的理由，請勿使用此原則。</span><span class="sxs-lookup"><span data-stu-id="997ec-137">You don't log on as **root**, so don't use this policy unless there's a really good reason.</span></span> <span data-ttu-id="997ec-138">您可以建立額外的原則中 hello**設定**hello hello 入口網站中的命名空間的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="997ec-138">You can create additional policies in hello **Configure** tab for hello namespace in hello portal.</span></span> <span data-ttu-id="997ec-139">向上 too12 附加 tooit 只能有單一樹狀結構中的層級 （命名空間、 佇列等） 的服務匯流排的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="997ec-139">It's important toonote that a single tree level in Service Bus (namespace, queue, etc.) can only have up too12 policies attached tooit.</span></span>

## <a name="configuration-for-shared-access-signature-authentication"></a><span data-ttu-id="997ec-140">共用存取簽章驗證的設定</span><span class="sxs-lookup"><span data-stu-id="997ec-140">Configuration for Shared Access Signature authentication</span></span>
<span data-ttu-id="997ec-141">您可以設定 hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)服務匯流排命名空間、 佇列或主題上的規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-141">You can configure hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) rule on Service Bus namespaces, queues, or topics.</span></span> <span data-ttu-id="997ec-142">設定[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)服務匯流排訂用帳戶目前不支援，但是您可以使用命名空間或主題 toosecure 存取 toosubscriptions 上設定的規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-142">Configuring a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) on a Service Bus subscription is currently not supported, but you can use rules configured on a namespace or topic toosecure access toosubscriptions.</span></span> <span data-ttu-id="997ec-143">說明此程序的工作範例，請參閱 hello[搭配 Servicebus 訂閱使用共用存取簽章 (SAS) 驗證](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c)範例。</span><span class="sxs-lookup"><span data-stu-id="997ec-143">For a working sample that illustrates this procedure, see hello [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) sample.</span></span>

<span data-ttu-id="997ec-144">在服務匯流排命名空間、佇列或主題上最多可以設定 12 條這類規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-144">A maximum of 12 such rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="997ec-145">服務匯流排命名空間所設定的規則適用於該命名空間中的 tooall 實體。</span><span class="sxs-lookup"><span data-stu-id="997ec-145">Rules that are configured on a Service Bus namespace apply tooall entities in that namespace.</span></span>

![SAS](./media/service-bus-sas/service-bus-namespace.png)

<span data-ttu-id="997ec-147">在此圖中，hello *manageRuleNS*， *sendRuleNS*，和*listenRuleNS*授權規則套用 tooboth 佇列 Q1 和主題 T1，而*listenRuleQ*和*sendRuleQ*套用 tooqueue Q1 和*sendRuleT*適用於 tootopic T1。</span><span class="sxs-lookup"><span data-stu-id="997ec-147">In this figure, hello *manageRuleNS*, *sendRuleNS*, and *listenRuleNS* authorization rules apply tooboth queue Q1 and topic T1, while *listenRuleQ* and *sendRuleQ* apply only tooqueue Q1 and *sendRuleT* applies only tootopic T1.</span></span>

<span data-ttu-id="997ec-148">hello 的索引鍵參數[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)如下：</span><span class="sxs-lookup"><span data-stu-id="997ec-148">hello key parameters of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) are as follows:</span></span>

| <span data-ttu-id="997ec-149">參數</span><span class="sxs-lookup"><span data-stu-id="997ec-149">Parameter</span></span> | <span data-ttu-id="997ec-150">說明</span><span class="sxs-lookup"><span data-stu-id="997ec-150">Description</span></span> |
| --- | --- |
| <span data-ttu-id="997ec-151">*KeyName*</span><span class="sxs-lookup"><span data-stu-id="997ec-151">*KeyName*</span></span> |<span data-ttu-id="997ec-152">描述 hello 授權規則的字串。</span><span class="sxs-lookup"><span data-stu-id="997ec-152">A string that describes hello authorization rule.</span></span> |
| <span data-ttu-id="997ec-153">*PrimaryKey*</span><span class="sxs-lookup"><span data-stu-id="997ec-153">*PrimaryKey*</span></span> |<span data-ttu-id="997ec-154">Base64 編碼 256 位元主要金鑰來簽署和驗證 hello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-154">A base64-encoded 256-bit primary key for signing and validating hello SAS token.</span></span> |
| <span data-ttu-id="997ec-155">*SecondaryKey*</span><span class="sxs-lookup"><span data-stu-id="997ec-155">*SecondaryKey*</span></span> |<span data-ttu-id="997ec-156">Base64 編碼 256 位元次要金鑰來簽署和驗證 hello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-156">A base64-encoded 256-bit secondary key for signing and validating hello SAS token.</span></span> |
| <span data-ttu-id="997ec-157">*AccessRights*</span><span class="sxs-lookup"><span data-stu-id="997ec-157">*AccessRights*</span></span> |<span data-ttu-id="997ec-158">Hello 授權規則授與的存取權限清單。</span><span class="sxs-lookup"><span data-stu-id="997ec-158">A list of access rights granted by hello authorization rule.</span></span> <span data-ttu-id="997ec-159">這些權限可以是任何接聽、傳送和管理權限的集合。</span><span class="sxs-lookup"><span data-stu-id="997ec-159">These rights can be any collection of Listen, Send, and Manage rights.</span></span> |

<span data-ttu-id="997ec-160">服務匯流排命名空間是佈建， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)，與[KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName)設定得**RootManageSharedAccessKey**，預設會建立。</span><span class="sxs-lookup"><span data-stu-id="997ec-160">When a Service Bus namespace is provisioned, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), with [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) set too**RootManageSharedAccessKey**, is created by default.</span></span>

## <a name="generate-a-shared-access-signature-token"></a><span data-ttu-id="997ec-161">產生共用存取簽章 (權杖)</span><span class="sxs-lookup"><span data-stu-id="997ec-161">Generate a Shared Access Signature (token)</span></span>

<span data-ttu-id="997ec-162">hello 原則本身不是服務匯流排的 hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-162">hello policy itself is not hello access token for Service Bus.</span></span> <span data-ttu-id="997ec-163">它是 hello 物件的 hello 存取權杖以產生-使用任一 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-163">It is hello object from which hello access token is generated - using either hello primary or secondary key.</span></span> <span data-ttu-id="997ec-164">已簽署 hello 共用的存取授權規則中指定的金鑰存取 toohello 任何用戶端可能會產生 hello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-164">Any client that has access toohello signing keys specified in hello shared access authorization rule can generate hello SAS token.</span></span> <span data-ttu-id="997ec-165">請仔細製作 hello 遵循格式字串所產生 hello 語彙基元：</span><span class="sxs-lookup"><span data-stu-id="997ec-165">hello token is generated by carefully crafting a string in hello following format:</span></span>

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

<span data-ttu-id="997ec-166">其中`signature-string`hello hello 語彙基元範圍 hello sha-256 雜湊 (**範圍**hello 上一節中所述) CRLF，附加與到期時間 (以秒為單位 hello 新紀元以來的： `00:00:00 UTC` 1 年 1 月從 1970)。</span><span class="sxs-lookup"><span data-stu-id="997ec-166">Where `signature-string` is hello SHA-256 hash of hello scope of hello token (**scope** as described in hello previous section) with a CRLF appended and an expiry time (in seconds since hello epoch: `00:00:00 UTC` on 1 January 1970).</span></span> 

> [!NOTE]
> <span data-ttu-id="997ec-167">tooavoid 簡短權杖到期時間，建議您為至少為 32 位元不帶正負號的整數，或最好是長時間 （64 位元） 整數編碼 hello 到期時間值。</span><span class="sxs-lookup"><span data-stu-id="997ec-167">tooavoid a short token expiry time, it is recommended that you encode hello expiry time value as at least a 32-bit unsigned integer, or preferably a long (64-bit) integer.</span></span>  
> 
> 

<span data-ttu-id="997ec-168">hello 雜湊看起來類似 toohello 下列虛擬程式碼，並傳回 32 個位元組。</span><span class="sxs-lookup"><span data-stu-id="997ec-168">hello hash looks similar toohello following pseudo code and returns 32 bytes.</span></span>

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

<span data-ttu-id="997ec-169">hello 非雜湊值如下所示 hello **SharedAccessSignature**以便 hello 收件者可以計算出 hello 雜湊的字串 hello 與相同的參數，確認它傳回 toobe hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="997ec-169">hello non-hashed values are in hello **SharedAccessSignature** string so that hello recipient can compute hello hash with hello same parameters, toobe sure that it returns hello same result.</span></span> <span data-ttu-id="997ec-170">hello URI 指定 hello 範圍和 hello 索引鍵名稱識別 hello 原則使用 toobe toocompute hello 雜湊。</span><span class="sxs-lookup"><span data-stu-id="997ec-170">hello URI specifies hello scope, and hello key name identifies hello policy toobe used toocompute hello hash.</span></span> <span data-ttu-id="997ec-171">從安全性的觀點而言，這很重要。</span><span class="sxs-lookup"><span data-stu-id="997ec-171">This is important from a security standpoint.</span></span> <span data-ttu-id="997ec-172">如果 hello 簽章不符合哪些 hello 收件者 (Service Bus) 計算的則會拒絕存取。</span><span class="sxs-lookup"><span data-stu-id="997ec-172">If hello signature doesn't match that which hello recipient (Service Bus) calculates, then access is denied.</span></span> <span data-ttu-id="997ec-173">此時您可以確定該 hello 寄件者有存取 toohello 金鑰，應該被授與 hello hello 原則中指定的權限。</span><span class="sxs-lookup"><span data-stu-id="997ec-173">At this point you can be sure that hello sender had access toohello key and should be granted hello rights specified in hello policy.</span></span>

<span data-ttu-id="997ec-174">請注意，您應該使用 hello 編碼這項作業的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="997ec-174">Note that you should use hello encoded resource URI for this operation.</span></span> <span data-ttu-id="997ec-175">hello 資源 URI 為 hello Service Bus toowhich 存取資源的完整 URI 宣告的 hello。</span><span class="sxs-lookup"><span data-stu-id="997ec-175">hello resource URI is hello full URI of hello Service Bus resource toowhich access is claimed.</span></span> <span data-ttu-id="997ec-176">例如，`http://<namespace>.servicebus.windows.net/<entityPath>` 或 `sb://<namespace>.servicebus.windows.net/<entityPath>`；也就是 `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`。</span><span class="sxs-lookup"><span data-stu-id="997ec-176">For example, `http://<namespace>.servicebus.windows.net/<entityPath>` or `sb://<namespace>.servicebus.windows.net/<entityPath>`; that is, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.</span></span>

<span data-ttu-id="997ec-177">必須指定此 URI，或其中一個階層上層的 hello 實體上設定 hello 用於簽章的共用的存取授權規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-177">hello shared access authorization rule used for signing must be configured on hello entity specified by this URI, or by one of its hierarchical parents.</span></span> <span data-ttu-id="997ec-178">例如，`http://contoso.servicebus.windows.net/contosoTopics/T1`或`http://contoso.servicebus.windows.net`hello 前一個範例中。</span><span class="sxs-lookup"><span data-stu-id="997ec-178">For example, `http://contoso.servicebus.windows.net/contosoTopics/T1` or `http://contoso.servicebus.windows.net` in hello previous example.</span></span>

<span data-ttu-id="997ec-179">SAS 權杖的有效 hello 下所有資源`<resourceURI>`用於 hello `signature-string`。</span><span class="sxs-lookup"><span data-stu-id="997ec-179">A SAS token is valid for all resources under hello `<resourceURI>` used in hello `signature-string`.</span></span>

<span data-ttu-id="997ec-180">hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName)在 hello SAS 權杖是指 toohello **keyName** hello 的共用的存取授權規則使用 toogenerate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="997ec-180">hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) in hello SAS token refers toohello **keyName** of hello shared access authorization rule used toogenerate hello token.</span></span>

<span data-ttu-id="997ec-181">hello *URL 編碼 resourceURI*必須是 hello 與 hello hello 計算 hello 簽章期間用於 hello 字串簽章 URI 相同。</span><span class="sxs-lookup"><span data-stu-id="997ec-181">hello *URL-encoded-resourceURI* must be hello same as hello URI used in hello string-to-sign during hello computation of hello signature.</span></span> <span data-ttu-id="997ec-182">它應該是 [百分比編碼](https://msdn.microsoft.com/library/4fkewx0t.aspx)。</span><span class="sxs-lookup"><span data-stu-id="997ec-182">It should be [percent-encoded](https://msdn.microsoft.com/library/4fkewx0t.aspx).</span></span>

<span data-ttu-id="997ec-183">建議您定期重新產生用於 hello 的 hello 金鑰[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件。</span><span class="sxs-lookup"><span data-stu-id="997ec-183">It is recommended that you periodically regenerate hello keys used in hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object.</span></span> <span data-ttu-id="997ec-184">應用程式，通常應該使用 hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-184">Applications should generally use hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate a SAS token.</span></span> <span data-ttu-id="997ec-185">當重新產生 hello 金鑰，您應該取代 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) hello 舊主要金鑰，並產生新的金鑰為 hello 新主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="997ec-185">When regenerating hello keys, you should replace hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) with hello old primary key, and generate a new key as hello new primary key.</span></span> <span data-ttu-id="997ec-186">這可讓您 toocontinue 使用 token 簽發 hello 舊的主索引鍵和，有尚未到期的授權。</span><span class="sxs-lookup"><span data-stu-id="997ec-186">This enables you toocontinue using tokens for authorization that were issued with hello old primary key, and that have not yet expired.</span></span>

<span data-ttu-id="997ec-187">如果金鑰被盜，而且您有 toorevoke hello 索引鍵，您可以重新產生兩個 hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey)和 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey)的[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)，請將其取代為新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-187">If a key is compromised and you have toorevoke hello keys, you can regenerate both hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) and hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), replacing them with new keys.</span></span> <span data-ttu-id="997ec-188">此程序會認證所有與 hello 舊金鑰簽章的權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-188">This procedure invalidates all tokens signed with hello old keys.</span></span>

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a><span data-ttu-id="997ec-189">如何使用服務匯流排 toouse 共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="997ec-189">How toouse Shared Access Signature authentication with Service Bus</span></span>

<span data-ttu-id="997ec-190">下列案例的 hello 包括授權規則的設定、 產生 SAS 權杖，以及用戶端授權。</span><span class="sxs-lookup"><span data-stu-id="997ec-190">hello following scenarios include configuration of authorization rules, generation of SAS tokens, and client authorization.</span></span>

<span data-ttu-id="997ec-191">完整的說明 hello 設定和使用 SAS 授權的服務匯流排應用程式的工作範例，請參閱[使用服務匯流排的共用存取簽章驗證](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8)。</span><span class="sxs-lookup"><span data-stu-id="997ec-191">For a full working sample of a Service Bus application that illustrates hello configuration and uses SAS authorization, see [Shared Access Signature authentication with Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8).</span></span> <span data-ttu-id="997ec-192">這裡會提供相關的範例，說明如何使用命名空間或主題 toosecure 服務匯流排訂用帳戶上設定 SAS 授權規則 hello:[搭配 Servicebus 訂閱使用共用存取簽章 (SAS) 驗證](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).</span><span class="sxs-lookup"><span data-stu-id="997ec-192">A related sample that illustrates hello use of SAS authorization rules configured on namespaces or topics toosecure Service Bus subscriptions is available here: [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).</span></span>

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a><span data-ttu-id="997ec-193">存取命名空間上的共用存取授權規則</span><span class="sxs-lookup"><span data-stu-id="997ec-193">Access Shared Access Authorization rules on a namespace</span></span>

<span data-ttu-id="997ec-194">Hello 服務匯流排命名空間根目錄上的作業需要憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="997ec-194">Operations on hello Service Bus namespace root require certificate authentication.</span></span> <span data-ttu-id="997ec-195">您必須針對您的 Azure 訂用帳戶上傳管理憑證。</span><span class="sxs-lookup"><span data-stu-id="997ec-195">You must upload a management certificate for your Azure subscription.</span></span> <span data-ttu-id="997ec-196">tooupload 管理憑證，請依照下列步驟 hello[這裡](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate)，使用 hello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="997ec-196">tooupload a management certificate, follow hello steps [here](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), using hello [Azure portal][Azure portal].</span></span> <span data-ttu-id="997ec-197">如需有關 Azure 管理憑證的詳細資訊，請參閱 hello [Azure 憑證概觀](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates)。</span><span class="sxs-lookup"><span data-stu-id="997ec-197">For more information about Azure management certificates, see hello [Azure certificates overview](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="997ec-198">用於存取服務匯流排命名空間上的共用的存取授權規則的 hello 端點如下所示：</span><span class="sxs-lookup"><span data-stu-id="997ec-198">hello endpoint for accessing shared access authorization rules on a Service Bus namespace is as follows:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

<span data-ttu-id="997ec-199">toocreate [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件上的服務匯流排命名空間，請執行此端點上的 POST 作業具有序列化為 JSON 或 XML hello 規則資訊。</span><span class="sxs-lookup"><span data-stu-id="997ec-199">toocreate a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Service Bus namespace, execute a POST operation on this endpoint with hello rule information serialized as JSON or XML.</span></span> <span data-ttu-id="997ec-200">例如：</span><span class="sxs-lookup"><span data-stu-id="997ec-200">For example:</span></span>

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

<span data-ttu-id="997ec-201">同樣地，使用 hello 端點 tooread hello 授權規則 hello 命名空間上設定的 「 取得 」 作業。</span><span class="sxs-lookup"><span data-stu-id="997ec-201">Similarly, use a GET operation on hello endpoint tooread hello authorization rules configured on hello namespace.</span></span>

<span data-ttu-id="997ec-202">tooupdate 或刪除特定授權規則，請使用下列端點 hello:</span><span class="sxs-lookup"><span data-stu-id="997ec-202">tooupdate or delete a specific authorization rule, use hello following endpoint:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a><span data-ttu-id="997ec-203">存取實體上的共用存取授權規則</span><span class="sxs-lookup"><span data-stu-id="997ec-203">Access Shared Access Authorization rules on an entity</span></span>

<span data-ttu-id="997ec-204">您可以存取[Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)物件上的服務匯流排佇列或主題透過 hello 設定[AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules)中 hello 集合對應[QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription)或[TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription)。</span><span class="sxs-lookup"><span data-stu-id="997ec-204">You can access a [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object configured on a Service Bus queue or topic through hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) collection in hello corresponding [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) or [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).</span></span>

<span data-ttu-id="997ec-205">下列程式碼的 hello 顯示佇列 tooadd 授權規則的方式。</span><span class="sxs-lookup"><span data-stu-id="997ec-205">hello following code shows how tooadd authorization rules for a queue.</span></span>

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

## <a name="use-shared-access-signature-authorization"></a><span data-ttu-id="997ec-206">使用共用存取簽章授權</span><span class="sxs-lookup"><span data-stu-id="997ec-206">Use Shared Access Signature authorization</span></span>

<span data-ttu-id="997ec-207">使用 hello Azure.NET SDK 與 hello 服務匯流排.NET 程式庫的應用程式可以使用 SAS 授權透過 hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider)類別。</span><span class="sxs-lookup"><span data-stu-id="997ec-207">Applications using hello Azure .NET SDK with hello Service Bus .NET libraries can use SAS authorization through hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) class.</span></span> <span data-ttu-id="997ec-208">hello 下列程式碼說明如何 hello 使用 hello 權杖提供者 toosend 訊息 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="997ec-208">hello following code illustrates hello use of hello token provider toosend messages tooa Service Bus queue.</span></span>

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

<span data-ttu-id="997ec-209">應用程式在接受連接字串的方法中使用 SAS 連接字串，也可以使用 SAS 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="997ec-209">Applications can also use SAS for authentication by using a SAS connection string in methods that accept connection strings.</span></span>

<span data-ttu-id="997ec-210">請注意該 toouse SAS 授權，使用服務匯流排轉送，您可以使用設定 hello 服務匯流排命名空間的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-210">Note that toouse SAS authorization with Service Bus relays, you can use SAS keys configured on hello Service Bus namespace.</span></span> <span data-ttu-id="997ec-211">如果您明確建立轉送 hello 命名空間 ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)與[RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) 物件，您可以設定該轉送的 hello SAS 規則。</span><span class="sxs-lookup"><span data-stu-id="997ec-211">If you explicitly create a relay on hello namespace ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) with a [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) object, you can set hello SAS rules just for that relay.</span></span> <span data-ttu-id="997ec-212">具有服務匯流排訂閱 toouse SAS 授權，您可以使用服務匯流排命名空間或主題上設定的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="997ec-212">toouse SAS authorization with Service Bus subscriptions, you can use SAS keys configured on a Service Bus namespace or on a topic.</span></span>

## <a name="use-hello-shared-access-signature-at-http-level"></a><span data-ttu-id="997ec-213">使用共用存取簽章 hello （在 HTTP 層級）</span><span class="sxs-lookup"><span data-stu-id="997ec-213">Use hello Shared Access Signature (at HTTP level)</span></span>

<span data-ttu-id="997ec-214">您現在知道 toocreate 共用存取簽章服務匯流排中的任何實體，您在準備 tooperform HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="997ec-214">Now that you know how toocreate Shared Access Signatures for any entities in Service Bus, you are ready tooperform an HTTP POST:</span></span>

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

<span data-ttu-id="997ec-215">請記住，這適用於所有項目。</span><span class="sxs-lookup"><span data-stu-id="997ec-215">Remember, this works for everything.</span></span> <span data-ttu-id="997ec-216">您可以為佇列、主題或訂用帳戶建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="997ec-216">You can create SAS for a queue, topic, or subscription.</span></span> 

<span data-ttu-id="997ec-217">如果您提供的寄件者或用戶端的 SAS 權杖，不會直接管理，擁有 hello 索引鍵，而且它們無法回復 hello 雜湊 tooobtain 它。</span><span class="sxs-lookup"><span data-stu-id="997ec-217">If you give a sender or client a SAS token, they don't have hello key directly, and they cannot reverse hello hash tooobtain it.</span></span> <span data-ttu-id="997ec-218">因此，您可以控制他們可以存取的項目，以及時間長度。</span><span class="sxs-lookup"><span data-stu-id="997ec-218">As such, you have control over what they can access, and for how long.</span></span> <span data-ttu-id="997ec-219">重要的事情 tooremember 是，如果您變更 hello hello 原則中的主索引鍵，從它建立任何共用存取簽章將失效。</span><span class="sxs-lookup"><span data-stu-id="997ec-219">An important thing tooremember is that if you change hello primary key in hello policy, any Shared Access Signatures created from it will be invalidated.</span></span>

## <a name="use-hello-shared-access-signature-at-amqp-level"></a><span data-ttu-id="997ec-220">使用共用存取簽章 hello （在 AMQP 層級）</span><span class="sxs-lookup"><span data-stu-id="997ec-220">Use hello Shared Access Signature (at AMQP level)</span></span>

<span data-ttu-id="997ec-221">Hello 上一節，在您已看到如何 toouse hello 與 HTTP POST 要求來傳送資料 toohello 服務匯流排 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="997ec-221">In hello previous section, you saw how toouse hello SAS token with an HTTP POST request for sending data toohello Service Bus.</span></span> <span data-ttu-id="997ec-222">您知道，您可以存取 Service Bus 使用 hello 進階訊息佇列通訊協定 (AMQP) 是基於效能考量，在許多案例中的 hello 慣用通訊協定 toouse。</span><span class="sxs-lookup"><span data-stu-id="997ec-222">As you know, you can access Service Bus using hello Advanced Message Queuing Protocol (AMQP) that is hello preferred protocol toouse for performance reasons, in many scenarios.</span></span> <span data-ttu-id="997ec-223">hello SAS 權杖的用法與 AMQP 述 hello 文件[AMQP Claim-Based Security 版本 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc)也就是在工作草稿自今天 2013 但完善 azure 支援。</span><span class="sxs-lookup"><span data-stu-id="997ec-223">hello SAS token usage with AMQP is described in hello document [AMQP Claim-Based Security Version 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) that is in working draft since 2013 but well-supported by Azure today.</span></span>

<span data-ttu-id="997ec-224">開始之前 toosend 資料 tooService 匯流排，hello 發行者必須傳送 hello SAS 權杖，節點的內部 AMQP 訊息 tooa 完善 AMQP 名為**$cbs** （您可以將它視為 hello 服務 tooacquire 所使用的 「 特殊 」 佇列並驗證所有hello SAS 權杖）。</span><span class="sxs-lookup"><span data-stu-id="997ec-224">Before starting toosend data tooService Bus, hello publisher must send hello SAS token inside an AMQP message tooa well-defined AMQP node named **$cbs** (you can see it as a "special" queue used by hello service tooacquire and validate all hello SAS tokens).</span></span> <span data-ttu-id="997ec-225">hello 發行者必須指定 hello **ReplyTo**欄位內 hello AMQP 訊息; 這是 hello 節點中的 hello 服務回覆 toohello 發行者與 hello token 的驗證 （簡單要求/回覆模式之間的 hello 結果發行者和服務）。</span><span class="sxs-lookup"><span data-stu-id="997ec-225">hello publisher must specify hello **ReplyTo** field inside hello AMQP message; this is hello node in which hello service replies toohello publisher with hello result of hello token validation (a simple request/reply pattern between publisher and service).</span></span> <span data-ttu-id="997ec-226">會建立此回覆節點 hello 動態，」 講述 hello AMQP 1.0 規格所描述的 「 動態建立的遠端節點 」。</span><span class="sxs-lookup"><span data-stu-id="997ec-226">This reply node is created "on hello fly," speaking about "dynamic creation of remote node" as described by hello AMQP 1.0 specification.</span></span> <span data-ttu-id="997ec-227">在檢查該 hello SAS 權杖有效的之後, 可以向前 hello 發行者，並將其啟動 toosend 資料 toohello 服務中。</span><span class="sxs-lookup"><span data-stu-id="997ec-227">After checking that hello SAS token is valid, hello publisher can go forward and start toosend data toohello service.</span></span>

<span data-ttu-id="997ec-228">hello 下列步驟顯示如何 toosend hello 使用 AMQP 通訊協定使用 hello 的 SAS 權杖[AMQP.Net Lite](https://github.com/Azure/amqpnetlite)程式庫。</span><span class="sxs-lookup"><span data-stu-id="997ec-228">hello following steps show how toosend hello SAS token with AMQP protocol using hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) library.</span></span> <span data-ttu-id="997ec-229">這非常有用，如果您無法使用 hello 官方服務匯流排 SDK (例如在 WinRT，.Net Compact Framework、.Net 微架構和單聲道) 在 C 中開發\#。</span><span class="sxs-lookup"><span data-stu-id="997ec-229">This is useful if you can't use hello official Service Bus SDK (for example on WinRT, .Net Compact Framework, .Net Micro Framework and Mono) developing in C\#.</span></span> <span data-ttu-id="997ec-230">當然，此程式庫是有用 toohelp 了解如何以宣告為基礎的安全性層級 hello AMQP，運作方式，如同在 hello HTTP 層級 （使用 HTTP POST 要求和 hello SAS 權杖內傳送的嗨 「 授權 」 標頭中） 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="997ec-230">Of course, this library is useful toohelp understand how claims-based security works at hello AMQP level, as you saw how it works at hello HTTP level (with an HTTP POST request and hello SAS token sent inside hello "Authorization" header).</span></span> <span data-ttu-id="997ec-231">如果您不需要這類 AMQP 深度的知識，您可以使用 hello 官方服務匯流排 SDK 與.Net Framework 應用程式，將會替您完成。</span><span class="sxs-lookup"><span data-stu-id="997ec-231">If you don't need such deep knowledge about AMQP, you can use hello official Service Bus SDK with .Net Framework applications, which will do it for you.</span></span>

### <a name="c35"></a><span data-ttu-id="997ec-232">C&#35;</span><span class="sxs-lookup"><span data-stu-id="997ec-232">C&#35;</span></span>

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

<span data-ttu-id="997ec-233">hello`PutCbsToken()`方法會接收 hello*連接*(AMQP 連接類別執行個體所提供 hello [AMQP.NET Lite 程式庫](https://github.com/Azure/amqpnetlite)) 表示 hello TCP 連線 toohello 服務和 hello*sasToken* hello SAS 權杖 toosend 參數。</span><span class="sxs-lookup"><span data-stu-id="997ec-233">hello `PutCbsToken()` method receives hello *connection* (AMQP connection class instance as provided by hello [AMQP .NET Lite library](https://github.com/Azure/amqpnetlite)) that represents hello TCP connection toohello service and hello *sasToken* parameter that is hello SAS token toosend.</span></span> 

> [!NOTE]
> <span data-ttu-id="997ec-234">請務必 hello 連線會透過**SASL 驗證機制設定 tooEXTERNAL** （和不 hello 使用者名稱和密碼，您不需要 toosend hello SAS 權杖時使用的預設純）。</span><span class="sxs-lookup"><span data-stu-id="997ec-234">It's important that hello connection is created with **SASL authentication mechanism set tooEXTERNAL** (and not hello default PLAIN with username and password used when you don't need toosend hello SAS token).</span></span>
> 
> 

<span data-ttu-id="997ec-235">接下來，hello 「 發行者 」 會建立兩個 AMQP 連結來傳送 hello SAS 權杖，以及從 hello 服務收到 hello 回覆 （hello 權杖驗證結果）。</span><span class="sxs-lookup"><span data-stu-id="997ec-235">Next, hello publisher creates two AMQP links for sending hello SAS token and receiving hello reply (hello token validation result) from hello service.</span></span>

<span data-ttu-id="997ec-236">hello AMQP 訊息包含一組屬性，以及比簡單訊息的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="997ec-236">hello AMQP message contains a set of properties, and more information than a simple message.</span></span> <span data-ttu-id="997ec-237">hello SAS 權杖是 hello 主體 hello 訊息 （使用其建構函式）。</span><span class="sxs-lookup"><span data-stu-id="997ec-237">hello SAS token is hello body of hello message (using its constructor).</span></span> <span data-ttu-id="997ec-238">hello **"ReplyTo"**屬性設定為接收 hello hello 接收者連結 （您可以變更其名稱，而且它將會自動建立 hello 服務如果） 上的驗證結果 toohello 節點名稱。</span><span class="sxs-lookup"><span data-stu-id="997ec-238">hello **"ReplyTo"** property is set toohello node name for receiving hello validation result on hello receiver link (you can change its name if you want, and it will be created dynamically by hello service).</span></span> <span data-ttu-id="997ec-239">hello 最後三個應用程式/自訂屬性由 hello 服務 tooindicate 何種類型的作業，它有 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="997ec-239">hello last three application/custom properties are used by hello service tooindicate what kind of operation it has tooexecute.</span></span> <span data-ttu-id="997ec-240">如同 hello CBS 草稿規格所述，它們必須是 hello**作業名稱**（「 put-權杖 」），hello**權杖的型別**（在這個情況下，「 servicebus.windows.net:sastoken")，和 hello **"名稱"hello 觀眾**toowhich hello 語彙基元適用於 （hello 整個實體）。</span><span class="sxs-lookup"><span data-stu-id="997ec-240">As described by hello CBS draft specification, they must be hello **operation name** ("put-token"), hello **type of token** (in this case, a "servicebus.windows.net:sastoken"), and hello **"name" of hello audience** toowhich hello token applies (hello entire entity).</span></span>

<span data-ttu-id="997ec-241">Hello 寄件者連結傳送 hello SAS 權杖後, hello 發行者必須讀取 hello 回應 hello 接收者連結。</span><span class="sxs-lookup"><span data-stu-id="997ec-241">After sending hello SAS token on hello sender link, hello publisher must read hello reply on hello receiver link.</span></span> <span data-ttu-id="997ec-242">hello 回覆是名為應用程式屬性的簡單 AMQP 訊息**」 狀態碼 「**可以容納的 hello 相同值，則為 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="997ec-242">hello reply is a simple AMQP message with an application property named **"status-code"** that can contain hello same values as an HTTP status code.</span></span>

## <a name="rights-required-for-service-bus-operations"></a><span data-ttu-id="997ec-243">服務匯流排作業所需的權限</span><span class="sxs-lookup"><span data-stu-id="997ec-243">Rights required for Service Bus operations</span></span>

<span data-ttu-id="997ec-244">hello 下表顯示 hello 所需的各項作業上服務匯流排資源的存取權限。</span><span class="sxs-lookup"><span data-stu-id="997ec-244">hello following table shows hello access rights required for various operations on Service Bus resources.</span></span>

| <span data-ttu-id="997ec-245">作業</span><span class="sxs-lookup"><span data-stu-id="997ec-245">Operation</span></span> | <span data-ttu-id="997ec-246">所需的宣告</span><span class="sxs-lookup"><span data-stu-id="997ec-246">Claim Required</span></span> | <span data-ttu-id="997ec-247">宣告範圍</span><span class="sxs-lookup"><span data-stu-id="997ec-247">Claim Scope</span></span> |
| --- | --- | --- |
| <span data-ttu-id="997ec-248">**命名空間**</span><span class="sxs-lookup"><span data-stu-id="997ec-248">**Namespace**</span></span> | | |
| <span data-ttu-id="997ec-249">在命名空間上設定授權規則</span><span class="sxs-lookup"><span data-stu-id="997ec-249">Configure authorization rule on a namespace</span></span> |<span data-ttu-id="997ec-250">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-250">Manage</span></span> |<span data-ttu-id="997ec-251">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-251">Any namespace address</span></span> |
| <span data-ttu-id="997ec-252">**服務登錄**</span><span class="sxs-lookup"><span data-stu-id="997ec-252">**Service Registry**</span></span> | | |
| <span data-ttu-id="997ec-253">列舉私人原則</span><span class="sxs-lookup"><span data-stu-id="997ec-253">Enumerate Private Policies</span></span> |<span data-ttu-id="997ec-254">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-254">Manage</span></span> |<span data-ttu-id="997ec-255">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-255">Any namespace address</span></span> |
| <span data-ttu-id="997ec-256">開始在命名空間上接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-256">Begin listening on a namespace</span></span> |<span data-ttu-id="997ec-257">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-257">Listen</span></span> |<span data-ttu-id="997ec-258">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-258">Any namespace address</span></span> |
| <span data-ttu-id="997ec-259">在命名空間中傳送訊息 tooa 接聽程式</span><span class="sxs-lookup"><span data-stu-id="997ec-259">Send messages tooa listener at a namespace</span></span> |<span data-ttu-id="997ec-260">傳送</span><span class="sxs-lookup"><span data-stu-id="997ec-260">Send</span></span> |<span data-ttu-id="997ec-261">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-261">Any namespace address</span></span> |
| <span data-ttu-id="997ec-262">**佇列**</span><span class="sxs-lookup"><span data-stu-id="997ec-262">**Queue**</span></span> | | |
| <span data-ttu-id="997ec-263">建立佇列</span><span class="sxs-lookup"><span data-stu-id="997ec-263">Create a queue</span></span> |<span data-ttu-id="997ec-264">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-264">Manage</span></span> |<span data-ttu-id="997ec-265">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-265">Any namespace address</span></span> |
| <span data-ttu-id="997ec-266">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="997ec-266">Delete a queue</span></span> |<span data-ttu-id="997ec-267">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-267">Manage</span></span> |<span data-ttu-id="997ec-268">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-268">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-269">列舉佇列</span><span class="sxs-lookup"><span data-stu-id="997ec-269">Enumerate queues</span></span> |<span data-ttu-id="997ec-270">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-270">Manage</span></span> |<span data-ttu-id="997ec-271">/$Resources/Queues</span><span class="sxs-lookup"><span data-stu-id="997ec-271">/$Resources/Queues</span></span> |
| <span data-ttu-id="997ec-272">取得 hello 佇列描述</span><span class="sxs-lookup"><span data-stu-id="997ec-272">Get hello queue description</span></span> |<span data-ttu-id="997ec-273">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-273">Manage</span></span> |<span data-ttu-id="997ec-274">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-274">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-275">設定佇列的授權規則</span><span class="sxs-lookup"><span data-stu-id="997ec-275">Configure authorization rule for a queue</span></span> |<span data-ttu-id="997ec-276">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-276">Manage</span></span> |<span data-ttu-id="997ec-277">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-277">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-278">傳送到 toohello 佇列</span><span class="sxs-lookup"><span data-stu-id="997ec-278">Send into toohello queue</span></span> |<span data-ttu-id="997ec-279">傳送</span><span class="sxs-lookup"><span data-stu-id="997ec-279">Send</span></span> |<span data-ttu-id="997ec-280">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-280">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-281">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="997ec-281">Receive messages from a queue</span></span> |<span data-ttu-id="997ec-282">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-282">Listen</span></span> |<span data-ttu-id="997ec-283">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-283">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-284">放棄或完成訊息接收 hello 訊息，以查看並鎖定模式之後</span><span class="sxs-lookup"><span data-stu-id="997ec-284">Abandon or complete messages after receiving hello message in peek-lock mode</span></span> |<span data-ttu-id="997ec-285">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-285">Listen</span></span> |<span data-ttu-id="997ec-286">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-286">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-287">延遲訊息以便稍後擷取</span><span class="sxs-lookup"><span data-stu-id="997ec-287">Defer a message for later retrieval</span></span> |<span data-ttu-id="997ec-288">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-288">Listen</span></span> |<span data-ttu-id="997ec-289">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-289">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-290">讓訊息寄不出去</span><span class="sxs-lookup"><span data-stu-id="997ec-290">Deadletter a message</span></span> |<span data-ttu-id="997ec-291">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-291">Listen</span></span> |<span data-ttu-id="997ec-292">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-292">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-293">取得與訊息佇列工作階段相關聯的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="997ec-293">Get hello state associated with a message queue session</span></span> |<span data-ttu-id="997ec-294">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-294">Listen</span></span> |<span data-ttu-id="997ec-295">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-295">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-296">設定訊息佇列工作階段相關聯的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="997ec-296">Set hello state associated with a message queue session</span></span> |<span data-ttu-id="997ec-297">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-297">Listen</span></span> |<span data-ttu-id="997ec-298">任何有效的佇列位址</span><span class="sxs-lookup"><span data-stu-id="997ec-298">Any valid queue address</span></span> |
| <span data-ttu-id="997ec-299">**主題**</span><span class="sxs-lookup"><span data-stu-id="997ec-299">**Topic**</span></span> | | |
| <span data-ttu-id="997ec-300">建立主題</span><span class="sxs-lookup"><span data-stu-id="997ec-300">Create a topic</span></span> |<span data-ttu-id="997ec-301">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-301">Manage</span></span> |<span data-ttu-id="997ec-302">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-302">Any namespace address</span></span> |
| <span data-ttu-id="997ec-303">刪除主題</span><span class="sxs-lookup"><span data-stu-id="997ec-303">Delete a topic</span></span> |<span data-ttu-id="997ec-304">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-304">Manage</span></span> |<span data-ttu-id="997ec-305">任何有效的主題位址</span><span class="sxs-lookup"><span data-stu-id="997ec-305">Any valid topic address</span></span> |
| <span data-ttu-id="997ec-306">列舉主題</span><span class="sxs-lookup"><span data-stu-id="997ec-306">Enumerate topics</span></span> |<span data-ttu-id="997ec-307">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-307">Manage</span></span> |<span data-ttu-id="997ec-308">/$Resources/Topics</span><span class="sxs-lookup"><span data-stu-id="997ec-308">/$Resources/Topics</span></span> |
| <span data-ttu-id="997ec-309">取得 hello 主題描述</span><span class="sxs-lookup"><span data-stu-id="997ec-309">Get hello topic description</span></span> |<span data-ttu-id="997ec-310">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-310">Manage</span></span> |<span data-ttu-id="997ec-311">任何有效的主題位址</span><span class="sxs-lookup"><span data-stu-id="997ec-311">Any valid topic address</span></span> |
| <span data-ttu-id="997ec-312">設定主題的授權規則</span><span class="sxs-lookup"><span data-stu-id="997ec-312">Configure authorization rule for a topic</span></span> |<span data-ttu-id="997ec-313">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-313">Manage</span></span> |<span data-ttu-id="997ec-314">任何有效的主題位址</span><span class="sxs-lookup"><span data-stu-id="997ec-314">Any valid topic address</span></span> |
| <span data-ttu-id="997ec-315">傳送 toohello 主題</span><span class="sxs-lookup"><span data-stu-id="997ec-315">Send toohello topic</span></span> |<span data-ttu-id="997ec-316">傳送</span><span class="sxs-lookup"><span data-stu-id="997ec-316">Send</span></span> |<span data-ttu-id="997ec-317">任何有效的主題位址</span><span class="sxs-lookup"><span data-stu-id="997ec-317">Any valid topic address</span></span> |
| <span data-ttu-id="997ec-318">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="997ec-318">**Subscription**</span></span> | | |
| <span data-ttu-id="997ec-319">建立訂閱</span><span class="sxs-lookup"><span data-stu-id="997ec-319">Create a subscription</span></span> |<span data-ttu-id="997ec-320">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-320">Manage</span></span> |<span data-ttu-id="997ec-321">任何命名空間位址</span><span class="sxs-lookup"><span data-stu-id="997ec-321">Any namespace address</span></span> |
| <span data-ttu-id="997ec-322">刪除訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="997ec-322">Delete subscription</span></span> |<span data-ttu-id="997ec-323">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-323">Manage</span></span> |<span data-ttu-id="997ec-324">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-324">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-325">列舉訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="997ec-325">Enumerate subscriptions</span></span> |<span data-ttu-id="997ec-326">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-326">Manage</span></span> |<span data-ttu-id="997ec-327">../myTopic/Subscriptions</span><span class="sxs-lookup"><span data-stu-id="997ec-327">../myTopic/Subscriptions</span></span> |
| <span data-ttu-id="997ec-328">取得訂用帳戶描述</span><span class="sxs-lookup"><span data-stu-id="997ec-328">Get subscription description</span></span> |<span data-ttu-id="997ec-329">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-329">Manage</span></span> |<span data-ttu-id="997ec-330">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-330">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-331">放棄或完成訊息接收 hello 訊息，以查看並鎖定模式之後</span><span class="sxs-lookup"><span data-stu-id="997ec-331">Abandon or complete messages after receiving hello message in peek-lock mode</span></span> |<span data-ttu-id="997ec-332">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-332">Listen</span></span> |<span data-ttu-id="997ec-333">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-333">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-334">延遲訊息以便稍後擷取</span><span class="sxs-lookup"><span data-stu-id="997ec-334">Defer a message for later retrieval</span></span> |<span data-ttu-id="997ec-335">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-335">Listen</span></span> |<span data-ttu-id="997ec-336">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-336">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-337">讓訊息寄不出去</span><span class="sxs-lookup"><span data-stu-id="997ec-337">Deadletter a message</span></span> |<span data-ttu-id="997ec-338">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-338">Listen</span></span> |<span data-ttu-id="997ec-339">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-339">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-340">取得與主題工作階段相關聯的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="997ec-340">Get hello state associated with a topic session</span></span> |<span data-ttu-id="997ec-341">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-341">Listen</span></span> |<span data-ttu-id="997ec-342">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-342">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-343">與主題工作階段相關聯的設定 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="997ec-343">Set hello state associated with a topic session</span></span> |<span data-ttu-id="997ec-344">接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-344">Listen</span></span> |<span data-ttu-id="997ec-345">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-345">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-346">**規則**</span><span class="sxs-lookup"><span data-stu-id="997ec-346">**Rules**</span></span> | | |
| <span data-ttu-id="997ec-347">建立規則</span><span class="sxs-lookup"><span data-stu-id="997ec-347">Create a rule</span></span> |<span data-ttu-id="997ec-348">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-348">Manage</span></span> |<span data-ttu-id="997ec-349">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-349">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-350">刪除規則</span><span class="sxs-lookup"><span data-stu-id="997ec-350">Delete a rule</span></span> |<span data-ttu-id="997ec-351">管理</span><span class="sxs-lookup"><span data-stu-id="997ec-351">Manage</span></span> |<span data-ttu-id="997ec-352">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="997ec-352">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="997ec-353">列舉規則</span><span class="sxs-lookup"><span data-stu-id="997ec-353">Enumerate rules</span></span> |<span data-ttu-id="997ec-354">管理或接聽</span><span class="sxs-lookup"><span data-stu-id="997ec-354">Manage or Listen</span></span> |<span data-ttu-id="997ec-355">../myTopic/Subscriptions/mySubscription/Rules</span><span class="sxs-lookup"><span data-stu-id="997ec-355">../myTopic/Subscriptions/mySubscription/Rules</span></span> 

## <a name="next-steps"></a><span data-ttu-id="997ec-356">後續步驟</span><span class="sxs-lookup"><span data-stu-id="997ec-356">Next steps</span></span>

<span data-ttu-id="997ec-357">toolearn 有關服務匯流排傳訊的詳細資訊，請參閱下列主題中的 hello。</span><span class="sxs-lookup"><span data-stu-id="997ec-357">toolearn more about Service Bus messaging, see hello following topics.</span></span>

* [<span data-ttu-id="997ec-358">服務匯流排基本概念</span><span class="sxs-lookup"><span data-stu-id="997ec-358">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="997ec-359">服務匯流排佇列、主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="997ec-359">Service Bus queues, topics, and subscriptions</span></span>](service-bus-queues-topics-subscriptions.md)
* [<span data-ttu-id="997ec-360">如何 toouse 服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="997ec-360">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="997ec-361">如何 toouse Service Bus 主題和訂閱</span><span class="sxs-lookup"><span data-stu-id="997ec-361">How toouse Service Bus topics and subscriptions</span></span>](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com