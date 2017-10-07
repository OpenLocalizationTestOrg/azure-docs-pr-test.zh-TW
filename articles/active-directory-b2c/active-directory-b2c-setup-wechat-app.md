---
title: "Azure Active Directory B2C：WeChat 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers WeChat 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 WeChat 帳戶

> [!NOTE]
> 這項功能處於預覽狀態。
> 

## <a name="create-a-wechat-application"></a>建立 WeChat 應用程式

toouse WeChat B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate WeChat 應用程式和提供 hello 正確的參數。 您需要 WeChat 帳戶 toodo 此。 如果您沒有帳戶，您可以透過它們的其中一個行動裝置應用程式來註冊，或使用您的 QQ 號碼，藉以取得一個帳戶。 在這之後，取得您的帳戶向 hello WeChat 開發人員計劃。 您可以在 [這裡](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)找到詳細資訊。

### <a name="register-a-wechat-application"></a>註冊 WeChat 應用程式

1. 跳過[https://open.weixin.qq.com/](https://open.weixin.qq.com/)並登入。
2. 按一下 [管理中心]。
3. 請遵循 hello 必要步驟 tooregister 新的應用程式。
4. 針對 [授权回调域] \(回呼 URL)，輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。 例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。
5. 尋找並複製 hello**應用程式識別碼**和**應用程式金鑰**。 稍後您將需要這些資訊。

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>在租用戶中將 WeChat 設為識別提供者
1. 請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
2. 在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。
3. 按一下**+ 加**在 hello hello 刀鋒視窗最上方。
4. 提供方便**名稱**hello 身分識別提供者組態。 例如，輸入 "WeChat"。
5. 按一下 [識別提供者類型]、選取 [WeChat]，然後按一下 [確定]。
6. 按一下 [設定此識別提供者]。
7. 輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。
8. 輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。
9. 按一下**確定**，然後按一下**建立**toosave WeChat 組態。

