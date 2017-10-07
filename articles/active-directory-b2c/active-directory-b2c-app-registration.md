---
title: "Azure Active Directory B2C：應用程式註冊 | Microsoft Docs"
description: "如何 tooregister 您應用程式與 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C：註冊您的應用程式

本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。 當您完成時，使用 hello Azure B2C 租用戶中註冊您的應用程式。

## <a name="prerequisites"></a>必要條件

toobuild 接受取用者註冊和登入的應用程式，您必須先 tooregister hello 應用程式與 Azure Active Directory B2C 租用戶。 使用 hello 中所述的步驟，以取得自己的租用戶[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。

從 Azure AD B2C hello 刀鋒視窗 hello Azure 入口網站中建立的應用程式必須從 hello 管理相同的位置。 如果您編輯使用 PowerShell 或另一個入口網站的 hello B2C 應用程式，它們會變成不受支援，無法搭配 Azure AD B2C。 查看詳細資料中 hello[發生錯誤的應用程式](#faulted-apps)> 一節。 

## <a name="navigate-toob2c-settings"></a>瀏覽 tooB2C 設定

登入 toohello [Azure 入口網站](https://portal.azure.com/)為 hello hello B2C 租用戶的全域管理員。 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

選擇 [下一步] 步驟會依據您所註冊的 hello 應用程式類型：

* [註冊 Web 應用程式](#register-a-web-app)
* [註冊 Web API](#register-a-web-api)
* [註冊行動或原生應用程式](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>註冊 Web 應用程式

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

如果您的 Web 應用程式呼叫 Azure AD B2C 所保護的 Web API，請執行下列步驟：
   1. 建立應用程式密碼將 toohello**金鑰**刀鋒視窗，然後按一下 hello**產生金鑰** 按鈕。 請記下 hello**應用程式金鑰**值。 您可以使用 hello 值做為您的應用程式程式碼中的 hello 應用程式密碼。
   2. 按一下 [API 存取][新增] 並選取您的 Web API 和範圍 (權限)。

> [!NOTE]
> **應用程式密鑰** 是重要的安全性認證，應該適當地加以保護。
> 

[跳過**後續步驟**](#next-steps)

## <a name="register-a-web-api"></a>註冊 Web API

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

按一下**發行領域**tooadd 更範圍為必要。 依預設，會定義 hello"user_impersonation"範圍。 hello user_impersonation 範圍可讓其他應用程式 hello 能力 tooaccess 此應用程式開發介面代表 hello 登入的使用者。 如果您希望，可以移除 hello user_impersonation 範圍。

[跳過**後續步驟**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>註冊行動或原生應用程式

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[跳過**後續步驟**](#next-steps)

## <a name="limitations"></a>限制

### <a name="choosing-a-web-app-or-api-reply-url"></a>選擇 Web 應用程式或 API 回覆 URL

目前，會向 Azure AD B2C 的應用程式是有限的限制的 tooa 組回覆 URL 值。 hello 的回覆的 web 應用程式和服務的 URL 必須以 hello 配置開頭`https`，及所有回覆 URL 值都必須共用單一的 DNS 網域。 例如，您不能註冊具有下列其中一個回覆 URL 的 Web 應用程式︰

`https://login-east.contoso.com`

`https://login-west.contoso.com`

hello 註冊系統比較 hello 現有回覆 URL toohello DNS 名稱的 hello 回覆 URL，您要加入的 hello 整個 DNS 名稱。 如果其中一個 hello 下列條件成立，就會失敗 hello 要求 tooadd hello DNS 名稱：

* hello 整個 DNS 名稱的新回覆 URL hello 與 hello 現有的回覆 URL hello DNS 名稱不相符。
* 新回覆 URL hello hello 整個 DNS 名稱不是 hello 現有的回覆 URL 的子網域。

例如，如果 hello 應用程式會出現此回覆 URL:

`https://login.contoso.com`

您可以加入 tooit，像這樣：

`https://login.contoso.com/new`

在此情況下，hello DNS 名稱與完全相符。 或者，您可以這樣做：

`https://new.login.contoso.com`

在此情況下，您參照 login.contoso.com tooa DNS 子的網域。如果您想 toohave 已登入： east.contoso.com 與登入-west.contoso.com，如回覆 Url 的應用程式，您必須加入這些回覆 Url 順序如下：

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

您可以新增 hello 後面兩個，因為它們是子網域的第一個回覆 URL hello，contoso.com。

### <a name="choosing-a-native-app-redirect-uri"></a>選擇原生應用程式重新導向 URI

選擇行動/原生應用程式的重新導向 URI 時，有兩個重要的考量︰

* **唯一**: hello 配置 hello 重新導向 URI 應該是唯一的每個應用程式。 在我們的範例 (com.onmicrosoft.contoso.appname://redirect/path)，我們會使用 com.onmicrosoft.contoso.appname 為 hello 配置。 我們建議您遵循此模式。 如果兩個應用程式共用 hello 相同配置、 hello 使用者會看到 「 選擇應用程式 」 的對話方塊。 如果 hello 使用者選擇不正確，hello 登入將會失敗。
* **完成**︰重新導向 URI 必須有配置和路徑。 hello 路徑必須包含至少一個斜線之後 hello 網域 （例如，//contoso/ 運作和 //contoso 失敗）。

請確定沒有任何特殊字元像 hello 中的底線重新導向 uri。

### <a name="faulted-apps"></a>發生錯誤的應用程式

下列情況不得編輯 B2C 應用程式：

* 在其他應用程式管理入口網站上，例如[Azure 傳統入口網站](https://manage.windowsazure.com/)和[應用程式註冊入口網站](https://apps.dev.microsoft.com/)。
* 使用圖形 API 或 PowerShell

如果您編輯 hello B2C 應用程式，如上面所述，然後再次嘗試 tooedit 再次在 hello Azure AD B2C 功能刀鋒視窗上 hello Azure 入口網站、 它會變成錯誤的應用程式，和您的應用程式就不能再使用 Azure AD B2C。 您擁有 toodelete hello 應用程式，並且建立一次。

toodelete hello 應用程式，請移 toohello[應用程式註冊入口網站](https://apps.dev.microsoft.com/)並刪除那里 hello 應用程式。 為了讓 hello 應用程式 toobe 可見，您需要 toobe hello 的擁有者 hello 應用程式 （和不只是 hello 租用戶的系統管理員）。

## <a name="next-steps"></a>後續步驟

現在，您已經向 Azure AD B2C 應用程式，您可以完成其中一種[我們的快速入門教學課程](active-directory-b2c-overview.md#get-started)tooget 啟動並執行。

> [!div class="nextstepaction"]
> [透過註冊、登入和密碼重設來建立 ASP.NET Web 應用程式](active-directory-b2c-devquickstarts-web-dotnet-susi.md)