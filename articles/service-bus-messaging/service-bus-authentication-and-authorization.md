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
# <a name="service-bus-authentication-and-authorization"></a>服務匯流排驗證和授權

應用程式可以驗證 tooAzure Service Bus 使用共用存取簽章 (SAS) 驗證。 共用存取簽章驗證可讓應用程式 tooauthenticate tooService 匯流排使用 hello 命名空間，或與特定權限相關聯的 hello 實體上設定的存取金鑰。 然後，您可以使用此索引鍵 toogenerate 用戶端可以使用 tooauthenticate tooService 匯流排的共用存取簽章語彙基元。

> [!IMPORTANT]
> 您應該使用 SAS 而不是 Azure Active Directory 存取控制 (也稱為存取控制服務或 ACS)，因為 ACS 已被取代。 SAS 可為服務匯流排提供簡單、有彈性且容易使用的驗證配置。 應用程式可以使用 SAS，在案例中就不需要 toomanage hello 概念授權 「 使用者。 」 如需詳細資訊，請參閱 [此部落格文章](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)。

## <a name="shared-access-signature-authentication"></a>共用存取簽章驗證

[SAS 驗證](service-bus-sas.md)可讓您 toogrant 使用者存取 tooService 匯流排 」 資源，以特定權限。 服務匯流排中的 SAS 驗證包括 hello 組態與服務匯流排資源上的權限相關聯的密碼編譯金鑰。 用戶端便可以存取 toothat 資源所呈現 SAS 權杖，其中包含 hello 資源所存取的 URI 和簽署以 hello 到期設定索引鍵。

您可以在服務匯流排命名空間上設定 SAS 的金鑰。 hello 金鑰適用於 tooall 該命名空間中的訊息實體。 您也可以在服務匯流排佇列和主題上設定金鑰。 [Azure 轉送](../service-bus-relay/relay-authentication-and-authorization.md)上也支援 SAS。

您可以設定 toouse SAS， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)命名空間、 佇列或主題上的物件。 此規則包含下列項目 hello:

* *KeyName*可識別 hello 規則。
* *PrimaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。
* *SecondaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。
* *權限*代表 hello 接聽的集合，傳送或管理權授與權限。

在 hello 命名空間層級設定的授權規則可以授與存取 tooall 實體命名空間中的用戶端以使用 hello 對應金鑰簽署的權杖。 向上 too12 可以服務匯流排命名空間、 佇列或主題上設定這類的授權規則。 根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。

實體 tooaccess，hello 用戶端需要使用特定產生 SAS 權杖[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)。 hello SAS 權杖會產生過期的 hello 組成 hello 資源 URI toowhich 存取的資源字串的 hmac-sha256 宣告，以及使用 hello 授權規則與相關聯的密碼編譯金鑰。

服務匯流排的 SAS 驗證支援是包含在 hello Azure.NET SDK 2.0 版及更新版本。 SAS 包括 [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。 所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。

## <a name="next-steps"></a>後續步驟

- 如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](service-bus-sas.md)。
- [變更 tooACS 已啟用命名空間。](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- 如需 Azure 轉送驗證和授權的相關對應資訊，請參閱 [Azure 轉送驗證和授權](../service-bus-relay/relay-authentication-and-authorization.md)。 

