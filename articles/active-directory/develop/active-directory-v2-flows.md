---
title: "hello Azure Active Directory v2.0 端點 aaaApp 類型 |Microsoft 文件"
description: "hello 類型的應用程式和 hello Azure Active Directory v2.0 端點所支援的案例。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Hello Azure Active Directory v2.0 端點的應用程式類型
hello Azure Active Directory (Azure AD) v2.0 端點支援驗證的各種不同的現代化應用程式架構，全部都根據業界標準通訊協定[OAuth 2.0 或 OpenID Connect](active-directory-v2-protocols.md)。 本文說明 hello 種您可以使用 Azure AD v2.0，不論您偏好的語言或平台建置的應用程式。 hello 這篇文章中的資訊是您了解高階案例才能設計的 toohelp[開始 hello 程式碼的使用](active-directory-appmodel-v2-overview.md#getting-started)。

> [!NOTE]
> hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。 toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## <a name="hello-basics"></a>hello 基本概念
您必須註冊每個應用程式中，使用 hello v2.0 端點 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com)。 hello 應用程式登錄程序會收集，並將您的應用程式的這些值：

* 可唯一識別應用程式的「應用程式識別碼」
* A**重新導向 URI** ，您可以使用 toodirect 回應後 tooyour 應用程式
* 一些其他案例特定值

如需詳細資訊，了解如何太[註冊應用程式](active-directory-v2-app-registration.md)。

Hello 應用程式註冊之後，hello 應用程式將會傳送要求 Azure AD toohello v2.0 端點通訊與 Azure AD。 我們提供開放原始碼架構和處理這些要求的 hello 詳細資料的程式庫。 您也可以 hello 選項 tooimplement hello 驗證邏輯自行建立要求 toothese 端點：

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Web 應用程式
針對 web 應用程式 （.NET、 PHP、 Java、 Ruby、 Python、 節點） 的 hello 透過瀏覽器的使用者存取，您可以使用[OpenID Connect](active-directory-v2-protocols.md)使用者登入。 在 OpenID Connect，hello web 應用程式接收的 ID 語彙基元。 ID 權杖是安全性權杖驗證 hello 使用者的身分識別，並提供 hello 形式的宣告中的 hello 使用者的相關資訊：

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

您可以了解的權杖與宣告的 hello 可用 tooan 應用程式的所有 hello 類型[v2.0 權杖參考](active-directory-v2-tokens.md)。

在 web 伺服器應用程式，hello 登入驗證流程會採用下列高階步驟：

