---
title: "Azure Active Directory B2C：要求存取權杖 | Microsoft Docs"
description: "這篇文章將示範如何 toosetup 用戶端應用程式，並取得存取權杖。"
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C︰要求存取權杖

存取權杖 (表示為**存取\_語彙基元**從 Azure AD B2C hello 回應中) 是一種安全性權杖的用戶端可以使用 tooaccess 資源都會受到[授權伺服器](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics)，例如 web API。 存取權杖以[Jwt](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens)包含 hello 預期之資源伺服器與 hello 授與權限 toohello 伺服器相關資訊。 在呼叫 hello 資源伺服器，hello 存取權杖中必須要有 hello HTTP 要求。

本文將討論 tooconfigure 用戶端應用程式和 web API 中的順序如何 tooobtain**存取\_語彙基元**。

> [!NOTE]
> **Azure AD B2C 不支援 Web API 鏈結 (代理者)。**
>
> 許多架構包含 web API 需要 toocall 另一個下游 web API，同時受到 Azure AD B2C。 這種情況下會在具有 web API 後端，依序呼叫的 Microsoft 線上服務，例如 hello Azure AD Graph API 的原生用戶端。
>
> 這個鏈結的 web API 」 案例可支援使用 OAuth 2.0 JWT Bearer 認證授與，否則為 hello 稱為 hello 代表的流程。 不過，hello 上-代表 」 流程目前尚未實作 Azure AD B2C 中。

## <a name="register-a-web-api-and-publish-permissions"></a>註冊 Web API 與發佈權限

要求存取權杖之前，首先需要 tooregister web API，並發佈 toohello 用戶端應用程式被授與的權限 （範圍）。

### <a name="register-a-web-api"></a>註冊 Web API

