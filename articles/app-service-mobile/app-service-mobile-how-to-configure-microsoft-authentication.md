---
title: "aaaHow tooconfigure Microsoft 帳戶驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Microsoft 帳戶驗證您的應用程式服務應用程式。"
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>如何 tooconfigure 您 App Service 應用程式 toouse 的 Microsoft 帳戶登入
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

本主題說明如何 tooconfigure Azure App Service toouse 作為驗證提供者的 Microsoft 帳戶。 

## <a name="register-microsoft-account"> </a>使用 Microsoft 帳戶註冊應用程式
1. 登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。 複製您**URL**，稍後您使用 tooconfigure 您的應用程式使用 Microsoft 帳戶。
2. 瀏覽 toohello[我的應用程式]hello Microsoft 帳戶開發人員中心，在頁面上，並視需要使用您的 Microsoft 帳戶登入。
3. 按一下 [新增應用程式]，然後輸入應用程式名稱，再按一下 [建立應用程式]。
4. 請記下 hello**應用程式識別碼**，因為您稍後需要它。 
5. 在 [平台] 下，按一下 [新增平台]  ，然後選取 [網站]。
6. 然後按一下 應用程式 」 重新導向 Uri"供應 hello 端點下,**儲存**。 
   
   > [!NOTE]
   > 您重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/microsoftaccount/callback*。 例如： `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`。   
   > 請確定您使用 hello HTTPS 配置。
   
7. 在 [應用程式密碼] 下，按一下 [產生新密碼] 。 記下顯示 hello 值。 一旦您離開 hello 頁面，它就不會顯示一次。

    > [!IMPORTANT]
    > hello 密碼是重要的安全性認證。 請勿與任何人共用 hello 密碼或分散在用戶端應用程式中。

## <a name="secrets"></a>新增 Microsoft 帳戶資訊 tooyour App Service 應用程式
1. 在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式，按一下 **設定** > **驗證 / 授權**。
2. 如果 hello 驗證 / 授權功能未啟用，請切換它**上**。
3. 按一下 [Microsoft 帳戶] 。 貼上您先前，取得 hello 應用程式識別碼和密碼值，並選擇性地啟用應用程式所需的任何範圍。 然後按一下 [確定] 。
   
    ![][1]
   
    根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
4. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者由 Microsoft 帳戶驗證設定**當要求未經驗證的動作 tootake**太**Microsoft 帳戶**。 這需要驗證的所有要求，且所有未經驗證的要求會被重新導向 tooMicrosoft 帳戶進行驗證。
5. 按一下 [儲存] 。

現在您已準備好 toouse Microsoft 帳戶進行驗證您的應用程式。

## <a name="related-content"> </a>相關內容
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[我的應用程式]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure 入口網站]: https://portal.azure.com/
