---
title: "aaaGet Xamarin.iOS 應用程式入門 Azure App Service 行動應用程式 |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用 Xamarin.iOS 開發行動應用程式。"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>建立 Xamarin.iOS 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端架構後端服務使用 Azure 行動應用程式後端的 tooa Xamarin.iOS 行動裝置應用程式。  您會建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Xaamrin.iOS 應用程式。

完成本教學課程是有關使用 Azure App Service 中的 hello 行動應用程式功能所有其他 Xamarin.iOS 教學課程的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要下列必要條件 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，註冊 Azure 的試用版，並啟動 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* Visual Studio 和 Xamarin。 如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。
* 已安裝 Xcode v7.0 或更新版本以及 Xamarin Studio Community 的 Mac。 請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)及[針對 Mac 使用者的設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN)。

## <a name="create-an-azure-mobile-app-backend"></a>建立 Azure 行動應用程式後端
請遵循這些步驟 toocreate 行動裝置應用程式後端。

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案
您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。 接下來，下載簡單 「 todo 清單 」 的伺服器專案後端，將其發行 tooAzure。

請遵循下列步驟 tooconfigure hello 伺服器專案 toouse hello 任一 hello Node.js 或.NET 後端。

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>下載並執行 hello Xamarin.iOS 應用程式
1. 開啟 hello [Azure 入口網站]瀏覽器視窗中。
2. 在您的行動裝置應用程式的 hello 設定刀鋒視窗，按一下 **開始** > **Xamarin.iOS**。 在步驟 3 中，按一下 [建立新的應用程式]  \(如果尚未選取的話)。  接下來按一下 [hello**下載**] 按鈕。

      連接 tooyour 行動後端的用戶端應用程式會下載。 Hello 壓縮的專案檔儲存到本機電腦，並記下您儲存的位置。
3. 解壓縮您下載的 hello 專案，然後再將它開啟 Xamarin Studio （或 Visual Studio） 中。

    ![][9]

    ![][8]
4. Hello F5 鍵 toobuild hello 專案，請按住 hello iPhone 模擬器中啟動 hello 應用程式。
5. 在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，然後按一下hello  **+**   按鈕。

    ![][10]

    Hello 要求的資料會插入至 hello TodoItem 資料表。 Hello 行動裝置應用程式後端，所傳回項目儲存在 hello 資料表和資料會顯示 hello 清單中。

> [!NOTE]
> 您可以檢閱會存取您的行動裝置應用程式後端 tooquery hello 程式碼，並且在 hello QSTodoService.cs C# 檔案中插入資料。
>
>

## <a name="next-steps"></a>後續步驟
* [新增離線同步 tooyour 應用程式](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [新增驗證 tooyour 應用程式](app-service-mobile-xamarin-ios-get-started-users.md)
* [新增推播通知 tooyour Xamarin.Android 應用程式](app-service-mobile-xamarin-ios-get-started-push.md)
* [Toouse hello 如何管理 Azure 行動應用程式的用戶端](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure 入口網站]: https://portal.azure.com/
