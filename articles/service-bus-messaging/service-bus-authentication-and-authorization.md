---
title: "aaaAzure Service Bus 驗證與授權 |Microsoft 文件"
description: "驗證使用共用存取簽章 (SAS) 驗證的應用程式 tooService 匯流排。"
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
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a><span data-ttu-id="912a3-103">服務匯流排驗證和授權</span><span class="sxs-lookup"><span data-stu-id="912a3-103">Service Bus authentication and authorization</span></span>

<span data-ttu-id="912a3-104">應用程式可以驗證 tooAzure Service Bus 使用共用存取簽章 (SAS) 驗證。</span><span class="sxs-lookup"><span data-stu-id="912a3-104">Applications can authenticate tooAzure Service Bus using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="912a3-105">共用存取簽章驗證可讓應用程式 tooauthenticate tooService 匯流排使用 hello 命名空間，或與特定權限相關聯的 hello 實體上設定的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-105">Shared Access Signature authentication enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello entity with which specific rights are associated.</span></span> <span data-ttu-id="912a3-106">然後，您可以使用此索引鍵 toogenerate 用戶端可以使用 tooauthenticate tooService 匯流排的共用存取簽章語彙基元。</span><span class="sxs-lookup"><span data-stu-id="912a3-106">You can then use this key toogenerate a Shared Access Signature token that clients can use tooauthenticate tooService Bus.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="912a3-107">您應該使用 SAS 而不是 Azure Active Directory 存取控制 (也稱為存取控制服務或 ACS)，因為 ACS 已被取代。</span><span class="sxs-lookup"><span data-stu-id="912a3-107">You should use SAS instead of Azure Active Directory Access Control (also known as Access Control Service or ACS), as ACS is being deprecated.</span></span> <span data-ttu-id="912a3-108">SAS 可為服務匯流排提供簡單、有彈性且容易使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="912a3-108">SAS provides a simple, flexible, and easy-to-use authentication scheme for Service Bus.</span></span> <span data-ttu-id="912a3-109">應用程式可以使用 SAS，在案例中就不需要 toomanage hello 概念授權 「 使用者。 」</span><span class="sxs-lookup"><span data-stu-id="912a3-109">Applications can use SAS in scenarios in which they do not need toomanage hello notion of an authorized "user."</span></span> <span data-ttu-id="912a3-110">如需詳細資訊，請參閱 [此部落格文章](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)。</span><span class="sxs-lookup"><span data-stu-id="912a3-110">For more information, see [this blog post](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="912a3-111">共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="912a3-111">Shared Access Signature authentication</span></span>

<span data-ttu-id="912a3-112">[SAS 驗證](service-bus-sas.md)可讓您 toogrant 使用者存取 tooService 匯流排 」 資源，以特定權限。</span><span class="sxs-lookup"><span data-stu-id="912a3-112">[SAS authentication](service-bus-sas.md) enables you toogrant a user access tooService Bus resources with specific rights.</span></span> <span data-ttu-id="912a3-113">服務匯流排中的 SAS 驗證包括 hello 組態與服務匯流排資源上的權限相關聯的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-113">SAS authentication in Service Bus involves hello configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="912a3-114">用戶端便可以存取 toothat 資源所呈現 SAS 權杖，其中包含 hello 資源所存取的 URI 和簽署以 hello 到期設定索引鍵。</span><span class="sxs-lookup"><span data-stu-id="912a3-114">Clients can then gain access toothat resource by presenting a SAS token, which consists of hello resource URI being accessed and an expiry signed with hello configured key.</span></span>

<span data-ttu-id="912a3-115">您可以在服務匯流排命名空間上設定 SAS 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-115">You can configure keys for SAS on a Service Bus namespace.</span></span> <span data-ttu-id="912a3-116">hello 金鑰適用於 tooall 該命名空間中的訊息實體。</span><span class="sxs-lookup"><span data-stu-id="912a3-116">hello key applies tooall messaging entities in that namespace.</span></span> <span data-ttu-id="912a3-117">您也可以在服務匯流排佇列和主題上設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-117">You can also configure keys on Service Bus queues and topics.</span></span> <span data-ttu-id="912a3-118">[Azure 轉送](../service-bus-relay/relay-authentication-and-authorization.md)上也支援 SAS。</span><span class="sxs-lookup"><span data-stu-id="912a3-118">SAS is also supported on [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).</span></span>

