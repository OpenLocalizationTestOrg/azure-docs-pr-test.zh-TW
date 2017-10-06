---
title: "Azure Active Directory B2C：Google+ 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers 與 Google + 應用程式保護 Azure Active Directory B2C 的帳戶。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active Directory B2C： 提供與 Google + 帳戶註冊和登入 tooconsumers
## <a name="create-a-google-application"></a>建立 Google+ 應用程式
toouse Google + B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Google + 應用程式和提供 hello 正確的參數。 您需要 Google + 帳戶 toodo 此。 如果您沒有該帳戶，您可以在 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)上申請。

1. 移 toohello [Google 開發人員主控台](https://console.developers.google.com/)並以您的 Google + 帳戶認證登入。
2. 按一下 [建立專案]，輸入 [專案名稱]，接著按一下 [建立]。
   
    ![Google+ - 開始使用](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - 新增專案](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. 按一下**API Manager** ，然後按一下 [**認證**在 hello 左瀏覽。
4. 按一下 hello **OAuth 同意畫面**hello 頂端的索引標籤。
   
    ![Google+ - 認證](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. 選取或指定有效的**電子郵件地址**、提供**產品名稱**，然後按一下 [儲存]。
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. 按一下 [新增認證]，然後選擇 [OAuth 用戶端識別碼]。
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. 在 [應用程式類型] 下方，選取 [Web 應用程式]。
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. 提供**名稱**針對您的應用程式中，輸入`https://login.microsoftonline.com`在 hello**授權 JavaScript origins**欄位，和`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Uri**欄位。 使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。 hello **{tenant}**值會區分大小寫。 按一下 [建立] 。
   
    ![Google+ -  建立用戶端識別碼](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. 複製的 hello 值**用戶端識別碼**和**用戶端密碼**。 您將需要這兩種 tooconfigure Google + 身分識別提供者，在您的租用戶。 **用戶端密碼** 是重要的安全性認證。
   
    ![Google+ - 用戶端密碼](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>將 Google+ 帳戶於租用戶中設定為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "G+"。
5. 按一下 [識別提供者類型]、選取 [Google]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello 用戶端識別碼和用戶端密碼 hello Google + 應用程式，您稍早建立。
7. 按一下**確定**，然後按一下 [**建立**toosave Google + 設定。

