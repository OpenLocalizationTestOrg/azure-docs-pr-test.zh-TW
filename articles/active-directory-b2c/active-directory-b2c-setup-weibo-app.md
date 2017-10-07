---
title: "Azure Active Directory B2C：Weibo 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers Weibo 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 Weibo 帳戶

> [!NOTE]
> 這項功能處於預覽狀態。 請勿在生產環境中使用此識別提供者。
> 

## <a name="create-a-weibo-application"></a>建立 Weibo 應用程式

toouse Weibo B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Weibo 應用程式和提供 hello 正確的參數。 您需要 Weibo 帳戶 toodo 此。 如果您沒有帳戶，您可以取得在 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us) 上取得一個。

### <a name="register-for-hello-weibo-developer-program"></a>註冊 hello Weibo 開發人員計劃

1. 移 toohello [Weibo 開發人員入口網站](http://open.weibo.com/)並以您 Weibo 帳戶認證登入。
2. 登入之後，按一下您在 hello 右上角的顯示名稱。
3. 在 hello 下拉式清單中，選取 **编辑开发者信息**（編輯開發人員資訊）。
4. Hello 所需的資訊輸入 hello 表單，然後按一下**提交**（提交）。
5. 完成 hello 電子郵件驗證程序。
6. 移 toohello[身分識別驗證頁面](http://open.weibo.com/developers/identity/edit)。
7. Hello 所需的資訊輸入 hello 表單，然後按一下**提交**（提交）。

### <a name="register-a-weibo-application"></a>註冊 Weibo 應用程式

1. 移 toohello[新 Weibo 應用程式登錄頁面](http://open.weibo.com/apps/new)。
2. 輸入 hello 必要的應用程式資訊。
3. 按一下 [创建] \(建立)。
4. 複製的 hello 值**應用程式金鑰**和**應用程式秘鑰**。 稍後您將會需要此資訊。
5. 上傳所需的 hello 相片，然後輸入 hello 所需的資訊。
6. 按一下 [保存以上信息] \(儲存)。
7. 按一下 [高级信息] \(進階資訊)。
8. 按一下**编辑**（編輯） 下一步 toohello 欄位 OAuth2.0**授权设置**（重新導向 URL）。
9. 針對 OAuth2.0 [授权设置] \(重新導向 URL) 輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。 例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。
10. 按一下 [提交]。  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>在租用戶中將 Weibo 設為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "Weibo"。
5. 按一下 [識別提供者類型]、選取 [Weibo]，然後按一下 [確定]。
6. 按一下 [設定此識別提供者]。
7. 輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。
8. 輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。
9. 按一下**確定**，然後按一下**建立**toosave Weibo 組態。

