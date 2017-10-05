---
title: "開始使用適用於 Xamarin.Android 應用程式的Azure 行動應用程式"
description: "遵循此教學課程，可開始使用 Azure Mobile Apps 進行 Xamarin Android 開發。"
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
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a>建立 Xamarin.Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程將示範如何將雲端後端服務加入至 Xamarin.Android 應用程式。 如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。

以下是完成之應用程式的螢幕擷取畫面：

![][0]

完成本教學課程是 Xamarin Android 應用程式所有其他行動應用程式教學課程的必要條件。

## <a name="prerequisites"></a>必要條件
若要完成本教學課程，您需要下列必要條件：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，請註冊 Azure 試用版並取得最多 10 個免費的 Mobile Apps。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* Visual Studio 和 Xamarin。 如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。

## <a name="create-an-azure-mobile-app-backend"></a>建立 Azure 行動應用程式後端
依照下列步驟建立行動應用程式後端。

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。 接下來，下載簡易「待辦事項清單」後端的伺服器專案，然後將專案發佈至 Azure。

## <a name="configure-the-server-project"></a>設定伺服器專案
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a>下載並執行 Xamarin.Android 應用程式
1. 在 [下載並執行 Xamarin.Android 專案] 底下，按 [下載] 按鈕。

      將此壓縮專案檔案儲存到您的本機電腦，並記錄儲存位置。
2. 按 **F5** 鍵，以重建專案並啟動應用程式。
3. 在應用程式中輸入有意義的文字 (例如 Complete the tutorial)，然後按一下 [新增] 按鈕。

    ![][10]

    要求中的資料會插入 TodoItem 資料表中。 行動應用程式後端會傳回資料表中儲存的項目，而該資料會顯示在清單中。

   > [!NOTE]
   > 您可以檢閱存取行動應用程式後端以查詢與插入資料的程式碼，您可在 ToDoActivity.cs C# 檔案中找到此程式碼。
   >
   >

## <a name="next-steps"></a>後續步驟
* [將離線同步處理新增至您的應用程式](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [在您的應用程式中新增驗證 ](app-service-mobile-xamarin-android-get-started-users.md)
* [將推播通知新增至您的 Xamarin.Android 應用程式](app-service-mobile-xamarin-android-get-started-push.md)
* [如何針對 Azure Mobile Apps 使用受管理的用戶端](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
