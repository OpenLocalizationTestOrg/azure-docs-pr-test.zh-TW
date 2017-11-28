---
title: "aaaAzure 轉送驗證和授權 |Microsoft 文件"
description: "Azure 轉送中的共用存取簽章 (SAS) 驗證概觀"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a><span data-ttu-id="0c6a0-103">Azure 轉送驗證和授權</span><span class="sxs-lookup"><span data-stu-id="0c6a0-103">Azure Relay authentication and authorization</span></span>
<span data-ttu-id="0c6a0-104">應用程式可以驗證 tooAzure 轉送使用共用存取簽章 (SAS) 驗證。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-104">Applications can authenticate tooAzure Relay using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="0c6a0-105">類似太[服務匯流排傳訊](../service-bus-messaging/service-bus-authentication-and-authorization.md)，SAS 驗證可讓應用程式 tooauthenticate toohello Azure 轉送服務使用 hello 轉送命名空間上設定的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-105">Similar too[Service Bus messaging](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS authentication enables applications tooauthenticate toohello Azure Relay service using an access key configured on hello Relay namespace.</span></span> <span data-ttu-id="0c6a0-106">然後，您可以使用此索引鍵 toogenerate 用戶端可以使用 tooauthenticate toohello 轉送服務的共用存取簽章語彙基元。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-106">You can then use this key toogenerate a Shared Access Signature token that clients can use tooauthenticate toohello relay service.</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="0c6a0-107">共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="0c6a0-107">Shared Access Signature authentication</span></span>
<span data-ttu-id="0c6a0-108">[SAS 驗證](../service-bus-messaging/service-bus-sas.md)可讓您 toogrant 使用者存取 tooAzure 轉送 」 資源，以特定權限。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-108">[SAS authentication](../service-bus-messaging/service-bus-sas.md) enables you toogrant a user access tooAzure Relay resources with specific rights.</span></span> <span data-ttu-id="0c6a0-109">SAS 驗證包括 hello 組態與資源上的權限相關聯的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-109">SAS authentication involves hello configuration of a cryptographic key with associated rights on a resource.</span></span> <span data-ttu-id="0c6a0-110">用戶端便可以存取 toothat 資源所呈現 SAS 權杖，其中包含 hello 資源所存取的 URI 和簽署以 hello 到期設定索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-110">Clients can then gain access toothat resource by presenting a SAS token, which consists of hello resource URI being accessed and an expiry signed with hello configured key.</span></span>

<span data-ttu-id="0c6a0-111">您可以在轉送命名空間上設定 SAS 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-111">You can configure keys for SAS on a Relay namespace.</span></span> <span data-ttu-id="0c6a0-112">不同於服務匯流排傳訊，[轉送混合式連線](relay-hybrid-connections-protocol.md)支援未經授權或匿名的寄件者。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-112">Unlike Service Bus messaging, [Relay Hybrid Connections](relay-hybrid-connections-protocol.md) supports unauthorized or anonymous senders.</span></span> <span data-ttu-id="0c6a0-113">您可以啟用 hello 實體的匿名存取您在建立時，下列螢幕擷取畫面從 hello 入口網站的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="0c6a0-113">You can enable anonymous access for hello entity when you create it, as shown in hello following screen shot from hello portal:</span></span>

![][0]

<span data-ttu-id="0c6a0-114">您可以設定 toouse SAS， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)上轉送命名空間所組成 hello 下列物件：</span><span class="sxs-lookup"><span data-stu-id="0c6a0-114">toouse SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Relay namespace that consists of hello following:</span></span>

* <span data-ttu-id="0c6a0-115">*KeyName*可識別 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-115">*KeyName* that identifies hello rule.</span></span>
* <span data-ttu-id="0c6a0-116">*PrimaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-116">*PrimaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="0c6a0-117">*SecondaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-117">*SecondaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="0c6a0-118">*權限*代表 hello 接聽的集合，傳送或管理權授與權限。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-118">*Rights* representing hello collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="0c6a0-119">在 hello 命名空間層級設定的授權規則可以授與存取 tooall 轉送連線命名空間中的用戶端以使用 hello 對應金鑰簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-119">Authorization rules configured at hello namespace level can grant access tooall relay connections in a namespace for clients with tokens signed using hello corresponding key.</span></span> <span data-ttu-id="0c6a0-120">向上 too12 可以轉送命名空間上設定這類的授權規則。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-120">Up too12 such authorization rules can be configured on a Relay namespace.</span></span> <span data-ttu-id="0c6a0-121">根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-121">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="0c6a0-122">實體 tooaccess，hello 用戶端需要使用特定產生 SAS 權杖[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-122">tooaccess an entity, hello client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="0c6a0-123">hello SAS 權杖會產生過期的 hello 組成 hello 資源 URI toowhich 存取的資源字串的 hmac-sha256 宣告，以及使用 hello 授權規則與相關聯的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-123">hello SAS token is generated using hello HMAC-SHA256 of a resource string that consists of hello resource URI toowhich access is claimed, and an expiry with a cryptographic key associated with hello authorization rule.</span></span>

<span data-ttu-id="0c6a0-124">包含在 hello Azure.NET SDK 2.0 版及更新版本 Azure 轉送的 SAS 驗證支援。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-124">SAS authentication support for Azure Relay is included in hello Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="0c6a0-125">SAS 包括 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-125">SAS includes support for a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="0c6a0-126">所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-126">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c6a0-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c6a0-127">Next steps</span></span>
- <span data-ttu-id="0c6a0-128">如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](../service-bus-messaging/service-bus-sas.md)。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-128">Continue reading [Service Bus authentication with Shared Access Signatures](../service-bus-messaging/service-bus-sas.md) for more details about SAS.</span></span>
- <span data-ttu-id="0c6a0-129">請參閱 hello [Azure 轉送混合式連線通訊協定指南](relay-hybrid-connections-protocol.md)hello 混合式連線功能的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-129">See hello [Azure Relay Hybrid Connections protocol guide](relay-hybrid-connections-protocol.md) for detailed information about hello Hybrid Connections capability.</span></span>
- <span data-ttu-id="0c6a0-130">如需服務匯流排傳訊驗證和授權的相關對應資訊，請參閱[服務匯流排驗證和授權](../service-bus-messaging/service-bus-authentication-and-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="0c6a0-130">For corresponding information about Service Bus Messaging authentication and authorization, see [Service Bus authentication and authorization](../service-bus-messaging/service-bus-authentication-and-authorization.md).</span></span> 

[0]: ./media/relay-authentication-and-authorization/hcanon.png