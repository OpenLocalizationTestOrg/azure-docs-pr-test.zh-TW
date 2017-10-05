---
title: "Azure 服務匯流排驗證和授權 | Microsoft Docs"
description: "使用共用存取簽章 (SAS) 驗證向服務匯流排驗證應用程式。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 28fb41499c919e5006f1be7daa97610c2a0583af
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-authentication-and-authorization"></a><span data-ttu-id="27f41-103">服務匯流排驗證和授權</span><span class="sxs-lookup"><span data-stu-id="27f41-103">Service Bus authentication and authorization</span></span>

<span data-ttu-id="27f41-104">應用程式可以使用共用存取簽章 (SAS) 驗證向 Azure 服務匯流排進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27f41-104">Applications can authenticate to Azure Service Bus using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="27f41-105">共用存取簽章 (SAS) 驗證可讓應用程式使用在命名空間或在與特定權限相關聯的實體上設定的存取金鑰，向服務匯流排進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27f41-105">Shared Access Signature authentication enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the entity with which specific rights are associated.</span></span> <span data-ttu-id="27f41-106">您可以接著使用此金鑰來產生共用存取簽章權杖，以便用戶端用來向服務匯流排進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27f41-106">You can then use this key to generate a Shared Access Signature token that clients can use to authenticate to Service Bus.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27f41-107">您應該使用 SAS 而不是 Azure Active Directory 存取控制 (也稱為存取控制服務或 ACS)，因為 ACS 已被取代。</span><span class="sxs-lookup"><span data-stu-id="27f41-107">You should use SAS instead of Azure Active Directory Access Control (also known as Access Control Service or ACS), as ACS is being deprecated.</span></span> <span data-ttu-id="27f41-108">SAS 可為服務匯流排提供簡單、有彈性且容易使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="27f41-108">SAS provides a simple, flexible, and easy-to-use authentication scheme for Service Bus.</span></span> <span data-ttu-id="27f41-109">在應用程式不需要管理已授權「使用者」概念的情況下，可以使用 SAS。</span><span class="sxs-lookup"><span data-stu-id="27f41-109">Applications can use SAS in scenarios in which they do not need to manage the notion of an authorized "user."</span></span> <span data-ttu-id="27f41-110">如需詳細資訊，請參閱 [此部落格文章](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)。</span><span class="sxs-lookup"><span data-stu-id="27f41-110">For more information, see [this blog post](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="27f41-111">共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="27f41-111">Shared Access Signature authentication</span></span>

<span data-ttu-id="27f41-112">[SAS 驗證](service-bus-sas.md) 可讓您授與使用者具有特定權限之服務匯流排資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="27f41-112">[SAS authentication](service-bus-sas.md) enables you to grant a user access to Service Bus resources with specific rights.</span></span> <span data-ttu-id="27f41-113">服務匯流排中的 SAS 驗證牽涉到在服務匯流排資源上設定具有相關權限的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="27f41-113">SAS authentication in Service Bus involves the configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="27f41-114">接著用戶端可以藉由提出 SAS 權杖 (其中包含正在存取的資源 URI 及利用設定金鑰簽署的到期日) 存取該資源。</span><span class="sxs-lookup"><span data-stu-id="27f41-114">Clients can then gain access to that resource by presenting a SAS token, which consists of the resource URI being accessed and an expiry signed with the configured key.</span></span>

<span data-ttu-id="27f41-115">您可以在服務匯流排命名空間上設定 SAS 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="27f41-115">You can configure keys for SAS on a Service Bus namespace.</span></span> <span data-ttu-id="27f41-116">金鑰套用至該命名空間中的所有訊息實體。</span><span class="sxs-lookup"><span data-stu-id="27f41-116">The key applies to all messaging entities in that namespace.</span></span> <span data-ttu-id="27f41-117">您也可以在服務匯流排佇列和主題上設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="27f41-117">You can also configure keys on Service Bus queues and topics.</span></span> <span data-ttu-id="27f41-118">[Azure 轉送](../service-bus-relay/relay-authentication-and-authorization.md)上也支援 SAS。</span><span class="sxs-lookup"><span data-stu-id="27f41-118">SAS is also supported on [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).</span></span>

<span data-ttu-id="27f41-119">若要使用 SAS，您可以在命名空間、佇列或主題上設定 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 物件。</span><span class="sxs-lookup"><span data-stu-id="27f41-119">To use SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a namespace, queue, or topic.</span></span> <span data-ttu-id="27f41-120">此規則由下列元素組成：</span><span class="sxs-lookup"><span data-stu-id="27f41-120">This rule consists of the following elements:</span></span>

* <span data-ttu-id="27f41-121">*KeyName* 。</span><span class="sxs-lookup"><span data-stu-id="27f41-121">*KeyName* that identifies the rule.</span></span>
* <span data-ttu-id="27f41-122">*PrimaryKey* 是用來簽署/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="27f41-122">*PrimaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="27f41-123">*SecondaryKey* 是用來簽署/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="27f41-123">*SecondaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="27f41-124">*權限* 表示接聽、傳送或管理授與權限的集合。</span><span class="sxs-lookup"><span data-stu-id="27f41-124">*Rights* representing the collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="27f41-125">在命名空間層級設定的授權規則可以授與命名空間中所有實體的存取權給具備使用對應金鑰簽署之權杖的用戶端。</span><span class="sxs-lookup"><span data-stu-id="27f41-125">Authorization rules configured at the namespace level can grant access to all entities in a namespace for clients with tokens signed using the corresponding key.</span></span> <span data-ttu-id="27f41-126">在服務匯流排命名空間、佇列或主題上最多可以設定 12 條這類授權規則。</span><span class="sxs-lookup"><span data-stu-id="27f41-126">Up to 12 such authorization rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="27f41-127">根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。</span><span class="sxs-lookup"><span data-stu-id="27f41-127">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="27f41-128">若要存取實體，用戶端需要使用特定 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)產生的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="27f41-128">To access an entity, the client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="27f41-129">SAS 權杖乃是使用資源字串的 HMAC-SHA256 所產生，該字串由宣告存取的資源 URI 以及具備與授權規則相關聯之密碼編譯金鑰的過期所組成。</span><span class="sxs-lookup"><span data-stu-id="27f41-129">The SAS token is generated using the HMAC-SHA256 of a resource string that consists of the resource URI to which access is claimed, and an expiry with a cryptographic key associated with the authorization rule.</span></span>

