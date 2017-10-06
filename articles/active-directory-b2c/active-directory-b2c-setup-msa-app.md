---
title: "Azure Active Directory B2C：Microsoft 帳戶設定 | Microsoft Docs"
description: "提供在受保護的 Azure Active Directory B2C 的應用程式中的 Microsoft 帳戶註冊和登入 tooconsumers。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure Active Directory B2C： 提供與 Microsoft 帳戶註冊和登入 tooconsumers
## <a name="create-a-microsoft-account-application"></a>建立 Microsoft 帳戶應用程式
身分識別提供者，在 Azure Active Directory (Azure AD) B2C 的 toouse Microsoft 帳戶，您需要 toocreate Microsoft 帳戶應用程式，並提供與 hello 正確的參數。 您需要 Microsoft 帳戶 toodo 此。 如果您沒有該帳戶，您可以在 [https://www.live.com/](https://www.live.com/)上申請。

1. 移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)並以您的 Microsoft 帳戶認證登入。
2. 按一下 [新增應用程式] 。
   
    ![Microsoft 帳戶 - 加入新的應用程式](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. 為應用程式提供 [名稱]，然後按一下 [建立應用程式]。
   
    ![Microsoft 帳戶 - 應用程式名稱](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. 複製 hello 值**應用程式識別碼**。您需要這些 tooconfigure Microsoft 帳戶身分識別提供者租用戶中。
   
    ![Microsoft 帳戶 - 應用程式識別碼](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. 按一下 [新增平台]，然後選擇 [Web]。
   
    ![Microsoft 帳戶 - 新增平台](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft 帳戶 - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. 輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**重新導向 Uri**欄位。 使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。
   
    ![Microsoft 帳戶 - 重新導向 URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. 按一下**產生新的密碼**下 hello**應用程式密碼**> 一節。 複製顯示在螢幕上的 hello 新密碼。 您需要這些 tooconfigure Microsoft 帳戶身分識別提供者租用戶中。 此密碼是重要的安全性認證。
   
    ![Microsoft 帳戶 - 產生新密碼](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft 帳戶 - 新密碼](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. 指出核取 hello 方塊**Live SDK 支援**下 hello**進階選項**> 一節。 按一下 [儲存] 。
   
    ![Microsoft 帳戶 - Live SDK 支援](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>將 Microsoft 帳戶於租用戶中設定為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "MSA"。
5. 按一下 [識別提供者類型]、選取 [Microsoft 帳戶]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello 應用程式識別碼和密碼的 hello 您稍早建立的 Microsoft 帳戶應用程式。
7. 按一下**確定**，然後按一下 [**建立**toosave 您的 Microsoft 帳戶設定。

