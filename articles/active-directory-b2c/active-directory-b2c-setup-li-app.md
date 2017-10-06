---
title: "Azure Active Directory B2C：LinkedIn 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers LinkedIn 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 LinkedIn 帳戶
## <a name="create-a-linkedin-application"></a>建立 LinkedIn 應用程式
toouse LinkedIn B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate LinkedIn 應用程式和提供 hello 正確的參數。 您需要 LinkedIn 帳戶 toodo 此。 如果您沒有該帳戶，您可以在 [https://www.linkedin.com/](https://www.linkedin.com/)上申請。

1. 移 toohello [LinkedIn 開發人員網站](https://www.developer.linkedin.com/)並以您 LinkedIn 的帳戶認證登入。
2. 按一下**我的應用程式**在 hello 頂端功能表列，然後按一下 [**建立應用程式**。
   
    ![LinkedIn - 新建應用程式](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. 在 [hello**建立新的應用程式**表單中，填寫 hello 相關資訊 (**公司名稱**，**名稱**，**描述**， **應用程式標誌 URL**，**應用程式使用**，**網站 URL**，**公司電子郵件**和**公司電話**).
4. 同意 toohello **LinkedIn API 的使用規定**按一下**送出**。
   
    ![LinkedIn - 註冊應用程式](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. 複製的 hello 值**用戶端識別碼**和**用戶端密碼**。 (您可以在 [驗證金鑰] 下方找到這些資訊)。您將需要這兩種 tooconfigure LinkedIn 身分識別提供者，在您的租用戶。
   
   > [!NOTE]
   > **用戶端密碼** 是重要的安全性認證。
   > 
   > 
6. 輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Url**欄位 (下**OAuth 2.0**)。 使用您的租用戶名稱 (例如 contoso.onmicrosoft.com) 來取代 **{tenant}**。 按一下 [新增]，然後按一下 [更新]。 hello **{tenant}**值會區分大小寫。
   
    ![LinkedIn - 設定應用程式](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>將 LinkedIn 設定為您租用戶中的識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入「LI」。
5. 按一下 [識別提供者類型]、選取 [LinkedIn]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello 用戶端識別碼和用戶端密碼的 hello LinkedIn 您稍早建立的應用程式。
7. 按一下**確定**，然後按一下 [**建立**toosave LinkedIn 組態。