1. 在 [hello B2C 功能刀鋒視窗中 hello Azure 入口網站上，按一下 [**應用程式**。
1. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
1. 輸入**名稱**會描述應用程式 tooconsumers hello 應用程式。 例如，您可以輸入「Contoso API」。
1. 切換 hello**包括 web 應用程式 / web API**太切換**是**。
1. 輸入代表 hello 的任意值**回覆 Url**。 例如，輸入 `https://localhost:44316/`。 因為應用程式開發介面應該不會收到 hello 語彙基元直接從 Azure AD B2C hello 值並不重要。
1. 輸入 [應用程式識別碼 URI]。 這是用於您的 web API 的 hello 識別碼。 例如，在 hello 方塊中輸入 「 附註 」。 hello**應用程式識別碼 URI**將`https://{tenantName}.onmicrosoft.com/notes`。
1. 按一下**建立**tooregister 您的應用程式。
1. 按一下您剛才建立的 hello 應用程式，並複製 hello 全域唯一**應用程式用戶端識別碼**，您將使用您的程式碼中的更新版本。

### <a name="publishing-permissions"></a>發佈權限

您的應用程式呼叫 API 時，所需範圍，也就是類似 toopermissions。 舉例來說，「讀取」或「寫入」即是範圍。 假設您想要您的 web 或太 「 讀取 」 從 API 的原生應用程式。 您的應用程式會呼叫 Azure AD B2C，並要求存取權杖，提供存取 toohello 領域 「 讀取 」。 若要讓 Azure AD B2C tooemit 存取權杖，必須授與權限太 「 讀取 」 從 hello 特定 API 的 toobe hello 應用程式。 toodo，您的 API，首先必須 toopublish hello 「 讀取 」 的範圍。

1. 在 Azure AD B2C hello**應用程式**刀鋒視窗中，開啟 hello web API 應用程式 ("Contoso API 」)。
1. 按一下 [已發佈範圍]。 這是您用來定義 hello 權限 （領域） 可以授與 tooother 應用程式。
1. 視需要新增 [範圍值] \(例如「讀取」)。 依預設，會定義 hello"user_impersonation"範圍。 想要的話，也可以忽略此步驟。 在 [hello 輸入 hello 範圍的描述**領域名稱**資料行。
1. 按一下 [儲存] 。

> [!IMPORTANT]
> hello**領域名稱**hello hello 描述**範圍值**。 當使用 hello 範圍，請確定 toouse hello**範圍值**。

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>授與原生或 web 應用程式的權限 tooa web API

一旦應用程式開發介面設定的 toopublish 範圍，hello 用戶端應用程式需要 toobe 授與這些範圍透過 hello Azure 入口網站。

1. 瀏覽 toohello**應用程式**hello B2C 功能刀鋒視窗中的功能表。
1. 如果您還沒有用戶端應用程式 ([Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)或[原生用戶端](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app))，請註冊一個。 如果您是依照本指南為您的起始點，您將需要 tooregister 用戶端應用程式。
1. 按一下 [API 存取]。
1. 按一下 [新增]。
1. 選取您 web 應用程式開發介面和 hello 範圍 （權限） （您想要 toogrant。
1. 按一下 [確定] 。

> [!NOTE]
> Azure AD B2C 不會要求您的用戶端應用程式使用者同意。 相反地，所有同意都係由 hello 系統管理員，根據設定 hello 上面所述的應用程式之間的 hello 權限。 如果已撤銷的權限授與應用程式，所有使用者都已之前可以 tooacquire 該權限都將不再是無法 toodo 使。

## <a name="requesting-a-token"></a>要求權杖

Hello 用戶端應用程式要求存取 token 時，需要 toospecify hello 所需權限，在 hello**範圍**hello 要求參數。 比方說，toospecify hello**範圍值**「 讀取 」 hello API 具有 hello**應用程式識別碼 URI**的`https://contoso.onmicrosoft.com/notes`，hello 範圍會`https://contoso.onmicrosoft.com/notes/read`。 以下是範例的授權碼要求 toohello`/authorize`端點。

> [!NOTE]
> 目前，自訂網域並未和存取權杖一起受到支援。 您必須使用 tenantName.onmicrosoft.com 網域 hello 要求 URL 中。

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire 相同要求中 hello 的多個權限，您可以加入多個項目在單一的 hello**範圍**參數，以空格分隔。 例如：

解碼的 URL：

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

編碼的 URL：

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

您可能會要求比授與用戶端應用程式更多的資源範圍 (權限)。 當這種情況 hello 時，hello 呼叫將會成功，如果至少一項權限會授與。 hello 產生**存取\_語彙基元**必須填入唯一的 hello 權限成功授與它的"scp"宣告。

> [!NOTE] 
> 我們在 hello 不支援要求的權限，針對兩個不同的網頁資源相同的要求。 這種要求將會失敗。

### <a name="special-cases"></a>特殊案例

hello OpenID Connect 標準指定數個特殊的 「 範圍 」 值。 hello 太下列特殊領域代表 hello 權限 「 存取 hello 使用者設定檔 」:

* **openid**︰這會要求識別碼權杖
* **offline\_access**︰這會要求重新整理權杖 (使用[授權碼流程](active-directory-b2c-reference-oauth-code.md))。

如果 hello`response_type`中的參數`/authorize`要求包含`token`，hello`scope`參數必須包含至少一個資源的範圍 (以外`openid`和`offline_access`)，將被授與。 否則，hello`/authorize`要求將會終止與失敗。

## <a name="hello-returned-token"></a>傳回語彙基元的 hello

在 [已成功產生**存取\_語彙基元**(從任一 hello`/authorize`或`/token`端點)，hello 下列宣告會出現：

| 名稱 | 宣告 | 說明 |
| --- | --- | --- |
|對象 |`aud` |hello**應用程式識別碼**hello 單一資源的 hello 權杖授與存取權。 |
|Scope |`scp` |hello 權限授與 toohello 資源。 多個授與權限將會以空格隔開。 |
|授權的合作對象 |`azp` |hello**應用程式識別碼**起始 hello 要求 hello 用戶端應用程式。 |

當您的 API 收到 hello**存取\_語彙基元**，它必須[驗證 hello 權杖](active-directory-b2c-reference-tokens.md)hello 語彙基元的 tooprove 是真確的且 hello 正確宣告。

我們一定是開啟 toofeedback，以及建議 ！ 如果您有本主題的任何問題，請張貼的堆疊溢位使用 hello 標記['azure-ad b2c 的'](https://stackoverflow.com/questions/tagged/azure-ad-b2c)。 功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。

## <a name="next-steps"></a>後續步驟

* 使用 [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi) 建置 Web API
* 使用 [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) 建置 Web API
