---
title: "Azure Active Directory B2C：QQ 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers QQ 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 QQ 帳戶

> [!NOTE]
> 這項功能處於預覽狀態。
> 

## <a name="create-a-qq-application"></a>建立 QQ 應用程式

toouse QQ B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate QQ 應用程式和提供 hello 正確的參數。 您需要 QQ 帳戶 toodo 此。 如果您沒有帳戶，您可以在 [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033) 上取得一個。

### <a name="register-for-hello-qq-developer-program"></a>註冊 hello QQ 開發人員計劃

1. 移 toohello [QQ 開發人員入口網站](http://open.qq.com)並以您 QQ 帳戶認證登入。
2. 登入之後，請移過[http://open.qq.com/reg](http://open.qq.com/reg) tooregister 自行身為開發人員。
3. 在 [hello] 功能表中，選取 [**个人**（個別開發人員）。
4. Hello 所需的資訊輸入 hello 表單，然後按一下**庫**（下一個步驟）。
5. 完成 hello 電子郵件驗證程序。

> [!NOTE]
> 您將需要核准身為開發人員註冊之後的幾天 toobe toowait。 

### <a name="register-a-qq-application"></a>註冊 QQ 應用程式

1. 跳過[https://connect.qq.com/index.html](https://connect.qq.com/index.html)。
2. 按一下 [应用管理] \(應用程式管理)。
3. 按一下 [创建应用] \(建立應用程式)。
4. 輸入 hello 必要的應用程式資訊。
5. 按一下 [创建应用] \(建立應用程式)。
6. 輸入 hello 所需的資訊。
7. Hello**授权回调域**(回呼 URL) 欄位中，輸入`https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。 例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。
8. 按一下 [创建应用] \(建立應用程式)。
9. 在 [hello] 確認頁面上，按一下**应用管理**（應用程式管理） tooreturn toohello 應用程式管理頁面。
10. 按一下**查看**您剛建立 （檢視） 下一步 toohello 應用程式。
11. 按一下 [修改] \(編輯)。
12. 從 hello hello 頁面頂端，複製 [hello**應用程式識別碼**和**應用程式金鑰**。

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>在租用戶中將 QQ 設為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "QQ"。
5. 按一下 [識別提供者類型]、選取 [QQ]，然後按一下 [確定]。
6. 按一下 [設定此識別提供者]。
7. 輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。
8. 輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。
9. 按一下**確定**，然後按一下 [**建立**toosave QQ 組態。

