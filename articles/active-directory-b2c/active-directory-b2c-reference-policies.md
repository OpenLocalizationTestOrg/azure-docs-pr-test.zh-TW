---
title: "Azure Active Directory B2C：內建原則 | Microsoft Docs"
description: "在 Azure Active Directory B2C 的 hello 可延伸原則架構和如何主題 toocreate 各種原則類型"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C：內建原則


Azure Active Directory (Azure AD) B2C 的 hello 可延伸原則架構是 hello 服務 hello 核心強度。 原則可完整描述取用者身分識別體驗，例如註冊、登入或設定檔編輯。 比方說，註冊原則可讓您 toocontrol 行為藉由設定下列設定的 hello:

* 帳戶類型 （例如 Facebook 社交帳戶） 或本機帳戶，例如電子郵件地址，取用者可以使用 toosign hello 應用程式註冊
* 屬性 （例如，名字、 郵遞區號和鞋子尺寸） toobe hello 取用者從收集在註冊期間
* Azure Multi-Factor Authentication 的使用
* 註冊的所有頁面的 hello 外觀與風格
* 資訊 （資訊清單，以在權杖中宣告的形式） 的 hello 應用程式收到 hello 原則執行完成時

您可以在租用戶中建立多個不同類型的原則，並視需要在您的應用程式中使用。 原則可以跨應用程式重複使用。 這種彈性可讓開發人員 toodefine 或並不修改取用者身分識別體驗，幾乎不需要任何變更 tootheir 程式碼。

透過簡單的開發人員介面就可使用原則。 您的應用程式會使用標準 HTTP 驗證要求 （hello 要求中傳遞原則參數） 來觸發原則，並接收自訂的語彙基元為回應。 比方說，hello 唯一的差別，可以叫用註冊的原則，以及要求叫用的登入原則是使用 hello"p"查詢字串參數中的 hello 原則名稱：

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

如需 hello 原則架構的詳細資訊，請參閱[有關 Azure AD B2C 上 hello Enterprise Mobility and Security 部落格此部落格文章](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx)。

## <a name="create-a-sign-up-or-sign-in-policy"></a>建立註冊或登入原則

此原則可使用單一組態處理取用者註冊和登入經驗。 取用者會導致下 hello 正確的路徑 （註冊或登入） 視 hello 內容而定。 它也會說明 hello 內容 hello 應用程式將會收到在成功註冊或登入的語彙基元。Hello 註冊或登入原則的程式碼範例是[這裡](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。  建議您使用這個原則，而不要使用註冊原則和登入原則。  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>建立註冊原則

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>建立登入原則

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>建立設定檔編輯原則

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>建立密碼重設原則

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>如何將註冊或登入原則與密碼重設原則連結在一起？
當您建立的註冊或登入的原則 （使用本機帳戶） 時，您會看到**Forgot 密碼？** hello 經驗 hello 第一頁上的連結。 按一下此連結並不會自動觸發密碼重設原則。 

相反地，hello 錯誤碼** `AADB2C90118` **傳回 tooyour 應用程式。 您的應用程式必須透過叫用特定的密碼重設原則 toohandle 此錯誤碼。 如需詳細資訊，請參閱[示範 hello 方法將原則連結的範例](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI)。

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>應該使用註冊原則、登入原則還是註冊原則加上登入原則？
我們建議使用註冊原則或是登入原則，而不要使用註冊原則加上登入原則。  

hello 註冊或登入的原則都有更多能力比 hello 登入的原則。 它也可讓您自訂 toouse 頁面 UI，並有更佳的支援，以進行當地語系化。 

hello 登入原則建議，如果您不需要 toolocalize 您的原則，只需要次要的自訂功能的商標，而且想密碼重設內建於它。

## <a name="next-steps"></a>後續步驟
* [權杖、工作階段及單一登入組態](active-directory-b2c-token-session-sso.md)
* [在取用者註冊期間停用電子郵件驗證](active-directory-b2c-reference-disable-ev.md)