<span data-ttu-id="27f41-130">服務匯流排的 SAS 驗證支援包含在 Azure .NET SDK 2.0 版或更新版本中。</span><span class="sxs-lookup"><span data-stu-id="27f41-130">SAS authentication support for Service Bus is included in the Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="27f41-131">SAS 包括 [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。</span><span class="sxs-lookup"><span data-stu-id="27f41-131">SAS includes support for a [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="27f41-132">所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。</span><span class="sxs-lookup"><span data-stu-id="27f41-132">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27f41-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27f41-133">Next steps</span></span>

- <span data-ttu-id="27f41-134">如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](service-bus-sas.md)。</span><span class="sxs-lookup"><span data-stu-id="27f41-134">Continue reading [Service Bus authentication with Shared Access Signatures](service-bus-sas.md) for more details about SAS.</span></span>
- [<span data-ttu-id="27f41-135">變更為已啟用 ACS 的命名空間。</span><span class="sxs-lookup"><span data-stu-id="27f41-135">Changes To ACS Enabled namespaces.</span></span>](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- <span data-ttu-id="27f41-136">如需 Azure 轉送驗證和授權的相關對應資訊，請參閱 [Azure 轉送驗證和授權](../service-bus-relay/relay-authentication-and-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="27f41-136">For corresponding information about Azure Relay authentication and authorization, see [Azure Relay authentication and authorization](../service-bus-relay/relay-authentication-and-authorization.md).</span></span> 

