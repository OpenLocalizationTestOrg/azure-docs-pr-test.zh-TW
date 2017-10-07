---
title: "aaaHow toocreate 在 Azure API 管理的應用程式開發介面"
description: "深入了解如何 toocreate 並在 Azure API 管理中設定應用程式開發介面。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>如何在 Azure API 管理的應用程式開發介面 toocreate
API 管理中的 API 代表可供用戶端應用程式叫用的一組作業。 Hello 發行者入口網站中建立新的應用程式開發介面，然後 hello 想要加入作業。 一旦加入 hello 作業之後，hello API 加入 tooa 產品，並可以發行。 一旦發行應用程式開發介面，它可以是訂閱的 tooand 由開發人員使用。

本指南會顯示 hello 第一個步驟 hello 程序中： 如何 toocreate 及 API 管理中設定新的應用程式開發介面。 如需有關加入作業並發行產品的詳細資訊，請參閱[如何 tooadd 作業 tooan API] [ How tooadd operations tooan API]和[如何 toocreate 及發佈產品][How toocreate and publish a product].

## <a name="create-new-api"> </a>建立新的 API
建立並設定在 hello 發行者入口網站應用程式開發介面。 tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**新增應用程式開發介面**。

![Create API][api-management-create-api]

使用 hello**加入新的 API**視窗 tooconfigure hello 新 API。

![Add new API][api-management-add-new-api]

hello 下列欄位會使用的 tooconfigure hello 新 API。

* **Web 應用程式開發介面名稱**提供 hello 應用程式開發介面的唯一和描述性名稱。 它會顯示 hello 開發人員和發行者入口網站中。
* **Web 服務 URL**參考 hello 實作 hello API 的 HTTP 服務。 API 管理將要求轉送 toothis 位址。
* **Web API URL 尾碼**是附加的 toohello hello API 管理服務的基底 URL。 hello 基底 URL 是很常見的 API 管理服務執行個體所裝載的所有 Api。 API 管理它們的後置字元來區分應用程式開發介面，因此 hello 後置字元必須是唯一的給定發行者的每一種 API。
* **Web API URL 配置**決定哪些通訊協定，可為使用的 tooaccess hello API。 預設會指定 HTTPs。
* toooptionally 加入這個新的應用程式開發介面 tooa 產品，請按一下 hello**產品 （選擇性）**下拉式清單並選擇產品。 此步驟可以重複的多次 tooadd hello API toomultiple 產品。

一旦 hello 需要值的設定，請按一下**儲存**。 一旦建立 hello 新 API，hello hello api 摘要頁面會顯示 hello 發行者入口網站中。

![API summary][api-management-api-summary]

## <a name="configure-api-settings"> </a>設定 API 設定
您可以使用 hello**設定**tooverify 索引標籤上和編輯應用程式開發介面的 hello 組態。 **Web 應用程式開發介面名稱**， **Web 服務 URL**，和**Web API URL 尾碼**一開始建立 hello 應用程式開發介面，而且可以進行修改時在這裡會設定。 **描述**提供選擇性描述，和**Web API URL 配置**決定哪些通訊協定，可為使用的 tooaccess hello API。

![API settings][api-management-api-settings]

tooconfigure 閘道驗證 hello 後端服務實作的 hello API 中，選取 hello**安全性** 索引標籤 hello**認證**下拉式清單可以是使用的 tooconfigure **HTTP基本**或**用戶端憑證**驗證。 toouse HTTP 基本驗證時，只要輸入 hello 所需的認證。 如需使用用戶端憑證驗證的資訊，請參閱[toosecure 後端服務使用用戶端憑證驗證在 Azure API 管理的如何][How toosecure back-end services using client certificate authentication in Azure API Management]。

hello**安全性** 索引標籤也可以使用的 tooconfigure**使用者授權**使用 OAuth 2.0。 如需詳細資訊，請參閱[tooauthorize 開發人員帳戶使用的方式在 Azure API 管理的 OAuth 2.0][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]。

![Basic authentication settings][api-management-api-settings-credentials]

按一下**儲存**toosave 任何您所做變更 toohello API 設定。

## <a name="next-steps"> </a>後續步驟
一旦建立應用程式開發介面，並設定 hello 設定，hello 接下來的步驟 tooadd hello 作業 toohello 應用程式開發介面，加入 hello API tooa 產品，並將它發行，使其可讓開發人員。 如需詳細資訊，請參閱下列文章 hello。

* [如何 tooadd 作業 tooan 應用程式開發介面][How tooadd operations tooan API]
* [如何 toocreate 及發佈產品][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
