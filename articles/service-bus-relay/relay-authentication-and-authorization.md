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
# <a name="azure-relay-authentication-and-authorization"></a>Azure 轉送驗證和授權
應用程式可以驗證 tooAzure 轉送使用共用存取簽章 (SAS) 驗證。 類似太[服務匯流排傳訊](../service-bus-messaging/service-bus-authentication-and-authorization.md)，SAS 驗證可讓應用程式 tooauthenticate toohello Azure 轉送服務使用 hello 轉送命名空間上設定的存取金鑰。 然後，您可以使用此索引鍵 toogenerate 用戶端可以使用 tooauthenticate toohello 轉送服務的共用存取簽章語彙基元。

## <a name="shared-access-signature-authentication"></a>共用存取簽章驗證
[SAS 驗證](../service-bus-messaging/service-bus-sas.md)可讓您 toogrant 使用者存取 tooAzure 轉送 」 資源，以特定權限。 SAS 驗證包括 hello 組態與資源上的權限相關聯的密碼編譯金鑰。 用戶端便可以存取 toothat 資源所呈現 SAS 權杖，其中包含 hello 資源所存取的 URI 和簽署以 hello 到期設定索引鍵。

您可以在轉送命名空間上設定 SAS 的金鑰。 不同於服務匯流排傳訊，[轉送混合式連線](relay-hybrid-connections-protocol.md)支援未經授權或匿名的寄件者。 您可以啟用 hello 實體的匿名存取您在建立時，下列螢幕擷取畫面從 hello 入口網站的 hello 中所示：

![][0]

您可以設定 toouse SAS， [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)上轉送命名空間所組成 hello 下列物件：

* *KeyName*可識別 hello 規則。
* *PrimaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。
* *SecondaryKey*是使用 toosign/驗證 SAS 權杖的密碼編譯金鑰。
* *權限*代表 hello 接聽的集合，傳送或管理權授與權限。

在 hello 命名空間層級設定的授權規則可以授與存取 tooall 轉送連線命名空間中的用戶端以使用 hello 對應金鑰簽署的權杖。 向上 too12 可以轉送命名空間上設定這類的授權規則。 根據預設，具備所有權限的 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 會在第一次佈建時為每個命名空間設定。

實體 tooaccess，hello 用戶端需要使用特定產生 SAS 權杖[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)。 hello SAS 權杖會產生過期的 hello 組成 hello 資源 URI toowhich 存取的資源字串的 hmac-sha256 宣告，以及使用 hello 授權規則與相關聯的密碼編譯金鑰。

包含在 hello Azure.NET SDK 2.0 版及更新版本 Azure 轉送的 SAS 驗證支援。 SAS 包括 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)的支援。 所有接受連接字串做為參數的 API 包括 SAS 連接字串的支援。

## <a name="next-steps"></a>後續步驟
- 如需 SAS 的詳細資料，請繼續閱讀[使用共用存取簽章的服務匯流排驗證](../service-bus-messaging/service-bus-sas.md)。
- 請參閱 hello [Azure 轉送混合式連線通訊協定指南](relay-hybrid-connections-protocol.md)hello 混合式連線功能的詳細資訊。
- 如需服務匯流排傳訊驗證和授權的相關對應資訊，請參閱[服務匯流排驗證和授權](../service-bus-messaging/service-bus-authentication-and-authorization.md)。 

[0]: ./media/relay-authentication-and-authorization/hcanon.png