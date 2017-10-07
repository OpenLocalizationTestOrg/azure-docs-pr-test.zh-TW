---
title: "aaaHow tooconfigure Facebook 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Facebook 驗證您的應用程式服務應用程式。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>如何 tooconfigure 您 App Service 應用程式 toouse Facebook 登入
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

本主題說明如何 tooconfigure Azure App Service toouse Facebook 做為驗證提供者。

toocomplete hello 程序，本主題中的，您必須擁有已驗證的電子郵件地址和行動電話號碼的 Facebook 帳戶。 新的 Facebook 帳戶，toocreate 太移[facebook.com]。

## <a name="register"> </a>向 Facebook 註冊您的應用程式
1. 登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。 複製您的 **URL**。 您將使用此 tooconfigure Facebook 應用程式。
2. 在另一個瀏覽器視窗中，瀏覽 toohello [Facebook 開發人員]網站，並使用您的 Facebook 登入帳戶的認證。
3. （選擇性）如果您具有尚未註冊，請按一下**應用程式** > **身為開發人員註冊**，然後接受 hello 原則，並遵循 hello 註冊步驟。
4. 按一下 [我的應用程式] > [新增應用程式] > [網站] > [略過並建立應用程式識別碼]。 
5. 在**顯示名稱**，輸入您的應用程式類型的唯一名稱您**Contact Email**，選擇**類別**應用程式，然後按一下**建立應用程式識別碼**並完成 hello 安全性檢查。 這會帶您 toohello 新的 Facebook 應用程式的開發人員儀表板。
6. 在 [Facebook 登入] 下，按一下 [開始使用]。 新增您的應用程式**重新導向 URI**太**有效的 OAuth 重新導向 Uri**，然後按一下 **儲存變更**。 
   
   > [!NOTE]
   > 您重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/facebook/callback*。 例如： `https://contoso.azurewebsites.net/.auth/login/facebook/callback`。 請確定您使用 hello HTTPS 配置。
   > 
   > 
7. 在 hello 左側導覽中，按一下 **設定**。 在 hello**應用程式秘鑰**欄位中，按一下**顯示**，提供您的密碼，如果要求，然後記下的 hello 值**應用程式識別碼**和**應用程式秘鑰**. 您使用這些更新 tooconfigure 您的應用程式在 Azure 中。
   
   > [!IMPORTANT]
   > hello 應用程式密碼是重要的安全性認證。 請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。
   > 
   > 
8. hello 已使用的 tooregister hello 應用程式的 Facebook 帳戶是 hello 應用程式的系統管理員。 此時，只有系統管理員可以登入此應用程式。 tooauthenticate 其他 Facebook 帳戶，按一下**應用程式檢閱**並啟用**< 您的應用程式名稱 > 請公用**tooenable 使用 Facebook 驗證一般公用存取。

## <a name="secrets"></a>新增 Facebook 資訊 tooyour 應用程式
1. 在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。 按一下 [設定] > [驗證/授權]，並確定 [App Service 驗證] 為 [開啟]。
2. 按一下**Facebook**，貼上您先前取得 hello 應用程式識別碼和應用程式密碼值，選擇性地啟用應用程式所需的任何範圍然後按一下**確定**。
   
    ![][0]
   
    根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
3. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者驗證 Facebook、 設定**當要求未經驗證的動作 tootake**太**Facebook**。 這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooFacebook 進行驗證。
4. 設定驗證完成時，按一下 [儲存] 。

現在您已準備好 toouse Facebook 驗證您的應用程式。

## <a name="related-content"> </a>相關內容
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook 開發人員]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure 入口網站]: https://portal.azure.com/
