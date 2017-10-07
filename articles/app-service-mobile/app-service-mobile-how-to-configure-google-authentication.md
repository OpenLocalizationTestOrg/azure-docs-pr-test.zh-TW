---
title: "aaaHow tooconfigure Google 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Google 驗證您的應用程式服務應用程式。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>如何 tooconfigure 您 App Service 應用程式 toouse Google 登入
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

本主題說明如何 tooconfigure Azure App Service toouse Google 作為驗證提供者。

toocomplete hello 程序，本主題中的，您必須具有 已驗證的電子郵件地址的 Google 帳戶。 toocreate 新 Google 帳戶，跳過[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)。

## <a name="register"> </a>向 Google 註冊您的應用程式
1. 登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。 複製您**URL**，而您使用稍後 tooconfigure Google 應用程式。
2. 瀏覽 toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303)網站，使用您的 Google 帳戶認證登入。 按一下**建立專案**，提供**專案名稱**，然後按一下  **建立**。
3. 在 [社交平台類 API] 下，按一下 [Google + API]，然後按一下 [啟用]。
4. 在左瀏覽，hello**認證** > **OAuth 同意畫面**，然後選取您**電子郵件地址**，輸入**產品名稱**，然後按一下**儲存**。
5. 在 hello**認證**索引標籤上，按一下 **建立認證** > **OAuth 用戶端識別碼**，然後選取**Web 應用程式**。
6. 貼上 hello App Service **URL**您先前複製到**授權 JavaScript Origins**，然後貼上您重新導向 URI 切割**授權重新導向 URI**。 hello 重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/google/callback*。 例如： `https://contoso.azurewebsites.net/.auth/login/google/callback`。 請確定您使用 hello HTTPS 配置。 然後按一下 [ **建立**]。
7. Hello 下一個畫面中，記下的 hello 值 hello 用戶端識別碼和用戶端密碼。

    > [!IMPORTANT]
    > hello 用戶端機密是重要的安全性認證。 請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。


## <a name="secrets"></a>新增 Google 資訊 tooyour 應用程式
1. 在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。 依序按一下 [設定] 及 [驗證/授權]。
2. 如果 hello 驗證 / 授權功能未啟用，請開啟 hello 參數太**上**。
3. 按一下 [Google] 。 貼上您先前，取得 hello 應用程式識別碼和應用程式密碼值，並選擇性地啟用應用程式所需的任何範圍。 然後按一下 [確定] 。
   
   ![][1]
   
   根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
4. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者經過 Google、 設定**當要求未經驗證的動作 tootake**太**Google**。 這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooGoogle 進行驗證。
5. 按一下 [儲存] 。

現在您已準備好 toouse Google 驗證您的應用程式。

## <a name="related-content"> </a>相關內容
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 入口網站]: https://portal.azure.com/

