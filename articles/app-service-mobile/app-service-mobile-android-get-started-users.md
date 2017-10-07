---
title: "Android 的行動應用程式上的 aaaAdd 驗證 |Microsoft 文件"
description: "了解如何 toouse hello 的 Android 應用程式透過不同的身分識別提供者，包括 Google、 Facebook、 Twitter 和 Microsoft Azure App Service tooauthenticate 使用者的行動應用程式功能。"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>新增驗證 tooyour Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>摘要
在此教學課程中，您將驗證 toohello todolist 快速入門專案在 Android 上使用支援的身分識別提供者。 本教學課程根據 hello[開始使用行動應用程式]教學課程中，您必須先完成。

## <a name="register"></a>註冊應用程式進行驗證，並設定 Azure App Service
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。 Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。 在本教學課程中，我們使用 hello URL 配置_appname_整個。 不過，您可以使用任何您選擇的 URL 結構描述。 它應該是唯一的 tooyour 行動應用程式。 hello 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 在 hello**允許外部重新導向 Url**，輸入`appname://easyauth.callback`。  hello _appname_這個字串中為 行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

4. 按一下 [確定] 。

5. 按一下 [儲存] 。

## <a name="permissions"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* 在 Android Studio 中，開啟您已完成的 hello 專案 hello 教學課程[開始使用行動應用程式]。 從 hello**執行**功能表上，按一下 **執行應用程式**，並確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。

     這個例外狀況是因為 tooaccess 回 hello hello 應用程式嘗試結束身為未經驗證的使用者，但 hello *TodoItem*資料表現在需要驗證。

接下來，您可以更新 hello 應用程式 tooauthenticate 使用者要求資源從 hello 回行動應用程式結束之前。 

## <a name="add-authentication-toohello-app"></a>新增驗證 toohello 應用程式
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Hello 用戶端上快取驗證權杖
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>後續步驟
現在，您完成本教學課程中基本驗證，請考慮 tooone hello 遵循教學課程的上繼續進行：

* [加入推播通知 tooyour Android 應用程式](app-service-mobile-android-get-started-push.md)。
  了解如何 tooconfigure 回您的行動應用程式結束 toouse Azure 通知中樞 toosend 推播通知。
* [啟用 Android 應用程式的離線同步處理](app-service-mobile-android-get-started-offline-data.md)。
  了解如何離線 tooadd 支援 tooyour 應用程式使用的行動應用程式後端。 使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[開始使用行動應用程式]: app-service-mobile-android-get-started.md