![Web 應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

您可以使用收到來自 hello v2.0 端點公開簽署金鑰驗證 hello 的 ID 語彙基元，以確保 hello 使用者的身分識別。 已設定的工作階段 cookie，可能會在後續頁面要求上的使用的 tooidentify hello 使用者。

toosee 此案例中的動作，再試一次一個 hello web 應用程式登入程式碼範例中我們 v2.0[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。

此外 toosimple 登入，web 伺服器應用程式可能需要 tooaccess 另一個 web 服務，例如 REST API。 在此情況下，hello web 伺服器應用程式會結合 OpenID Connect 和 OAuth 2.0 資料流程，使用 hello [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)。 如需有關此案例的詳細資訊，請參閱[開始使用 Web 應用程式和 Web API](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)。

## <a name="web-apis"></a>Web API
您可以使用 hello v2.0 端點 toosecure web 服務，例如您的應用程式 RESTful Web API。 而不是 ID 語彙基元和工作階段 cookie，Web API 所使用的 OAuth 2.0 存取權杖 toosecure 其資料和 tooauthenticate 連入要求。 hello Web api 的呼叫端將附加 hello 的 HTTP 要求，就像這樣的授權標頭中的存取權杖：

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

hello Web API 會使用有關 hello 呼叫端被編碼 hello 存取權杖中的宣告中的 hello 存取語彙基元 tooverify hello API 呼叫者的身分識別與 tooextract 資訊。 toolearn hello 類型的權杖與宣告的可用 tooan 應用程式，請參閱 hello [v2.0 權杖參考](active-directory-v2-tokens.md)。

Web API 可以提供使用者 hello 電源 tooopt 或退出特有的功能或資料所公開的權限，也稱為[範圍](active-directory-v2-scopes.md)。 呼叫應用程式 tooacquire 權限 tooa 範圍，hello 使用者必須同意 toohello 範圍流程期間。 hello v2.0 端點 hello 使用者要求權限，而且然後權限中記錄所有存取權杖 Web 應用程式開發介面會接收該 hello。 hello Web API 驗證 hello 存取權杖，它在每個呼叫上接收及執行授權檢查。

Web API 可以從所有類型的應用程式接收存取權杖，包括 Web 伺服器應用程式、傳統型應用程式和行動應用程式、單頁應用程式、伺服器端精靈，甚至是其他的 Web API。 Web API 的 hello 高階流程看起來像這樣：

![Web API 驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn 如何 toosecure Web API 使用 OAuth2 存取權杖，簽出 hello Web API 的程式碼範例中我們[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。

在許多情況下，web 應用程式開發介面，也需要 toomake 輸出 tooother 下游 web Api 受到 Azure Active Directory 的要求。  toodo，web Api 可以利用 Azure AD 的**上代表的**流程，可讓 hello web API tooexchange 另一個用於輸出要求存取權杖 toobe 的傳入存取權杖。  hello v2.0 端點的流量代表述[詳](active-directory-v2-protocols-oauth-on-behalf-of.md)。

## <a name="mobile-and-native-apps"></a>行動和原生應用程式
裝置安裝的應用程式，例如行動及桌面應用程式，通常需要 tooaccess 後端服務或 Web Api，將資料儲存和執行代表使用者的功能。 這些應用程式可以使用 hello 新增登入和授權 tooback 後端服務[OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)。

在此流程中，hello 應用程式授權程式碼從 hello v2.0 端點時收到 hello 使用者登入。 hello 授權碼代表 hello hello 使用者身分登入應用程式的權限 toocall 後端服務。 hello 應用程式可以交換 hello hello 背景的 OAuth 2.0 存取權杖和重新整理權杖的授權碼。 hello 應用程式可以使用 hello 存取語彙基元 tooauthenticate tooWeb 在 HTTP 要求中，應用程式開發介面，並使用 hello 重新整理語彙基元 tooget 新存取權杖，較舊的存取權杖到期時間。

![原生應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>單頁應用程式 (JavaScript)
許多新式應用程式都有一個單頁應用程式前端，主要是以 JavaScript 撰寫。 通常是使用 AngularJS、Ember.js、Durandal.js 等架構來撰寫它們。 hello Azure AD v2.0 端點支援這些應用程式使用 hello [OAuth 2.0 隱含流程](active-directory-v2-protocols-implicit.md)。

Hello 應用程式在此流程中，直接從 hello 接收權杖 v2.0 授權端點，沒有任何伺服器對伺服器交換。 所有的驗證邏輯和工作階段處理會置於完全 hello JavaScript 用戶端，沒有額外的頁面重新導向。

![隱含驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee 此案例中的動作，再試一次的其中一個 hello 單一頁面應用程式程式碼範例中我們[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。

## <a name="daemons-and-server-side-apps"></a>精靈和伺服器端應用程式
應用程式具有長時間執行的程序或運作而不需與使用者互動所也需要 tooaccess 保護的資源，例如 Web 應用程式開發介面的方法。 這些應用程式可驗證及使用 hello 應用程式識別來取得權杖而非使用者的委派識別 hello OAuth 2.0 用戶端認證流程。

此流程，hello 應用程式會直接與 hello 互動`/token`端點 tooobtain 端點：

![精靈應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild 的精靈應用程式，請參閱中的 hello 用戶端認證文件我們[入門](active-directory-appmodel-v2-overview.md#getting-started)區段，或嘗試[.NET 範例應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)。
