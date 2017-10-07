---
title: "Azure Active Directory B2C：Twitter 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers Twitter 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure Active Directory B2C： 提供與 Twitter 帳戶註冊和登入 tooconsumers

> [!NOTE]
> 這項功能處於預覽狀態。
> 

## <a name="create-a-twitter-application"></a>建立 Twitter 應用程式
toouse Twitter 身分識別提供者，在 Azure Active Directory (Azure AD) B2C 中，您需要 toocreate Twitter 應用程式，並提供與 hello 正確的參數。 您需要 Twitter 開發人員帳戶 toodo 此。 如果您沒有該帳戶，您可以在 [https://dev.twitter.com/](https://dev.twitter.com/) 上申請。

1. 移 toohello [Twitter 開發人員網站](https://dev.twitter.com/)並以您的認證登入。
2. 按一下 工具和支援 底下的 我的應用程式，然後按一下建立新的應用程式。 
3. 在 hello 表單中，提供值給 hello**名稱**，**描述**，和**網站**。
4. Hello**回呼 URL**，輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。 請確定 tooreplace **{tenant}**與您的租用戶名稱 (例如，contosob2c.onmicrosoft.com)。
5. 檢查 hello 方塊 tooagree toohello**開發人員合約**按一下**建立應用程式 Twitter**。
6. Hello 應用程式建立之後，按一下**機碼和存取權杖**。
7. 複製 hello 值**取用者索引鍵**和**取用者秘密**。 您將需要這兩種 tooconfigure Twitter 身分識別提供者，在您的租用戶。

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>在租用戶中將 Twitter 設為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入「Twitter」。
5. 按一下 [識別提供者類型]、選取 [Twitter]，然後按一下 [確定]。
6. 按一下**設定此身分識別提供者**，然後輸入 hello Twitter**取用者索引鍵**hello**用戶端識別碼**和 hello Twitter**取用者秘密**hello**用戶端密碼**。
7. 按一下**確定**，然後按一下**建立**toosave Twitter 組態。

