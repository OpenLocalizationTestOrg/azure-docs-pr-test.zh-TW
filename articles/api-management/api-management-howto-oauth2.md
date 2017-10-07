---
title: "在 Azure API 管理使用 OAuth 2.0 aaaAuthorize 開發人員帳戶 |Microsoft 文件"
description: "深入了解如何使用 API 管理中的 OAuth 2.0 tooauthorize 使用者。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>如何 tooauthorize 開發人員帳戶使用 Azure API 管理中的 OAuth 2.0
許多應用程式開發介面支援[OAuth 2.0](http://oauth.net/2/) toosecure hello 應用程式開發介面，並確保，只有有效的使用者有權存取，且他們只能存取資源 toowhich 他們正在權。 在訂單 toouse Azure API 管理的互動式開發人員主控台中使用這類應用程式開發介面，hello 服務可讓您 tooconfigure OAuth 2.0 與您服務執行個體 toowork 啟用應用程式開發介面。

## <a name="prerequisites"> </a>必要條件
本指南也說明您如何 tooconfigure 您 API 管理服務執行個體 toouse OAuth 2.0 授權的開發人員帳戶，但並未顯示您如何 tooconfigure OAuth 2.0 提供者。 每個提供者是不同，雖然 hello 步驟很類似，而且使用 OAuth 2.0 設定您的 API 管理服務執行個體中的資訊所需的 hello 前面的 OAuth 2.0 的 hello 組態 hello 相同。 本主題演示的範例將 Azure Active Directory 當做 OAuth 2.0 提供者。

> [!NOTE]
> 如需有關如何設定使用 Azure Active Directory 的 OAuth 2.0 的詳細資訊，請參閱 hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet]範例。
> 
> 

## <a name="step1"> </a>在 API 管理中設定 OAuth 2.0 授權伺服器
tooget 啟動，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。

![發行者入口網站][api-management-management-console]

> [!NOTE]
> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

按一下**安全性**從 hello **API 管理**hello，請按一下功能表**OAuth 2.0**，然後按一下**新增授權伺服器**。

![OAuth 2.0][api-management-oauth2]

按一下後**新增授權伺服器**，會顯示 hello 新授權伺服器表單。

![New server][api-management-oauth2-server-1]

中輸入名稱和選擇性描述 hello**名稱**和**描述**欄位。 

> [!NOTE]
> 這些欄位是使用的 tooidentify hello OAuth 2.0 授權伺服器 hello 目前 API 管理服務執行個體內，其值不是來自 hello OAuth 2.0 伺服器。
> 
> 

輸入 hello**用戶端註冊頁面 URL**。 此頁面是使用者可建立並管理他們的帳戶，並使用 hello OAuth 2.0 提供者而有所不同。 hello**用戶端註冊頁面 URL**點 toohello 頁面上的使用者可以使用 toocreate 並且支援帳戶的使用者管理的 OAuth 2.0 提供者設定自己的帳戶。 某些組織不設定或不使用這項功能，即使 hello OAuth 2.0 提供者支援它。 如果您的 OAuth 2.0 提供者並沒有設定帳戶的使用者管理，輸入以下預留位置 URL 例如 hello 您公司的 URL，或是如`https://placeholder.contoso.com`。

hello hello 表單下一個區段包含 hello**授權碼授與類型**，**授權端點 URL**，和**授權要求方法**設定。

![New server][api-management-oauth2-server-2]

指定 hello**授權碼授與類型**藉由檢查 hello 預期型別。  。

輸入 hello**授權端點 URL**。 針對 Azure Active Directory，此 URL 會類似 toohello 下列 URL，其中`<client_id>`取代 hello 識別您的應用程式 toohello OAuth 2.0 伺服器的用戶端識別碼。

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

hello**授權要求方法**指定 hello 授權要求傳送 toohello OAuth 2.0 伺服器的方式。 預設會選取 **GET**。

