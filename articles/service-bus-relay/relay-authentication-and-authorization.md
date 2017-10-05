---
title: "Azure 轉送驗證和授權 | Microsoft Docs"
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
ms.openlocfilehash: 95589ca169926362fa77f0e307afd449014c8402
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-authentication-and-authorization"></a><span data-ttu-id="e04b6-103">Azure 轉送驗證和授權</span><span class="sxs-lookup"><span data-stu-id="e04b6-103">Azure Relay authentication and authorization</span></span>
<span data-ttu-id="e04b6-104">應用程式可以使用共用存取簽章 (SAS) 驗證向 Azure 轉送進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e04b6-104">Applications can authenticate to Azure Relay using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="e04b6-105">與[服務匯流排傳訊](../service-bus-messaging/service-bus-authentication-and-authorization.md)相同，SAS 驗證可讓應用程式使用在轉送命名空間設定的存取金鑰，向 Azure 轉送服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e04b6-105">Similar to [Service Bus messaging](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS authentication enables applications to authenticate to the Azure Relay service using an access key configured on the Relay namespace.</span></span> <span data-ttu-id="e04b6-106">您可以接著使用此金鑰來產生共用存取簽章權杖，以便用戶端用來向轉送服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e04b6-106">You can then use this key to generate a Shared Access Signature token that clients can use to authenticate to the relay service.</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="e04b6-107">共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="e04b6-107">Shared Access Signature authentication</span></span>
<span data-ttu-id="e04b6-108">[SAS 驗證](../service-bus-messaging/service-bus-sas.md)可讓您授與使用者具有特定權限之 Azure 轉送資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="e04b6-108">[SAS authentication](../service-bus-messaging/service-bus-sas.md) enables you to grant a user access to Azure Relay resources with specific rights.</span></span> <span data-ttu-id="e04b6-109">SAS 驗證牽涉到在資源上設定具有相關權限的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e04b6-109">SAS authentication involves the configuration of a cryptographic key with associated rights on a resource.</span></span> <span data-ttu-id="e04b6-110">接著用戶端可以藉由提出 SAS 權杖 (其中包含正在存取的資源 URI 及利用設定金鑰簽署的到期日) 存取該資源。</span><span class="sxs-lookup"><span data-stu-id="e04b6-110">Clients can then gain access to that resource by presenting a SAS token, which consists of the resource URI being accessed and an expiry signed with the configured key.</span></span>

<span data-ttu-id="e04b6-111">您可以在轉送命名空間上設定 SAS 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e04b6-111">You can configure keys for SAS on a Relay namespace.</span></span> <span data-ttu-id="e04b6-112">不同於服務匯流排傳訊，[轉送混合式連線](relay-hybrid-connections-protocol.md)支援未經授權或匿名的寄件者。</span><span class="sxs-lookup"><span data-stu-id="e04b6-112">Unlike Service Bus messaging, [Relay Hybrid Connections](relay-hybrid-connections-protocol.md) supports unauthorized or anonymous senders.</span></span> <span data-ttu-id="e04b6-113">您可以在建立實體時啟用匿名存取，如下列入口網站中的螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="e04b6-113">You can enable anonymous access for the entity when you create it, as shown in the following screen shot from the portal:</span></span>

![][0]

<span data-ttu-id="e04b6-114">若要使用 SAS，您可以在轉送命名空間上設定包含下列項目的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 物件：</span><span class="sxs-lookup"><span data-stu-id="e04b6-114">To use SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Relay namespace that consists of the following:</span></span>

* <span data-ttu-id="e04b6-115">*KeyName* 。</span><span class="sxs-lookup"><span data-stu-id="e04b6-115">*KeyName* that identifies the rule.</span></span>
* <span data-ttu-id="e04b6-116">*PrimaryKey* 是用來簽署/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e04b6-116">*PrimaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="e04b6-117">*SecondaryKey* 是用來簽署/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e04b6-117">*SecondaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="e04b6-118">*權限* 表示接聽、傳送或管理授與權限的集合。</span><span class="sxs-lookup"><span data-stu-id="e04b6-118">*Rights* representing the collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="e04b6-119">在命名空間層級設定的授權規則可以授與命名空間中所有轉送連線的存取權給具備使用對應金鑰簽署之權杖的用戶端。</span><span class="sxs-lookup"><span data-stu-id="e04b6-119">Authorization rules configured at the namespace level can grant access to all relay connections in a namespace for clients with tokens signed using the corresponding key.</span></span> <span data-ttu-id="e04b6-120">在轉送命名空間上最多可以設定 12 條這類授權規則。</span><span class="sxs-lookup"><span data-stu-id="e04b6-120">Up to 12 such authorization rules can be configured on a Relay namespace.</span></span> <span data-ttu-id="e04b6-121">根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。</span><span class="sxs-lookup"><span data-stu-id="e04b6-121">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="e04b6-122">若要存取實體，用戶端需要使用特定 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)產生的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="e04b6-122">To access an entity, the client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="e04b6-123">SAS 權杖乃是使用資源字串的 HMAC-SHA256 所產生，該字串由宣告存取的資源 URI 以及具備與授權規則相關聯之密碼編譯金鑰的過期所組成。</span><span class="sxs-lookup"><span data-stu-id="e04b6-123">The SAS token is generated using the HMAC-SHA256 of a resource string that consists of the resource URI to which access is claimed, and an expiry with a cryptographic key associated with the authorization rule.</span></span>

<span data-ttu-id="e04b6-124">Azure 轉送的 SAS 驗證支援包含在 Azure .NET SDK 2.0 版或更新版本中。</span><span class="sxs-lookup"><span data-stu-id="e04b6-124">SAS authentication support for Azure Relay is included in the Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="e04b6-125">SAS 包括 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。</span><span class="sxs-lookup"><span data-stu-id="e04b6-125">SAS includes support for a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="e04b6-126">所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。</span><span class="sxs-lookup"><span data-stu-id="e04b6-126">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e04b6-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e04b6-127">Next steps</span></span>
- <span data-ttu-id="e04b6-128">如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](../service-bus-messaging/service-bus-sas.md)。</span><span class="sxs-lookup"><span data-stu-id="e04b6-128">Continue reading [Service Bus authentication with Shared Access Signatures](../service-bus-messaging/service-bus-sas.md) for more details about SAS.</span></span>
- <span data-ttu-id="e04b6-129">如需混合式連線功能的詳細資訊，請參閱 [Azure 轉送混合式連線通訊協定指南](relay-hybrid-connections-protocol.md)。</span><span class="sxs-lookup"><span data-stu-id="e04b6-129">See the [Azure Relay Hybrid Connections protocol guide](relay-hybrid-connections-protocol.md) for detailed information about the Hybrid Connections capability.</span></span>
- <span data-ttu-id="e04b6-130">如需服務匯流排傳訊驗證和授權的相關對應資訊，請參閱[服務匯流排驗證和授權](../service-bus-messaging/service-bus-authentication-and-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="e04b6-130">For corresponding information about Service Bus Messaging authentication and authorization, see [Service Bus authentication and authorization](../service-bus-messaging/service-bus-authentication-and-authorization.md).</span></span> 

[0]: ./media/relay-authentication-and-authorization/hcanon.png