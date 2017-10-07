---
title: "aaaHow tooconfigure Twitter 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Twitter 驗證您的應用程式服務應用程式。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>如何 tooconfigure 您 App Service 應用程式 toouse Twitter 登入
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

本主題說明如何 tooconfigure Azure App Service toouse Twitter 做為驗證提供者。

toocomplete hello 程序，本主題中的，您必須具有 [已驗證的電子郵件地址和電話號碼的 Twitter 帳戶。 toocreate 新的 Twitter 帳戶，跳過<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>。

## <a name="register"> </a>向 Twitter 註冊您的應用程式
1. 登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。 複製您的 **URL**。 您將使用此 tooconfigure Twitter 應用程式。
2. 瀏覽 toohello [Twitter 開發人員]網站，使用您的 Twitter 帳戶認證登入，然後按一下 [**建立新的應用程式**。
3. 型別在 hello**名稱**和**描述**新應用程式。 貼上您的應用程式的**URL** hello**網站**值。 然後，針對 hello**回呼 URL**，貼上 hello**回呼 URL**您之前複製。 這是您的行動裝置應用程式閘道加上 hello 路徑*/.auth/login/twitter/callback*。 例如： `https://contoso.azurewebsites.net/.auth/login/twitter/callback`。 請確定您使用 hello HTTPS 配置。
4. 在 hello 底部 hello] 頁面上，閱讀並接受 hello 條款。 然後按一下 [ **建立 Twitter 應用程式**]。 此暫存器 hello 應用程式會顯示 hello 應用程式詳細資料。
5. 按一下 hello**設定**索引標籤上，核取**允許 Twitter 入此應用程式使用 toobe toosign**，然後按一下 [**更新設定**。
6. 選取 hello**機碼和存取權杖**] 索引標籤。請記下的 hello 值**取用者金鑰 （應用程式開發介面）**和**取用者密碼 （應用程式開發介面機密）**。
   
   > [!NOTE]
   > hello 取用者密碼是重要的安全性認證。 請勿將此密碼告訴任何人或隨應用程式一起散發。
   > 
   > 

## <a name="secrets"></a>新增 Twitter 資訊 tooyour 應用程式
1. 在 [hello [Azure 入口網站]，瀏覽 tooyour 應用程式。 依序按一下 [設定] 及 [驗證/授權]。
2. 如果 hello 驗證 / 授權功能未啟用，請開啟 hello 參數太**上**。
3. 按一下 [Twitter] 。 您先前取得的值貼上在應用程式識別碼 hello 與應用程式密碼。 然後按一下 [確定] 。
   
   ![][1]
   
   根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
4. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者由 Twitter 驗證設定**當要求未經驗證的動作 tootake**太**Twitter**。 這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooTwitter 進行驗證。
5. 按一下 [儲存] 。

現在您已準備好 toouse Twitter 驗證您的應用程式。

## <a name="related-content"> </a>相關內容
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure 入口網站]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
