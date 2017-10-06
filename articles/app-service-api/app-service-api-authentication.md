---
title: "aaaAuthentication 和 Azure App Service 中的應用程式開發介面應用程式的授權 |Microsoft 文件"
description: "深入了解 Azure App Service API 應用程式提供的 hello 驗證和授權服務。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Azure App Service 中的 API Apps 驗證與授權
## <a name="overview"></a>概觀
> [!NOTE]
> 本主題將會移轉的 tooa 合併[應用程式服務驗證 / 授權](../app-service/app-service-authentication-overview.md)主題，其中涵蓋了網頁、 行動裝置版及 API 應用程式。
> 
> 

Azure App Service 提供內建的驗證與授權服務，可實作 [OAuth 2.0](#oauth) 和 [OpenID Connect](#oauth)。 本文說明 hello 和服務可供 Azure App Service 中的應用程式開發介面應用程式的選項。

hello 下列圖表將說明幾個重要特性的應用程式服務驗證：

* 它會前置處理傳入的 API 要求，這表示它能使用 App Service 所支援的任何語言或架構。
* 它提供幾個選項用於多少驗證正常運作，您想要 toodo 自己的程式碼中。
* 它適用於使用者與服務帳戶驗證。 
* 它支援五個識別提供者：Azure Active Directory、Facebook、Google、Twitter 和 Microsoft 帳戶。
* 它適用於 hello 相同應用程式開發介面應用程式、 Web 應用程式，和行動應用程式。

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>不限語言
要求到達應用程式開發介面應用程式，這表示任何語言或架構所撰寫的應用程式開發介面應用程式的 hello 驗證功能的運作之前，就會發生應用程式服務驗證處理。  您可以根據 ASP.NET、Java、Node.js 或任何 App Service 所支援的架構建立 API。

應用程式服務傳送的 hello JSON web 權杖 (JWT) 的 HTTP 要求，hello 授權標頭中，並以任何語言或架構所撰寫的程式碼可以取得 hello 所需要的資訊從 hello 語彙基元。 此外，應用程式服務可讓您更容易存取 toohello 最常使用的宣告設定特殊的標頭，hello 如下：

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

在.NET API 中，您可以使用 hello`Authorize`屬性，然後更細緻的授權，您可以輕鬆地撰寫程式碼根據的宣告的宣告資訊會為您填入.NET 類別中。

## <a name="multiple-protection-options"></a>多個保護選項
App Service 可以防止匿名 HTTP 要求進入您的 API 應用程式、傳遞所有要求並驗證要求中所包含的權杖，或是不採取任何動作就放行所有要求：

1. 只有已驗證的要求 tooreach 可讓您 API 應用程式。
   
    如果從瀏覽器中收到的匿名要求，則應用程式服務將會重新導向 tooa hello 驗證提供者的登入頁面 (Azure AD、 Google、 Twitter 等)，您選擇。 
   
    使用此選項，您不再需要 toowrite 任何驗證程式碼完全應用程式中，而授權程式碼已經過簡化，因為 hello HTTP 標頭中所提供的 hello 最重要的宣告。
2. 允許所有要求 tooreach 應用程式的應用程式開發介面，但驗證已驗證的要求，並傳遞 hello HTTP 標頭中的驗證資訊。
   
    此選項可讓您更有彈性地處理匿名要求，但是您有 toowrite 程式碼，如果您希望 tooprevent 匿名使用者使用您的 API。 Hello 最受歡迎的宣告會傳入 hello 標頭的 HTTP 要求，因為授權碼是相當簡單。
3. 允許所有要求 tooreach 您的 API，hello 要求中的驗證資訊採取任何動作。
   
    這個選項會將驗證與授權完全向上 tooyour 應用程式程式碼的 hello 工作。

在 hello [Azure 入口網站](https://portal.azure.com/)，選取您想要在 hello 的 hello 選項**驗證 / 授權**刀鋒視窗。

![](./media/app-service-api-authentication/authblade.png)

使用選項 1 和 2，請開啟**應用程式服務驗證**，在 hello**當要求未經驗證的動作 tootake**下拉式清單中選擇**登入**或**允許要求 （無動作）**。  如果您選擇**登入**，您有 toochoose 驗證提供者，並設定該提供者。

![](./media/app-service-api-authentication/actiontotake.png)

如需詳細資訊 tooconfigure 驗證，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。 hello 文章適用 tooAPI 應用程式，以及行動裝置的應用程式，而且連結 tooother 文章中的 hello 其他驗證提供者。

## <a id="internal"></a> 服務帳戶驗證
應用程式服務驗證適用於這類內部案例從一個應用程式開發介面應用程式 tooanother API 應用程式呼叫。 在此案例中，您可以使用服務帳戶認證 (而非使用者認證) 來取得權杖。 服務帳戶在 Azure Active Directory 中也稱為 *服務主體* ，使用這類帳戶的驗證也稱為服務對服務案例。 

服務對服務案例中，保護 hello 呼叫 API 應用程式使用 Azure Active Directory，並提供 AAD 服務主體的授權權杖，當您呼叫 hello API 應用程式。 您可以取得權杖，以提供 hello 用戶端識別碼和機密的 hello AAD 應用程式的用戶端。 沒有特殊的僅限 Azure 程式碼是必要項目，例如使用的 toobe true，表示處理 hello 行動服務 Zumo 語彙基元。 此案例中使用 ASP.NET 應用程式開發介面應用程式的範例 hello 教學課程涵蓋[API 應用程式的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)。

如果您想 toohandle 服務對服務案例不會使用應用程式服務驗證時，您可以使用用戶端憑證驗證或基本驗證。 在 Azure 中的用戶端憑證的相關資訊，請參閱[如何 tooConfigure TLS 相互驗證 Web 應用程式](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。 如需 ASP.NET 中的基本驗證相關資訊，請參閱 [ASP.NET Web API 2 中的驗證篩選](http://www.asp.net/web-api/overview/security/authentication-filters)。

從應用程式服務的邏輯應用程式 tooan API 應用程式的服務帳戶驗證是特殊案例，說明在[使用您裝載邏輯應用程式的 App Service 上的自訂 API](../logic-apps/logic-apps-custom-hosted-api.md)。

## <a name="mobile-client-authentication"></a>行動用戶端驗證
如需有關資訊 toohandle 驗證來自行動用戶端，請參閱 hello[驗證行動裝置應用程式的文件](../app-service-mobile/app-service-mobile-ios-get-started-users.md)。 應用程式服務驗證的運作方式 hello 行動裝置應用程式及 API 應用程式相同的方式。

## <a name="more-information"></a>詳細資訊
如需驗證和授權的 Azure 應用程式服務的詳細資訊，請參閱下列資源的 hello:

* [擴充 App Service 驗證/授權](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)（包括連結在 hello hello 頁面最上方的其他驗證提供者）。 

如需 OAuth 2.0、 OpenID Connect 和 JSON Web Token (JWT) 的詳細資訊，請參閱下列資源的 hello。

* [開始使用 OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [簡介 tooOAuth2 OpenID Connect 和 JSON Web 權杖 (JWT)-Pluralsight 課程](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [在 ASP.NET 中建置和保護多個用戶端的 RESTful API - Pluralsight 課程](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

如需 Azure Active Directory 的詳細資訊，請參閱下列資源的 hello。

* [Azure AD 案例](http://aka.ms/aadscenarios)
* [Azure AD 開發人員指南](http://aka.ms/aaddev)
* [Azure AD 範例](http://aka.ms/aadsamples)

## <a name="next-steps"></a>後續步驟
本文說明了可用於 API 應用程式之 App Service 的驗證和授權功能。 hello hello 取得下一個教學課程如何啟動系列的節目 tooimplement [App Service API 應用程式中的使用者驗證](app-service-api-dotnet-user-principal-auth.md)。

