---
title: "Azure Active Directory B2C：Facebook 設定 | Microsoft Docs"
description: "提供在受保護的 Azure Active Directory B2C 的應用程式中的 Facebook 帳戶註冊和登入 tooconsumers。"
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure Active Directory B2C： 提供與 Facebook 帳戶註冊和登入 tooconsumers
## <a name="create-a-facebook-application"></a>建立 Facebook 應用程式
toouse Facebook 中 Azure Active Directory (Azure AD) B2C 身分識別提供者，您需要 toocreate Facebook 應用程式和提供 hello 正確的參數。 您需要 Facebook 帳戶 toodo 此。 如果您沒有帳戶，您可以在 [https://www.facebook.com/](https://www.facebook.com/)上取得。

1. 移 toohello [Facebook 開發人員](https://developers.facebook.com/)網站並使用您的 Facebook 登入帳戶的認證。
2. 如果您尚未這樣做，您會需要 tooregister 身為 Facebook 開發人員。 toodo 此，依序按一下**註冊**（在 hello 右上角的 hello 頁面），接受 Facebook 的原則，並完成 hello 註冊步驟。
3. 按一下 我的應用程式，然後按一下新增應用程式。 
4. 在 hello 表單中，提供**顯示名稱**且有效**Contact Email**。
5. 按一下 [建立應用程式識別碼]。 這可能需要您 tooaccept Facebook 平台原則，並完成線上安全性檢查。
6. Hello 左欄中按一下**設定**，然後選取 **基本**如果尚未選取的話。
7. 選取一個**類別**。 
8. 按一下 [+ 新增平台]，然後選取 [網站]。
   
    ![Facebook - 設定](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - 設定 - 網站](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. 輸入`https://login.microsoftonline.com/`在 hello**網站 URL**欄位，然後按一下**儲存變更**hello hello 頁底端。
   
    ![Facebook - 網站 URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. 複製 hello 值**應用程式識別碼**。 按一下**顯示**和複製 hello 值**應用程式秘鑰**。 您將需要這兩種 tooconfigure Facebook 身分識別提供者，在您的租用戶。 **應用程式密碼**是重要的安全性認證。
   
    ![Facebook - 應用程式識別碼和應用程式密碼](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. 按一下**+ 加入產品**hello 左側瀏覽且然後 hello**設定**按鈕**Facebook 登入**。
   
    ![Facebook - Facebook 登入](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. 按一下**設定**上 hello 底下的右 nav **Facebook 登入**

    ![Facebook - Facebook 登入設定](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. 輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**有效的 OAuth 重新導向 Uri**欄位 hello**用戶端的 OAuth 設定**> 一節。 使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。 按一下**儲存變更**hello hello 頁底端。
    
    ![Facebook - OAuth 重新導向 URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake Facebook 應用程式可由 Azure AD B2C，您需要 toomake 公開使用它。 您可以按一下**應用程式檢閱**hello 左瀏覽並開啟 hello 切換 hello 頁面頂端的 hello 太**是**按一下**確認**。
    
    ![Facebook - App 公開](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>將 Facebook 設定為您租用戶中的身分識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入「Facebook」。
5. 按一下 [識別提供者類型]、選取 [Facebook]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello 應用程式識別碼和應用程式密碼 （的 hello 您稍早建立的 Facebook 應用程式) 中 hello**用戶端識別碼**和**用戶端密碼**分別欄位。
7. 按一下**確定**，然後按一下**建立**toosave Facebook 組態。

> [!NOTE]
> 加入**身分識別提供者**tooyour 租用戶不會修改現有的原則。 請記住您的原則 tooupdate 包含您剛才建立的 hello 身分識別提供者。
>