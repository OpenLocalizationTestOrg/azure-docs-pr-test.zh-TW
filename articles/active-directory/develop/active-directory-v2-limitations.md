---
title: "Active Directory aaaAzure v2.0 端點限制事項 |Microsoft 文件"
description: "限制 hello Azure AD v2.0 端點事項的清單。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>應該使用 hello v2.0 端點？
當您建置與 Azure Active Directory 整合的應用程式時，您會需要 toodecide 是否 hello v2.0 端點和驗證通訊協定符合您的需求。 Azure Active Directory 的原始端點仍受到完整的支援，而且在某些方面擁有比 v2.0 更豐富的功能。 不過，hello v2.0 端點[導入了重要的優點](active-directory-v2-compare.md)適用於開發人員。

以下是我們在這個時間點針對開發人員所提供的簡化建議：

* 如果您必須支援個人 Microsoft 帳戶應用程式中，使用 hello v2.0 端點。 但是，這麼做之前，請務必了解我們在本文中討論的 hello 限制。
* 如果您的應用程式只需要 toosupport Microsoft 工作及學校帳戶，不要使用 hello v2.0 端點。 請改為參考 tooour [Azure AD 開發人員指南](active-directory-developers-guide.md)。

經過一段時間，以便只需要 toouse hello v2.0 端點 hello v2.0 端點時，將會成長此處列出，tooeliminate hello 限制。 同時，在 hello 這篇文章是預定的 toohelp 您決定 hello v2.0 端點是最適合您。 我們將繼續 tooupdate hello v2.0 端點此發行項 tooreflect hello 目前狀態。 核取回 tooreevaluate v2.0 功能對您的需求。

如果您有現有的 Azure AD 應用程式不會使用 hello v2.0 端點，則從頭沒有需要 toostart。 在 hello 未來，我們會提供一種您 toouse hello v2.0 端點與現有的 Azure AD 應用程式。

## <a name="restrictions-on-app-types"></a>應用程式類型的限制
目前，hello 下列類型的應用程式不支援 hello v2.0 端點。 如需支援的應用程式類型的說明，請參閱[hello Azure Active Directory v2.0 端點的應用程式類型](active-directory-v2-flows.md)。

