---
title: "aaaAdd 推播通知 tooyour Android 應用程式與行動應用程式 |Microsoft 文件"
description: "了解如何 toouse 行動應用程式 toosend 推播通知 tooyour Android 應用程式。"
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a>加入推播通知 tooyour Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將加入推播通知 toohello [Android 的快速入門]專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您需要 hello 推播通知擴充套件。 如需詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

## <a name="prerequisites"></a>必要條件
您需要下列 hello:

* 根據您的專案後端的 IDE：

  * 如果此應用程式有 Node.js 後端，則為 [Android Studio](https://developer.android.com/sdk/index.html)。
  * 如果此應用程式有 Microsoft .NET 後端，則為 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 或更新版本。
* Android 2.3 或更新版本、Google Repository 版本 27 或更新版本，以及 Firebase 雲端傳訊適用的 Google Play 服務 9.0.2 或更新版本。
* 完整的 hello [Android 的快速入門]。

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>建立支援 Firebase 雲端通訊的專案
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>設定 Azure toosend 推播通知
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>啟用 hello 伺服器專案的推播通知
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>新增推播通知 tooyour 應用程式
在本節中，您會更新用戶端的 Android 應用程式 toohandle 推播通知。

### <a name="verify-android-sdk-version"></a>驗證 Android SDK 版本
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

下一步是 tooinstall Google Play 服務 」。 Google Cloud Messaging 有最小 API 層級需求的開發和測試，哪些 hello **minSdkVersion** hello 資訊清單中的屬性必須符合。

如果您要測試的較舊的裝置，請參閱[設定總 Google 播放 Services SDK] toodetermine 如何低您可以設定此值，並適當地進行設定。

### <a name="add-google-play-services-toohello-project"></a>將 Google Play 服務 toohello 專案
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>新增程式碼
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>針對 hello 測試 hello 應用程式發行行動服務
藉由直接附加的 Android 手機，使用 USB 纜線，或使用虛擬裝置 hello 模擬器中，您可以測試 hello 應用程式。

## <a name="next-steps"></a>後續步驟
現在，您完成本教學課程，請考慮 tooone hello 遵循教學課程的上繼續進行：

* [新增驗證 tooyour Android 應用程式](app-service-mobile-android-get-started-users.md)。
  了解 tooadd 驗證 toohello todolist 快速入門使用支援的身分識別提供者在 Android 上的專案。
* [啟用 Android 應用程式的離線同步處理](app-service-mobile-android-get-started-offline-data.md)。
  了解如何離線 tooadd 支援 tooyour 應用程式使用的行動應用程式後端。 使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。

<!-- URLs -->
[Android 的快速入門]: app-service-mobile-android-get-started.md

[設定總 Google 播放 Services SDK]:https://developers.google.com/android/guides/setup
