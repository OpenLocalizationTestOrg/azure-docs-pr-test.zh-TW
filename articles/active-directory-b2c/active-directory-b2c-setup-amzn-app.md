---
title: "Azure Active Directory B2C：Amazon 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers Amazon 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 Amazon 帳戶
## <a name="create-an-amazon-application"></a>建立 Amazon 應用程式
toouse Amazon B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Amazon 應用程式和提供 hello 正確的參數。 您需要 Amazon 帳戶 toodo 此。 如果您沒有帳戶，您可以在 [http://www.amazon.com/](http://www.amazon.com/)上取得。

1. 移 toohello [Amazon 開發人員中心](https://login.amazon.com/)並以您的 Amazon 帳戶認證登入。
2. 如果您尚未這樣做，請按一下**註冊**、 遵循 hello 開發人員註冊的步驟，以及接受 hello 原則。
3. 按一下 [註冊新應用程式] 。
   
    ![註冊新的應用程式在 hello Amazon 網站](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. 提供應用程式資訊 (**名稱**、**說明**和**隱私權注意事項 URL**)，然後按一下 [儲存]。
   
    ![提供應用程式資訊以便在 Amazon 上註冊新的應用程式](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. 在 hello **Web 設定**區段，複製 hello 值**用戶端識別碼**和**用戶端密碼**。 (您需要 tooclick hello**顯示密碼**這按鈕 toosee。)您需要這兩種 tooconfigure Amazon 身分識別提供者，在您的租用戶。 按一下**編輯**底部 hello hello > 一節。 **用戶端密碼** 是重要的安全性認證。
   
    ![針對您在 Amazon 上的新應用程式提供用戶端識別碼和用戶端密碼](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. 輸入`https://login.microsoftonline.com`在 hello**允許 JavaScript Origins**欄位和`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**允許傳回 Url**欄位。 使用您的租用戶名稱 (例如 contoso.onmicrosoft.com) 來取代 **{tenant}**。 按一下 [儲存] 。 hello **{tenant}**值會區分大小寫。
   
    ![針對您在 Amazon 上的新應用程式提供 JavaScript 原始來源及傳回 URL](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>將 Amazon 設為您租用戶中的身分識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "Amzn"。
5. 按一下 [識別提供者類型]、選取 [Amazon]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello 用戶端識別碼和用戶端密碼的 hello 您稍早建立的 Amazon 應用程式。
7. 按一下**確定**，然後按一下**建立**toosave Amazon 組態。

