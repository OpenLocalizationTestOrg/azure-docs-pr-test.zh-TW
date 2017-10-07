---
title: "aaaAzure AD B2C |Microsoft 文件"
description: "您可以在 hello Azure Active Directory B2C 建置 hello 類型的應用程式。"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C：應用程式類型
Azure Active Directory (Azure AD) B2C 支援各種現代應用程式架構的驗證。 全部都根據 hello 業界標準通訊協定[OAuth 2.0](active-directory-b2c-reference-protocols.md)或[OpenID Connect](active-directory-b2c-reference-protocols.md)。 本文件簡要描述 hello 可以建置的應用程式類型，與 hello 語言或平台無關您偏好。 也可協助您了解 hello 高階案例才能[開始建置應用程式](active-directory-b2c-overview.md#get-started)。

## <a name="hello-basics"></a>hello 基本概念
使用 Azure AD B2C 每個應用程式必須在中註冊您[B2C 目錄](active-directory-b2c-get-started.md)透過 hello [Azure 入口網站](https://portal.azure.com/)。 hello 應用程式登錄程序會收集，並將幾個值 tooyour 應用程式：

* 可唯一識別應用程式的 **應用程式識別碼** 。
* A**重新導向 URI**可以使用的 toodirect 回應後 tooyour 應用程式。
* 案例特有的其他任何值。 如需詳細資訊，了解如何太[註冊應用程式](active-directory-b2c-app-registration.md)。

Hello 應用程式的註冊後，通訊與 Azure AD 傳送要求 Azure AD toohello v2.0 端點：

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

指定每個要求傳送 tooAzure AD B2C**原則**。 原則控制 Azure AD 的 hello 的行為。 您也可以使用這些端點 toocreate 一組高度可自訂的使用者體驗。 常見的原則包括註冊、登入和設定檔編輯原則。 如果您不熟悉原則，您應該閱讀 hello Azure AD B2C[可延伸原則架構](active-directory-b2c-reference-policies.md)繼續進行之前。

與 2.0 版端點的 hello 互動的每個應用程式遵循類似的高層級模式：

1. hello 應用程式會引導 hello 使用者 toohello v2.0 端點 tooexecute[原則](active-directory-b2c-reference-policies.md)。
2. hello 使用者完成 hello 原則根據 toohello 原則定義。
3. hello 應用程式會收到 hello v2.0 端點某種類型的安全性權杖。
4. hello 應用程式會使用 hello 安全性語彙基元 tooaccess 受保護的資訊或受保護的資源。
5. hello 資源伺服器會驗證 hello 安全性語彙基元 tooverify，授與存取權。
6. hello 應用程式會定期重新整理 hello 安全性權杖。

<!-- TODO: Need a page for libraries toolink too-->
這些步驟可能稍有根據您要建置的應用程式的 hello 類型會不同。 開放原始碼程式庫可以讓您解決 hello 詳細資料。

## <a name="web-apps"></a>Web 應用程式
對於裝載於伺服器且透過瀏覽器存取的 Web 應用程式 (包括 .NET、PHP、Java、Ruby、Python、Node.js)，Azure AD B2C 支援以 [OpenID Connect](active-directory-b2c-reference-protocols.md) 完成一切使用者體驗。 這包括登入、註冊和設定檔管理。 在 Azure AD B2C hello 實作中的 OpenID Connect，您 web 應用程式會藉由發出驗證要求 tooAzure AD 起始這些使用者的體驗。 hello 要求的 hello 結果是`id_token`。 這個安全性權杖表示 hello 使用者的身分識別。 它也提供的宣告 hello 表單中的 hello 使用者的相關資訊：

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

深入了解 hello 類型的權杖與宣告的可用 tooan 應用程式在 hello [B2C 權杖參照](active-directory-b2c-reference-tokens.md)。

在 Web 應用程式中，每次執行 [原則](active-directory-b2c-reference-policies.md) 會採用下列高階步驟：

![Web 應用程式泳道映像](./media/active-directory-b2c-apps/webapp.png)

驗證的 hello`id_token`使用接收自 Azure AD 的公開金鑰簽署金鑰是 hello 使用者足夠 tooverify hello 識別。 這也可以設定可以在後續頁面要求上的使用的 tooidentify hello 使用者工作階段 cookie。

toosee 此案例中的動作，再試一次的其中一個 hello web 應用程式登入程式碼範例中我們[開始使用 > 一節](active-directory-b2c-overview.md#get-started)。

加法 toofacilitating 簡單登入，在 web 伺服器應用程式可能也需要 tooaccess 後端 web 服務。 在此情況下，hello web 應用程式可以執行稍有不同[OpenID Connect 流程](active-directory-b2c-reference-oidc.md)和使用授權碼取得權杖和重新整理權杖。 此案例中所述 hello 下列[Web 應用程式開發介面 > 一節](#web-apis)。

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Web API
您可以使用 Azure AD B2C toosecure web 服務，例如您的應用程式 rest 式 web 應用程式開發介面。 Web Api 可以使用 OAuth 2.0 toosecure 其資料，使用語彙基元的內送 HTTP 要求時進行驗證。 hello 的 web API 的呼叫端將附加 hello 授權標頭的 HTTP 要求中的語彙基元：

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

hello web API 可以使用 hello 語彙基元 tooverify hello API 呼叫者的身分識別與 tooextract 資訊編碼 hello 權杖中的宣告中的 hello 呼叫端。 深入了解 hello 類型的權杖與宣告的可用 tooan 應用程式在 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。

> [!NOTE]
> Azure AD B2C 目前僅支援以各自已知的用戶端存取的 Web API。 例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。 完全支援這種架構。 可讓協力廠商用戶端，例如另一個 iOS 應用程式、 tooaccess hello 相同的 web API 目前不支援。 所有應用程式完整 hello 元件必須共用單一應用程式識別碼。
>
>

Web API 接收的權杖可以來自許多類型的應用程式，包括 Web 應用程式、桌面和行動應用程式、單一頁面應用程式、伺服器端精靈，以及其他 Web API。 Web 應用程式中呼叫 web API 的 hello 完整流程的範例如下：

![Web 應用程式 Web API 泳道映像](./media/active-directory-b2c-apps/webapi.png)

深入了解授權碼、 重新整理權杖和 hello 步驟來取得權杖，toolearn 閱讀 hello [OAuth 2.0 通訊協定](active-directory-b2c-reference-oauth-code.md)。

如何使用 Azure AD B2C 簽出 hello toosecure web API web 應用程式開發介面中的教學課程的 toolearn 我們[開始使用 > 一節](active-directory-b2c-overview.md#get-started)。

## <a name="mobile-and-native-apps"></a>行動和原生應用程式
在裝置，行動和桌面應用程式，例如安裝應用程式通常需要 tooaccess 後端服務或代表使用者的 web 應用程式開發介面。 您可以加入自訂身分識別管理體驗 tooyour 原生應用程式，並安全地呼叫後端服務使用 Azure AD B2C 和 hello [OAuth 2.0 授權碼流程](active-directory-b2c-reference-oauth-code.md)。  

此流程，在 hello 應用程式會執行[原則](active-directory-b2c-reference-policies.md)並接收`authorization_code`從 Azure AD 之後 hello 使用者完成 hello 原則。 hello`authorization_code`代表 hello 代表 hello 使用者目前登入應用程式的權限 toocall 後端服務。 hello 應用程式可以接著交換 hello`authorization_code`在 hello 幕後`id_token`和`refresh_token`。  hello 應用程式可以使用 hello `id_token` tooauthenticate tooa 後端中的 web API HTTP 要求。 它也可以使用 hello`refresh_token`新 tooget`id_token`舊何時到期。

> [!NOTE]
> Azure AD B2C 目前支援權杖，這是使用的 tooaccess 應用程式本身的後端 web 服務。 例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。 完全支援這種架構。 目前不支援可讓您的 iOS 應用程式 tooaccess 協力廠商 web API，使用 OAuth 2.0 存取權杖。 所有應用程式完整 hello 元件必須共用單一應用程式識別碼。
>
>

![原生應用程式泳道映像](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>目前的限制
Azure AD B2C 目前不支援下列類型的應用程式，hello，但是可以在 hello 藍圖。 

### <a name="daemonsserver-side-apps"></a>精靈/伺服器端應用程式
應用程式包含長時間執行的處理序，或沒有 hello 使用者存在，運作也需要 tooaccess 保護的資源，例如 web 應用程式開發介面的方法。 這些應用程式可驗證及使用 hello 應用程式的身分識別 （而非使用者的委派的識別），並使用 hello OAuth 2.0 用戶端認證流程取得的權杖。

Azure AD B2C 目前不支援此流程。 這些應用程式只有在互動式使用者流程發生之後，才取得權杖。

### <a name="web-api-chains-on-behalf-of-flow"></a>Web API 鏈結 (代理者流程)
許多架構包含 web API 需要 toocall 另一個下游 web API，其中同時受到 Azure AD B2C。 此案例常見於有 Web API 後端的原生用戶端。 然後，這會呼叫 Microsoft 線上服務，例如 hello Azure AD Graph API。

使用 hello OAuth 2.0 JWT bearer 認證授與，也稱為 hello 代表的流程，可以支援此鏈結的 web API 」 案例。  不過，hello 上-代表 」 流程目前尚未實作 Azure AD B2C hello 中。
