---
title: "aaaAdd 推播通知 tooyour Xamarin.Android 應用程式 |Microsoft 文件"
description: "了解如何 toouse Azure App Service 與 Azure 通知中樞 toosend 推播通知 tooyour Xamarin.Android 應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>新增推播通知 tooyour Xamarin.Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將加入推播通知 toohello [Xamarin.Android 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。 請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* 有效的 Google 帳戶。 您可以在 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)註冊 Google 帳戶。
* [Google Cloud Messaging 用戶端元件](http://components.xamarin.com/view/GCMClient/)。

## <a name="configure-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>啟用 Firebase 雲端傳訊
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>設定 Azure toosend 推播要求
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>更新 hello 伺服器專案 toosend 推播通知
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>設定推播通知的 hello 用戶端專案
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>新增推播通知的程式碼 tooyour 應用程式
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>在應用程式中測試推播通知
您可以使用虛擬裝置 hello 模擬器中測試 hello 應用程式。 在模擬器上執行時，您需要採取其他設定步驟。

1. 請確定您要部署 tooor 偵錯包含 Google Api 將設為 hello 目標，如下所示 hello Android Virtual Device (AVD) manager 中的虛擬裝置上。
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. 按一下 新增 Google 帳戶 toohello Android 裝置**應用程式** > **設定** > **將帳戶加入**，然後依照 hello 提示。
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. 執行 hello todolist 應用程式做之前，插入新的 todo 項目。 此時，通知圖示會顯示 hello 通知區域中。 您可以開啟 hello 通知抽屜 tooview hello 全文檢索的 hello 通知。
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