hello 下一個區段是在 hello**語彙基元端點 URL**，**用戶端驗證方法**，**傳送方法的存取權杖**，和**預設範圍**所指定。

![New server][api-management-oauth2-server-3]

Azure Active Directory OAuth 2.0 伺服器，請 hello**語彙基元端點 URL**必須遵循格式，hello 其中`<APPID>`hello 格式的`yourapp.onmicrosoft.com`。

`https://login.microsoftonline.com/<APPID>/oauth2/token`

hello 預設設定**用戶端驗證方法**是**基本**，和**傳送方法的存取權杖**是**授權標頭**. 在 hello 表單，以及 hello 的這個區段上設定這些值**預設範圍**。

hello**用戶端認證**區段包含 hello**用戶端識別碼**和**用戶端密碼**，這取得的 OAuth 2.0 hello 建立及設定程序期間伺服器。 一次 hello**用戶端識別碼**和**用戶端密碼**都有指定，hello **redirect_uri** hello**授權碼**產生。 這個 URI 是 OAuth 2.0 伺服器設定中的使用的 tooconfigure hello 回覆 URL。

![New server][api-management-oauth2-server-4]

如果**授權碼授與類型**設定得**資源擁有者密碼**，hello**資源擁有者密碼認證**區段是使用的 toospecify 那些認證;或者您可以保留空白。

![New server][api-management-oauth2-server-5]

完成 hello 表單之後，請按一下**儲存**toosave hello API 管理的 OAuth 2.0 授權伺服器設定。 Hello 伺服器組態儲存之後，您可以設定應用程式開發介面 toouse 此組態中，hello 下一節中所示。

## <a name="step2"></a>設定 API toouse OAuth 2.0 使用者授權
按一下**Api**從 hello **API 管理**留在 hello 功能表，按一下所需的 hello API hello 名稱，按一下**安全性**，然後核取方塊 hello **OAuth2.0**。

![User authorization][api-management-user-authorization]

選取所需的 hello**授權伺服器**從 hello 下拉式清單中，然後按一下**儲存**。

![User authorization][api-management-user-authorization-save]

## <a name="step3"></a>測試 hello 開發人員入口網站中的 hello OAuth 2.0 使用者授權
一旦您已設定您的 OAuth 2.0 授權伺服器，並設定您的應用程式開發介面 toouse 該伺服器，您可以移 toohello 開發人員入口網站，並呼叫 API 來進行測試。  按一下**開發人員入口網站**hello 右上方功能表中。

![開發人員入口網站][api-management-developer-portal-menu]

按一下**Api** hello 最上層功能表，然後選取在**Echo API**。

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> 如果您有只有一個應用程式開發介面設定，或顯示 tooyour 帳戶，然後按一下 應用程式開發介面引導您直接 toohello 作業，該 api。
> 
> 

選取 hello**取得資源**作業中，按一下**開啟主控台**，然後選取**授權碼**hello 下拉式清單中。

![Open console][api-management-open-console]

當**授權碼**已選取，快顯視窗會顯示以 hello 登入表單 hello OAuth 2.0 提供者。 在此範例中是由 Azure Active Directory 提供 hello 登入表單。

> [!NOTE]
> 如果您有快顯視窗已停用將會提示您 tooenable 它們 hello 瀏覽器。 啟用之後，請選取**授權碼**再次 hello 登入表單便會出現。
> 
> 

![Sign in][api-management-oauth2-signin]

一旦您已登入，hello**要求標頭**會填入`Authorization : Bearer`授權 hello 要求的標頭。

![Request header token][api-management-request-header-token]

此時您可以設定所需的 hello 值 hello 剩餘參數，並送出 hello 要求。 

## <a name="next-steps"></a>後續步驟
如需有關如何使用 OAuth 2.0 和 API 管理的詳細資訊，請參閱 hello 下列視訊和隨附[文章](api-management-howto-protect-backend-with-aad.md)。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

