---
title: "aaaAzure Active Directory v2.0 驗證程式庫 |Microsoft 文件"
description: "相容的用戶端程式庫與伺服器中介軟體程式庫，和相關程式庫、 來源和 hello Azure Active Directory v2.0 端點的範例連結。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Azure Active Directory v2.0 驗證程式庫
hello Azure Active Directory (Azure AD) v2.0 端點支援 hello 業界標準 OAuth 2.0 和 OpenID Connect 1.0 通訊協定。 您可以使用各種程式庫，從 Microsoft 及其他組織與 hello v2.0 端點。

當您建置的應用程式使用 hello v2.0 端點時，我們建議您使用通訊協定網域專家遵循安全性開發週期 (SDL) 方法，例如所撰寫的程式庫[hello 一個後面接著 Microsoft][Microsoft-SDL]. 如果您決定 toohand 程式碼支援的 hello 通訊協定時，我們建議您遵循 SDL 方法，請密切注意 toohello 安全性考量，每個通訊協定的 hello 標準規格中。

## <a name="types-of-libraries"></a>程式庫類型
Azure AD v2.0 適用於兩種程式庫類型︰

* **用戶端程式庫**。 原生用戶端和伺服器可用於用戶端程式庫 tooget 存取權杖呼叫資源，例如 Microsoft Graph。
* **伺服器中介軟體程式庫**。 Web 應用程式會使用伺服器中介軟體程式庫進行使用者登入。 Web 應用程式開發介面使用伺服器中介軟體程式庫 toovalidate 語彙基元原生用戶端或其他伺服器所傳送。

## <a name="library-support"></a>程式庫支援
當您使用 hello v2.0 端點時，您可以選擇任何標準相容的文件庫，因為它是重要的 tooknow 其中 toogo 支援。 問題和程式庫程式碼中的功能要求，請連絡 hello 程式庫的擁有者。 問題和在 hello 服務端的通訊協定實作的功能要求，請連絡 Microsoft。

程式庫的支援類型有兩種︰

* **Microsoft 支援**。 Microsoft 會提供這些程式庫的修正程式，並已完成這些程式庫的 SDL 審查評鑑。
* **相容**。 Microsoft 有基本案例中測試這些程式庫，並確認他們使用 hello v2.0 端點。 Microsoft 不提供這些程式庫的修正程式，且尚未審查這些程式庫。 問題和功能要求應該導向的 toohello 程式庫的開放原始碼專案。

Hello v2.0 端點所使用的媒體櫃清單，請參閱本文章中的 hello 下一節。


## <a name="microsoft-supported-client-libraries"></a>Microsoft 支援的用戶端程式庫

> [!IMPORTANT]
> hello MSAL 預覽文件庫都適合用在實際執行環境中使用。 我們提供 hello 相同的生產環境層級支援這些文件庫，如同我們做法我們目前的實際執行程式庫 (ADAL)。 Hello 預覽期間，我們可能會讓變更 toohello MSAL API 內部快取格式，而不另行通知，您將這些程式庫的其他機制所需 tootake 以及錯誤修正或增強功能。 這可能會影響您的應用程式。 例如，變更 toohello 快取格式可能會影響您的使用者，例如需要 toosign 中的一次。 您的程式碼時，應用程式開發介面變更可能需要您 tooupdate。 當我們提供 hello 公開上市版本，我們會要求您 tooupdate toohello 公開上市版本六個月內時，作為使用預覽撰寫應用程式程式庫版本可能無法再運作。

| 平台 | 程式庫 | 下載 | 原始程式碼 | 範例 | 參考
| --- | --- | --- | --- | --- | --- |
| .NET 用戶端、Windows 市集、UWP、Xamarin iOS 和 Android | MSAL .NET (預覽) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [傳統型應用程式](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (預覽) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [單一頁面應用程式](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS、macOS | MSAL (預覽) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [iOS 應用程式](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (預覽) | [hello 中央儲存機制](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Android 應用程式](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Microsoft 支援的伺服器中介軟體程式庫

| 平台 | 程式庫 | 下載 | 原始程式碼 | 範例 | 參考
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | OWIN OpenID Connect 中介軟體 |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[MVC 應用程式](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | 適用於 AzureAD 的 OWIN OAuth Bearer 中介軟體 |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | 適用於 .NET 4.5 的 JWT 處理常式 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | ASP.NET OpenID Connect 中介軟體 |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[ASP.NET 安全性 (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[MVC 應用程式 (英文)](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | ASP.NET OAuth Bearer 中介軟體 |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[ASP.NET 安全性 (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | 適用於 .NET Core 的 JWT 處理常式  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Web 應用程式](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>相容的用戶端程式庫
| 平台 | 程式庫名稱 | 測試的版本 | 原始程式碼 | 範例 |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[原生應用程式範例](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[原生應用程式範例](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>相容的伺服器中介軟體程式庫
| 平台 | 程式庫名稱 | 測試的版本 | 原始程式碼 | 範例 |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribe Java scribejava](https://github.com/scribejava/scribejava) | [3.2.0 版](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [hello PHP League oauth2 用戶端](https://github.com/thephpleague/oauth2-client) | [1.4.2 版](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |[Web 應用程式](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>相關內容
如需 Azure AD hello v2.0 端點的詳細資訊，請參閱 hello [Azure AD 應用程式模型 v2.0 概觀][AAD-App-Model-V2-Overview]。

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
