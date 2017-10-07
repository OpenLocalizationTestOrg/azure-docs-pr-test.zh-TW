---
title: "aaaAzure Active Directory 程式碼範例 |Microsoft 文件"
description: "依案例的組織的 Azure Active Directory 程式碼範例的索引。"
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Azure Active Directory 程式碼範例
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

您可以使用 Microsoft Azure Active Directory (Azure AD) tooadd 驗證和授權 tooyour web 應用程式和 web 應用程式開發介面。 本節會連結您 toosamples 可為您示範如何進行，您可以使用您的應用程式中的程式碼片段。 在 hello 程式碼範例頁面上，您可以找到詳細的讀-我的需求、 安裝和設定說明的主題。 而且 hello 程式碼註解的 toohelp 您了解 hello 關鍵區段。

toounderstand hello 基本案例中的每個範例類型，請參閱 Azure AD 的驗證案例。

參與 tooour GitHub 上的範例： [Microsoft Azure Active Directory 範例和文件](https://github.com/Azure-Samples?page=3&query=active-directory)。

## <a name="web-browser-tooweb-application"></a>Web 瀏覽器 tooWeb 應用程式
以下範例示範如何 toowrite web 應用程式，以指示 hello 使用者的瀏覽器 toosign tooAzure AD 中。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |使用 OpenID Connect （ASP.Net OpenID Connect OWIN 中介軟體） 從 Azure AD 租用戶的 tooauthenticate 使用者。 |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |多租用戶.NET MVC web 應用程式會使用 OpenID Connect （ASP.Net OpenID Connect OWIN 中介軟體） 從多個 Azure AD 租用戶的 tooauthenticate 使用者。 |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |使用 Azure AD 租用戶的 WS-同盟 （ASP.Net WS-同盟 OWIN 中介軟體） tooauthenticate 使用者。 |

## <a name="single-page-application-spa"></a>單一頁面應用程式 (SPA)
這個範例會示範如何 toowrite 單一頁面應用程式保護與 Azure AD。  

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| JavaScript、C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |使用 ADAL，JavaScript 和 Azure AD toosecure AngularJS 型單一頁面應用程式使用 ASP.NET web API 後端實作。 |

## <a name="native-application-tooweb-api"></a>原生應用程式 tooWeb 應用程式開發介面
這些程式碼範例示範如何呼叫 web Api 的 toobuild 原生用戶端應用程式會在 Azure AD 所保護。 它們使用 [Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md) 和 [Azure AD 中的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| Javascript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |使用 Apache Cordova toobuild Apache Cordova 應用程式呼叫 web API，並使用 Azure AD 進行驗證的 hello ADAL 外掛程式。 |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |.NET WPF 應用程式，其呼叫使用 Azure AD 保護的 Web API。 |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Windows 市集應用程式，其呼叫使用 Azure AD 保護的 Web API。 |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Windows 市集應用程式，其呼叫使用 Azure AD 保護的多租用戶 Web API。 |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |原生用戶端應用程式呼叫 web API，其語彙基元 tooact 取得代表 hello 原始使用者，然後再使用 hello 語彙基元 toocall 其他 web API。 |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Windows Phone 8.1 適用的 Windows 市集應用程式，其呼叫由 Azure AD 保護的 Web API。 |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |iOS 應用程式，其呼叫的 Web API 需要 Azure AD 進行驗證。 |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |原生用戶端應用程式中 web API，包括邏輯 tooprocess JWT 權杖中，而不是使用 OWIN 中介軟體。 |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Xamarin 繫結 toohello 原生 Azure AD Authentication Library (ADAL) for hello Android 程式庫。 |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Xamarin 繫結 toohello 原生 Azure AD Authentication Library (ADAL) for iOS。 |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Xamarin 專案，以五個平台為目標，並呼叫由 Azure AD 保護的 Web API。 |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |原生應用程式，其執行非互動式驗證，並呼叫由 Azure AD 保護的 Web API。 |

## <a name="web-application-tooweb-api"></a>Web 應用程式 tooWeb 應用程式開發介面
這些程式碼範例示範如何使用[Azure AD 的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild web 應用程式呼叫 web Api 受到 Azure AD。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |以呼叫 web API hello 登入使用者的權限。 |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |以呼叫 web API hello 應用程式的權限。 |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |新增授權搭配[Azure AD 的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan 現有 web 應用程式使其能呼叫 web API。 |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |設定與 Azure AD 整合的 REST API 服務以保護 API。 包含 Node.js 伺服器與 Web API。 |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |多租用戶 MVC web 應用程式，使用 OpenID Connect （ASP.Net OpenID Connect OWIN 中介軟體） 從 Azure AD 租用戶的 tooauthenticate 使用者。 使用授權碼 tooinvoke hello Graph API。 |

## <a name="server-or-daemon-application-tooweb-api"></a>伺服器或精靈應用程式 tooWeb 應用程式開發介面
這些程式碼範例顯示如何 toobuild 精靈或伺服器應用程式來取得資源從 web API 使用[Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md)和[Azure AD 的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |呼叫 Web API 的主控台應用程式。 hello 用戶端認證是密碼。 |
| C#/.NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |呼叫 Web API 的主控台應用程式。 hello 用戶端認證是憑證。 |

## <a name="calling-azure-ad-graph-api"></a>呼叫 Azure AD Graph API
這些程式碼範例顯示如何呼叫 toobuild 應用程式 hello Azure AD Graph API tooread 和寫入目錄資料。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |使用 hello Graph API tooaccess Azure AD 目錄資料的 web 應用程式。 |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |使用 hello Graph API tooaccess Azure AD 目錄資料的 web 應用程式。 |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |使用 hello Graph API tooaccess Azure AD 目錄資料的 web 應用程式。 |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |此主控台應用程式示範一般讀取和寫入呼叫 toohello Graph API，並示範如何 tooexecute 使用者授權指派及更新使用者的縮圖相片和連結。 |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |主控台應用程式中，使用差異查詢的 hello hello Graph API tooget 定期變更 toouser Azure AD 租用戶中的物件。 |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |MVC 應用程式會使用 Graph API 查詢 toogenerate 簡易公司組織圖。 |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |PHP 應用程式呼叫 hello Graph API tooregister 延伸模組，然後讀取、 更新和刪除 hello 延伸模組屬性中的值。 |

## <a name="authorization"></a>Authorization
這些程式碼範例顯示如何 toouse Azure AD 進行授權。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |在與 Azure AD 整合的應用程式中，使用 Azure Active Directory 群組宣告執行角色型存取控制 (RBAC)。 |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |在與 Azure AD 整合的應用程式中，使用 Azure Active Directory 應用程式角色執行角色型存取控制 (RBAC)。 |

## <a name="legacy-walkthroughs"></a>舊版逐步解說
這些逐步解說使用稍早的技術，不過您也許會感興趣。

| 語言/平台 | 範例 | 說明 |
| --- | --- | --- |
| C#/.NET |[Microsoft Azure AD 應用程式中的角色型和 ACL 型授權](http://go.microsoft.com/fwlink/?LinkId=331694) |在與 Azure AD 整合的應用程式中，執行角色型授權 (RBAC) 和 ACL 型授權。 |
| C#/.NET |[AAL-Windows 市集應用程式 tooREST 服務-驗證](http://go.microsoft.com/fwlink/?LinkId=330605) |使用[Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md) (先前稱為 AAL) 的 Windows 市集 beta 版 tooadd 使用者驗證功能 tooa Windows 市集應用程式。 |
| C#/.NET |[ADAL-原生應用程式 tooREST 服務-透過瀏覽器對話方塊進行 AAD 的驗證](http://go.microsoft.com/fwlink/?LinkId=259814) |使用[Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md) tooadd 使用者驗證功能 tooa WPF 用戶端。 |
| C#/.NET |[ADAL-原生應用程式 tooREST 服務-透過瀏覽器對話方塊的 ACS 進行驗證](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |使用[Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md)和[存取控制服務 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd 使用者驗證功能 tooa WPF 用戶端。 |
| C#/.NET |[ADAL-伺服器 tooServer 驗證](http://go.microsoft.com/fwlink/?LinkId=259816) |使用[Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md) toosecure 從伺服器端處理序 tooan MVC4 Web API REST 服務的服務呼叫。 |
| C#/.NET |[新增登入 tooYour Web 應用程式使用 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |設定.NET 應用程式 tooperform 網頁單一登入針對 Azure AD 企業目錄。 |
| C#/.NET |[使用 Azure AD 開發多租用戶 Web 應用程式](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |跨多個組織使用 Azure AD tooadd toohello 單一登入和目錄存取功能的一個.NET 應用程式 toowork。 |
| Java |[Azure AD Graph API 的 Java 範例應用程式](http://go.microsoft.com/fwlink/?LinkId=263969) |使用 hello 從 Azure AD Graph API tooaccess 目錄資料。 |
| PHP |[Azure AD Graph API 的 PHP 範例應用程式](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |使用 hello 從 Azure AD Graph API tooaccess 目錄資料。 |
| C#/.NET |[Azure AD Graph API 的範例應用程式](http://go.microsoft.com/fwlink/?LinkID=262648) |使用 hello 從 Azure AD Graph API tooaccess 目錄資料。 |
| C#/.NET |[Azure AD Graph 差異查詢的範例應用程式](http://go.microsoft.com/fwlink/?LinkId=275398) |Hello 差異查詢 hello Graph API tooget 定期變更 toouser 在物件中使用 Azure AD 租用戶中。 |
| C#/.NET |[整合 Azure AD 多租用戶雲端應用程式的範例應用程式](http://go.microsoft.com/fwlink/?LinkId=275397) |將多租用戶應用程式整合至 Azure AD。 |
| C#/.NET |[使用 Azure AD 保護 Windows 市集應用程式和 REST Web 服務](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |建立簡單的 web API 資源和 Windows 市集用戶端的應用程式，使用 Azure AD 和 hello [Azure AD 驗證程式庫 (ADAL)](active-directory-authentication-libraries.md)。 |
| C#/.NET |[使用 hello Graph API tooQuery Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |設定 Microsoft.NET 應用程式 toouse hello Azure AD 租用戶目錄的 Azure AD Graph API tooaccess 資料。 |

## <a name="see-also"></a>另請參閱
##### <a name="other-resources"></a>其他資源
[Azure Active Directory 開發人員指南](active-directory-developers-guide.md)

[Azure AD 圖形 API 的概念和參考](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Azure AD Graph API 協助程式程式庫](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