### <a name="standalone-web-apis"></a>獨立的 Web API
您也可以使用 hello v2.0 端點[建置 OAuth 2.0 保護 Web API](active-directory-v2-flows.md#web-apis)。 不過，該 Web 應用程式開發介面可以語彙基元僅接收的應用程式，具有 hello 相同應用程式識別碼。 您無法從具有不同「應用程式識別碼」的用戶端存取 Web API。 hello 用戶端不會是能 toorequest，或者取得權限 tooyour Web API。

如何 toobuild Web API 可接受來自用戶端發出權杖 hello 相同的應用程式識別碼，請參閱的 toosee hello v2.0 端點 Web API 範例中的我們[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。

## <a name="restrictions-on-app-registrations"></a>應用程式註冊的限制
目前，您想與 hello v2.0 端點 toointegrate 每個應用程式中，您必須建立應用程式註冊在 hello 新[Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。 現有的 Azure AD 或 Microsoft 帳戶應用程式不相容與 hello v2.0 端點。 Hello 應用程式註冊入口網站以外的任何入口網站中註冊應用程式不相容與 hello v2.0 端點。 在 hello 未來，我們計劃 tooprovide 方式 toouse v2.0 應用程式現有的應用程式。 目前，不過，現有的應用程式 toowork 與 hello v2.0 端點沒有移轉路徑。

此外，您在 hello 中建立的應用程式註冊[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)擁有 hello 下列注意事項：

* 每個「應用程式識別碼」只允許兩個應用程式密碼。
* 由使用個人 Microsoft 帳戶之使用者所註冊的應用程式註冊，只能透過單一開發人員帳戶來檢視及管理。 不能在多位開發人員之間共用。  如果您想要 tooshare 多位開發人員在您的應用程式註冊，您可以建立 hello 應用程式登入 hello 註冊入口網站與 Azure AD 帳戶。
* 有幾項限制的 hello 重新導向 URI 允許 hello 格式。 如需有關重新導向 Uri 的詳細資訊，請參閱 hello 下一節。

## <a name="restrictions-on-redirect-uris"></a>重新導向 URI 的限制
目前，hello 應用程式註冊入口網站中註冊應用程式是有限的限制的 tooa 組重新導向 URI 值。 hello 重新導向的 web 應用程式和服務 URI 的開頭必須 hello 配置`https`，以及重新導向 URI 的所有值都必須都共用單一的 DNS 網域。 例如，您不能註冊具有下列其中一個重新導向 URI 的 Web 應用程式：

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

hello 註冊系統比較 hello 現有重新導向 URI toohello DNS 名稱的 hello 重新導向 URI，您要加入 hello 整個 DNS 名稱。 如果其中一個 hello 下列條件成立，hello 要求 tooadd hello DNS 名稱將會失敗：  

* hello 新重新導向 URI 的 hello 整個 DNS 名稱與 hello 現有重新導向 URI hello DNS 名稱不相符。
* hello 新重新導向 URI 的 hello 整個 DNS 名稱不是 hello 現有重新導向 URI 的子網域。

例如，如果 hello 應用程式具有此重新導向 URI:

`https://login.contoso.com`

您可以加入 tooit，像這樣：

`https://login.contoso.com/new`

在此情況下，hello DNS 名稱與完全相符。 或者，您可以這樣做：

`https://new.login.contoso.com`

在此情況下，您參照 login.contoso.com tooa DNS 子的網域。如果您想 toohave 已登入 east.contoso.com 與登入-west.contoso.com 新增為重新導向 Uri 的應用程式，您必須加入這些重新導向 Uri 依此順序：

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

您可以新增 hello 後面兩個因為它們是子網域的 hello 第一次重新導向 URI，contoso.com。即將推出的版本將會移除這項限制。

toolearn tooregister hello 應用程式註冊入口網站，在應用程式如何查看[如何 tooregister 應用程式，但 hello v2.0 端點](active-directory-v2-app-registration.md)。

## <a name="restrictions-on-services-and-apis"></a>服務和 API 的限制
登入 hello v2.0 端點支援 hello 應用程式註冊入口網站中登錄和其落在 hello 清單中的任何應用程式目前[支援驗證流程](active-directory-v2-flows.md)。 不過，這些應用程式只能取得非常有限的一組資源的 OAuth 2.0 存取權杖。 hello v2.0 endpoint 問題存取語彙基元僅適用於：

* 要求 hello 語彙基元的 hello 應用程式。 如果 hello 邏輯應用程式由數個不同的元件或層構成應用程式可以為其本身，取得存取權杖。 toosee 此案例中的動作，請參閱我們[入門](active-directory-appmodel-v2-overview.md#getting-started)教學課程。
* hello Outlook 郵件、 行事曆和連絡人的 REST Api，均位於 https://outlook.office.com。toolearn 如何 toowrite 應用程式存取這些 Api，請參閱 hello [Office 入門](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2)教學課程。
* Microsoft Graph API。 您可以深入了解[Microsoft Graph](https://graph.microsoft.io)和可用 tooyou hello 資料。

目前不支援其他服務。 多個 Microsoft Online Services 中將新增 hello 未來，此外 toosupport 您自己自訂的 Web Api 和服務。

## <a name="restrictions-on-libraries-and-sdks"></a>程式庫和 SDK 的限制
目前，媒體櫃 hello v2.0 端點受到支援。 如果您想 toouse hello v2.0 端點，生產環境應用程式中的，您會有下列選項：

* 如果您要建置的 web 應用程式，您可以安全地使用 Microsoft 廣泛地供伺服器端的中介軟體 tooperform 登入和權杖驗證。 這些適用於 ASP.NET 和 hello Node.js Passport 外掛程式包括 hello OWIN 開啟的 ID 連線中介軟體。 如需使用 Microsoft 中介軟體的程式碼範例，請參閱我們的[開始使用](active-directory-appmodel-v2-overview.md#getting-started)一節。
* 如果您正在建置傳統型或行動應用程式，可以使用我們的其中一個預覽 Microsoft Authentication Library (MSAL)。  這些程式庫是在生產環境支援預覽中，因此它是安全的 toouse 實際執行應用程式中。 Hello 使用條款 hello 預覽，以及 hello 可用程式庫中的，您可以閱讀我們[驗證程式庫參考](active-directory-v2-libraries.md)。
* 對於未涵蓋的 Microsoft 文件庫平台，您可以透過直接傳送和接收應用程式程式碼中的通訊協定訊息整合與 hello v2.0 端點。 hello v2.0 OpenID Connect 和 OAuth 通訊協定[明確地記載](active-directory-v2-protocols.md)toohelp 您執行這類的整合。
* 最後，您可以使用開放原始碼開啟 ID 連線和 OAuth 文件庫 toointegrate 與 hello v2.0 端點。 hello v2.0 通訊協定應該相容與不需要主要變更許多開放原始碼通訊協定文件庫。 這類程式庫的 hello 可用性會因語言與平台而異。 hello[開啟連接的識別碼](http://openid.net/connect/)和[OAuth 2.0](http://oauth.net/2/)網站維護一份受歡迎的實作。 如需詳細資訊，請參閱[Azure Active Directory v2.0 和驗證程式庫](active-directory-v2-libraries.md)，和 hello 的開放原始碼用戶端程式庫和範例，讓測試過與 hello v2.0 端點的清單。

## <a name="restrictions-on-protocols"></a>通訊協定的限制
hello v2.0 端點不支援 SAML 或 Ws-federation;它僅支援開啟連接的識別碼和 OAuth 2.0。  並非所有功能和 OAuth 通訊協定的功能已都納入 hello v2.0 端點。 這些通訊協定功能目前是*無法使用*hello v2.0 端點中：

* 不包含 ID 權杖所發出的 hello v2.0 端點`email`hello 使用者宣告，即使他們的電子郵件取得 hello 使用者 tooview 權限。
* hello OpenID 連接的使用者資訊端點未實作 hello v2.0 端點上。 不過，您可能會收到此端點上的所有使用者設定檔資料都，可以從 Microsoft Graph hello`/me`端點。
* hello v2.0 端點不支援 ID 語彙基元中發行的角色或群組宣告。
* hello [OAuth 2.0 資源擁有者密碼認證授與](https://tools.ietf.org/html/rfc6749#section-4.3)hello v2.0 端點不支援。

除了上述外，hello v2.0 端點不支援任何形式的 hello SAML 或 Ws-federation 通訊協定。

toobetter 了解 hello 範圍通訊協定支援的功能在 hello v2.0 端點，請閱讀我們[OpenID Connect 和 OAuth 2.0 通訊協定參考](active-directory-v2-protocols.md)。

## <a name="restrictions-for-work-and-school-accounts"></a>工作和學校帳戶的限制
如果您在 Windows 應用程式使用 Active Directory 驗證程式庫 (ADAL)，您可能已由 Windows 整合式驗證，使用 hello 安全性聲明標記語言 (SAML) 判斷提示授與的優點。 有了此授與之後，同盟 Azure AD 租用戶的使用者便可向其內部部署 Active Directory 執行個體以無訊息方式進行驗證，而不需輸入認證。 目前，hello v2.0 端點上不支援 hello SAML 判斷提示授與。
