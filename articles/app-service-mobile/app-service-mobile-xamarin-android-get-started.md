---
title: "aaaGet 開始使用 Azure 行動應用程式的 Xamarin.Android 應用程式"
description: "請遵循此教學課程 tooget 開始使用 Xamarin Android 開發的 Azure 行動應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>建立 Xamarin.Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端架構後端服務 tooa Xamarin.Android 應用程式。 如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。

從完成的 hello 應用程式螢幕擷取畫面如下：

![][0]

完成本教學課程是 Xamarin Android 應用程式所有其他行動應用程式教學課程的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要下列必要條件 hello:

* 使用中的 Azure 帳戶。 如果您還沒有帳戶，註冊試用 Azure，並啟動 too10 可用行動應用程式。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* Visual Studio 和 Xamarin。 如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。

## <a name="create-an-azure-mobile-app-backend"></a>建立 Azure 行動應用程式後端
請遵循這些步驟 toocreate 行動裝置應用程式後端。

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。 接下來，下載簡單 「 todo 清單 」 的伺服器專案後端，將其發行 tooAzure。

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>下載並執行 hello Xamarin.Android 應用程式
1. 在下**下載並執行您的 Xamarin.Android 專案**，按一下 hello**下載** 按鈕。

      儲存 hello 壓縮的專案檔案 tooyour 本機電腦，並記下您儲存的位置。
2. 按 hello **F5**鍵 toobuild hello 專案，然後啟動 hello 應用程式。
3. 在 hello 應用程式中，輸入有意義的文字，例如*完成 hello 教學課程*然後按一下hello**新增** 按鈕。

    ![][10]

    Hello 要求的資料會插入至 hello TodoItem 資料表。 Hello 資料表中儲存的項目所傳回 hello 行動裝置應用程式後端，而且資料會出現在 hello 清單。

   > [!NOTE]
   > 您可以檢閱會存取您的行動裝置應用程式後端 tooquery hello 程式碼，並插入 hello ToDoActivity.cs C# 檔案中找到的資料。
   >
   >

## <a name="next-steps"></a>後續步驟
* [新增離線同步 tooyour 應用程式](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [新增驗證 tooyour 應用程式](app-service-mobile-xamarin-android-get-started-users.md)
* [新增推播通知 tooyour Xamarin.Android 應用程式](app-service-mobile-xamarin-android-get-started-push.md)
* [Toouse hello 如何管理 Azure 行動應用程式的用戶端](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
