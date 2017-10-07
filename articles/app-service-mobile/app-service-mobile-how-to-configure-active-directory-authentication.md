---
title: "aaaHow tooconfigure Azure Active Directory 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Azure Active Directory 驗證您的應用程式服務應用程式。"
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

本主題說明如何 tooconfigure Azure 應用程式服務 toouse 作為驗證提供者的 Azure Active Directory。

## <a name="express"> </a>使用快速設定設定 Azure Active Directory
1. 在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。 依序按一下 [設定] 及 [驗證/授權]。
2. 如果 hello 驗證 / 授權功能未啟用，請開啟 hello 參數太**上**。
3. 按一下 Azure Active Directory，然後按一下管理模式 下方的 快速。
4. 按一下**確定**tooregister hello 應用程式在 Azure Active Directory 中的。 這樣會建立新的註冊。 如果要改為 toochoose 現有的註冊，請按一下**選取現有的應用程式**然後搜尋 hello 先前建立的登錄您的租用戶內的名稱。
   它並按一下 按一下 hello 註冊 tooselect**確定**。 然後按一下 [**確定**hello Azure Active Directory 設定] 刀鋒視窗上。
   
   ![][0]
   
   根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
5. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者驗證 Azure Active Directory 中，設定**當要求未經驗證的動作 tootake**太**登入 Azure Active Directory**。 這需要的所有要求經過都驗證，而且所有未經驗證的要求重新導向的 tooAzure Active Directory 進行驗證。
6. 按一下 [儲存] 。

現在您已準備好 toouse Azure Active Directory 進行驗證您的應用程式。

## <a name="advanced"> </a>(替代方法) 使用進階設定手動設定 Azure Active Directory
您也可以選擇 tooprovide 組態設定以手動方式。 如果您想 toouse hello AAD 租用戶不同於您登入 Azure 的 hello 租用戶，這是慣用的 hello 方案。 toocomplete hello 組態中，您必須先建立註冊 Azure Active Directory 中，您就必須提供一些 hello 註冊詳細資料 tooApp 服務。

### <a name="register"> </a>向 Azure Active Directory 註冊您的應用程式
1. 登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。 複製您的 **URL**。 您將使用此 tooconfigure Azure Active Directory 應用程式。
2. 登入 toohello [Azure 傳統入口網站]並瀏覽過**Active Directory**。
   
    ![][2]
3. 選取您的目錄，然後選取 hello**應用程式**hello 頂端的索引標籤。 按一下**新增**在 hello 底部 toocreate 新的應用程式註冊。
4. 按一下 [Add an application my organization is developing] 。
5. 在 hello 新增應用程式精靈中輸入**名稱**您的應用程式，按一下 hello **Web 應用程式和/或 Web API**型別。 然後按一下 toocontinue。
6. 在 hello**登入 URL**方塊中，貼上您之前複製的 hello 應用程式 URL。 輸入該相同的 URL hello**應用程式識別碼 URI**方塊。 然後按一下 toocontinue。
7. 一旦加入 hello 應用程式，按一下 hello**設定** 索引標籤。編輯 hello**回覆 URL**下**單一登入**toobe hello URL，加上 hello 路徑的應用程式的*/.auth/login/aad/callback*。 例如： `https://contoso.azurewebsites.net/.auth/login/aad/callback`。 請確定您使用 hello HTTPS 配置。
   
    ![][3]
8. 按一下 [儲存] 。 然後複本 hello**用戶端識別碼**hello 應用程式。 您將設定您的應用程式 toouse 稍後。
9. Hello 底部命令列中，按一下 **檢視端點**，然後複製 hello 和**同盟中繼資料文件**URL 和下載的文件或瀏覽 tooit 瀏覽器中的。
10. Hello 根目錄中**EntityDescriptor**項目，應該有**entityID** hello 表單的屬性`https://sts.windows.net/`後面接著 GUID 特定 tooyour 租用戶 （稱為 「 租用戶識別碼 」）。 複製這個值，此值將做為您的「簽發者 URL」 。 您將設定您的應用程式 toouse 稍後。

### <a name="secrets"></a>新增 Azure Active Directory 資訊 tooyour 應用程式
1. 在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。 依序按一下 [設定] 及 [驗證/授權]。
2. 如果未啟用 hello 驗證和授權功能，開啟 hello 參數太**上**。
3. 按一下 Azure Active Directory，然後按一下管理模式 下方的 進階。 貼上的用戶端識別碼 hello 和簽發者 URL 的哪些是您先前取得的值。 然後按一下 [確定] 。
   
   ![][1]
   
   根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。 您必須在應用程式程式碼中授權使用者。
4. （選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者驗證 Azure Active Directory 中，設定**當要求未經驗證的動作 tootake**太**登入 Azure Active Directory**。 這需要的所有要求經過都驗證，而且所有未經驗證的要求重新導向的 tooAzure Active Directory 進行驗證。
5. 按一下 [儲存] 。

現在您已準備好 toouse Azure Active Directory 進行驗證您的應用程式。

## <a name="optional-configure-a-native-client-application"></a>(選擇性步驟) 設定原生用戶端應用程式
Azure Active Directory 也可讓您 tooregister 原生用戶端，可提供更好的控制，透過對應的權限。 您會需要此如果您想使用的程式庫，例如 hello tooperform 登入**Active Directory Authentication Library**。

1. 瀏覽過**Active Directory**在 hello [Azure 傳統入口網站]。
2. 選取您的目錄，然後選取 hello**應用程式**hello 頂端的索引標籤。 按一下**新增**在 hello 底部 toocreate 新的應用程式註冊。
3. 按一下 [Add an application my organization is developing] 。
4. 在 hello 新增應用程式精靈中輸入**名稱**您的應用程式，按一下 hello**原生用戶端應用程式**型別。 然後按一下 toocontinue。
5. 在 hello**重新導向 URI**方塊中，輸入您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。 此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。 如果建立 Windows 應用程式，請改為使用 hello[封裝 SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid)為 hello URI。
6. 一旦加入 hello 原生應用程式，按一下 hello**設定** 索引標籤。尋找 hello**用戶端識別碼**並記下此值。
7. 捲軸 hello 下一頁 toohello**權限 tooother 應用程式**區段，然後按一下**新增應用程式**。
8. 搜尋您先前註冊的 hello web 應用程式，然後按一下 hello 加號圖示。 然後按一下 hello 核取 tooclose hello 對話方塊。 如果找到，瀏覽 tooits 註冊並加入新的回覆 URL （例如 hello HTTP 版本的目前 URL），不能是 hello web 應用程式，按一下 [儲存]，然後重複這些步驟-hello 應用程式應該會顯示在 hello 清單。
9. Hello 您剛才加入了新的項目，開啟 hello**委派的權限**下拉式清單中選取**存取 (appName)**。 然後按一下 [儲存] 。

您現在已設定了可以存取您 App Service 應用程式的原生用戶端應用程式。

## <a name="related-content"> </a>相關內容
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com/
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[alternative method]:#advanced