<span data-ttu-id="912a3-119">您可以設定 toouse SAS， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)命名空間、 佇列或主題上的物件。</span><span class="sxs-lookup"><span data-stu-id="912a3-119">toouse SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a namespace, queue, or topic.</span></span> <span data-ttu-id="912a3-120">此規則包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="912a3-120">This rule consists of hello following elements:</span></span>

* <span data-ttu-id="912a3-121">*KeyName*可識別 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="912a3-121">*KeyName* that identifies hello rule.</span></span>
* <span data-ttu-id="912a3-122">*PrimaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-122">*PrimaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="912a3-123">*SecondaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-123">*SecondaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="912a3-124">*權限*代表 hello 接聽的集合，傳送或管理權授與權限。</span><span class="sxs-lookup"><span data-stu-id="912a3-124">*Rights* representing hello collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="912a3-125">在 hello 命名空間層級設定的授權規則可以授與存取 tooall 實體命名空間中的用戶端以使用 hello 對應金鑰簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="912a3-125">Authorization rules configured at hello namespace level can grant access tooall entities in a namespace for clients with tokens signed using hello corresponding key.</span></span> <span data-ttu-id="912a3-126">向上 too12 可以服務匯流排命名空間、 佇列或主題上設定這類的授權規則。</span><span class="sxs-lookup"><span data-stu-id="912a3-126">Up too12 such authorization rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="912a3-127">根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。</span><span class="sxs-lookup"><span data-stu-id="912a3-127">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="912a3-128">實體 tooaccess，hello 用戶端需要使用特定產生 SAS 權杖[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)。</span><span class="sxs-lookup"><span data-stu-id="912a3-128">tooaccess an entity, hello client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="912a3-129">hello SAS 權杖會產生過期的 hello 組成 hello 資源 URI toowhich 存取的資源字串的 hmac-sha256 宣告，以及使用 hello 授權規則與相關聯的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="912a3-129">hello SAS token is generated using hello HMAC-SHA256 of a resource string that consists of hello resource URI toowhich access is claimed, and an expiry with a cryptographic key associated with hello authorization rule.</span></span>

<span data-ttu-id="912a3-130">服務匯流排的 SAS 驗證支援是包含在 hello Azure.NET SDK 2.0 版及更新版本。</span><span class="sxs-lookup"><span data-stu-id="912a3-130">SAS authentication support for Service Bus is included in hello Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="912a3-131">SAS 包括 [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。</span><span class="sxs-lookup"><span data-stu-id="912a3-131">SAS includes support for a [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="912a3-132">所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。</span><span class="sxs-lookup"><span data-stu-id="912a3-132">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="912a3-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="912a3-133">Next steps</span></span>

- <span data-ttu-id="912a3-134">如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](service-bus-sas.md)。</span><span class="sxs-lookup"><span data-stu-id="912a3-134">Continue reading [Service Bus authentication with Shared Access Signatures](service-bus-sas.md) for more details about SAS.</span></span>
- [<span data-ttu-id="912a3-135">變更 tooACS 已啟用命名空間。</span><span class="sxs-lookup"><span data-stu-id="912a3-135">Changes tooACS Enabled namespaces.</span></span>](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- <span data-ttu-id="912a3-136">如需 Azure 轉送驗證和授權的相關對應資訊，請參閱 [Azure 轉送驗證和授權](../service-bus-relay/relay-authentication-and-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="912a3-136">For corresponding information about Azure Relay authentication and authorization, see [Azure Relay authentication and authorization](../service-bus-relay/relay-authentication-and-authorization.md).</span></span> 

