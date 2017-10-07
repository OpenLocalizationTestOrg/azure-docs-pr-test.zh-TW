---
title: "概觀 - Azure AD B2C | Microsoft Docs"
description: "使用 Azure Active Directory B2C 開發取用者導向應用程式"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C︰將焦點放在您的應用程式，我們會擔心註冊和登入

Azure AD B2C 是適用於 Web 和行動應用程式的雲端身分識別管理解決方案。 它是高可用性的全域服務的縮放比例 toohundreds 數百萬個身分識別。 Azure AD B2C 建置於企業級安全平台，可確保您的應用程式、企業和客戶受到安全防護。

以最低組態，Azure AD B2C 可讓您的應用程式 tooauthenticate:

* **社交帳戶** (例如 Facebook、Google、LinkedIn 等等)
* **企業帳戶** (使用開放式標準通訊協定 OpenID Connect 或 SAML)
* **本機帳戶** (電子郵件地址和密碼，或使用者名稱和密碼)

## <a name="get-started"></a>開始使用

首先，取得自己的租用戶使用 hello 步驟中所述[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。

然後選擇應用程式開發案例：

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![行動和桌面應用程式](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />行動和桌面應用程式</center> | [概觀](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [概觀](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.js](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Single Page Apps](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Single Page Apps</center> | [概觀](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![Web API](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />Web API</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [呼叫 .NET Web API](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>新功能

回到這裡查看通常需未來變更 toohello Azure Active Directory B2C toolearn。 我們也會使用 @AzureAD 發佈任何更新的相關推文。

* 此外太 「 內建原則 」 的 （正式上市），hello [「 自訂原則 」](active-directory-b2c-overview-custom.md)功能現已推出公開預覽狀態。  自訂原則適用於需要控制他們的身分識別經驗的 hello 組合的身分識別專業人員。
* hello[存取權杖](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview)功能現已推出公開預覽狀態。
* 已經宣告[以歐洲為主的 Azure AD B2C 一般可用性](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/)目錄。
* 查看 [GitHub 上不斷成長的程式碼範例](https://github.com/Azure-Samples?q=b2c)程式庫！

## <a name="how-tooarticles"></a>如何 tooarticles

深入了解如何 toouse 特定 Azure Active Directory B2C 功能：

* 設定您要在取用者導向應用程式中使用的 [Facebook](active-directory-b2c-setup-fb-app.md)、[Google+](active-directory-b2c-setup-goog-app.md)、[Microsoft 帳戶](active-directory-b2c-setup-msa-app.md)、[Amazon](active-directory-b2c-setup-amzn-app.md) 和 [LinkedIn](active-directory-b2c-setup-li-app.md)。
* [使用您的取用者的自訂屬性 toocollect 資訊](active-directory-b2c-reference-custom-attr.md)。
* [在取用者導向應用程式中啟用 Azure Multi-Factor Authentication](active-directory-b2c-reference-mfa.md)。
* [設定取用者的自助式密碼重設](active-directory-b2c-reference-sspr.md)。
* [自訂 hello 的外觀及註冊、 登入在和其他消費者導向頁面](active-directory-b2c-reference-ui-customization.md)會由 Azure Active Directory B2C。
* [使用 hello Azure Active Directory Graph API tooprogrammatically 建立、 讀取、 更新和刪除取用者](active-directory-b2c-devquickstarts-graph-dotnet.md)Azure Active Directory B2C 租用戶中。

## <a name="next-steps"></a>後續步驟

這些連結是適合用來探索 hello 項服務：

* 請參閱 hello [Azure Active Directory B2C 定價資訊](https://azure.microsoft.com/pricing/details/active-directory-b2c/)。
* 檢閱 Azure Active Directory B2C 的[程式碼範例](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c)。 
* 取得說明的堆疊溢位，使用 hello [azure ad b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c)標記。
* 藉由提供您的想法[User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)，我們想要 toohear 它們 ！
* 檢閱 hello [Azure AD B2C 通訊協定參考](active-directory-b2c-reference-protocols.md)。
* 檢閱 hello [Azure AD B2C 語彙基元參考](active-directory-b2c-reference-tokens.md)。
* 讀取 hello [Azure Active Directory B2C 常見問題集](active-directory-b2c-faqs.md)。
* [提出 Azure Active Directory B2C 的支援要求](active-directory-b2c-support.md)。

## <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新

我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。

