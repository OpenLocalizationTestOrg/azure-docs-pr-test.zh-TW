---
title: "開始使用行動應用程式，使用 Xamarin.Forms aaaGet"
description: "請遵循此教學課程 toostart 使用 Xamarin.Forms 開發的行動應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>建立 Xamarin.Forms 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端後端服務 tooa Xamarin.Forms 行動應用程式使用 hello 做為 hello 後端的 Azure App Service 行動應用程式功能。 您會同時建立新的 Mobile Apps 後端，以及可在 Azure 中儲存應用程式資料的簡易待辦事項清單 Xamarin.Forms 應用程式。

完成本教學課程是所有其他 Xamarin.Forms 應用程式的行動應用程式教學課程的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 Azure 的試用版，並取得向上 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* Visual Studio 和 Xamarin。 如需資訊，請參閱 hello[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)頁面。

* 已安裝 Xcode v7.0 或更新版本以及 Xamarin Studio Community 的 Mac。 如需相關資訊，請參閱[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 及[針對 Mac 使用者設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN)。

## <a name="create-a-new-mobile-apps-back-end"></a>建立新的 Mobile Apps 後端

toocreate 新行動裝置應用程式備份結束時，請不要 hello 遵循：

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

您現在已設定您的行動用戶端應用程式可以使用的 Mobile Apps 後端。 接下來，您下載的簡單的待辦事項清單後端伺服器專案，然後將它發行 tooAzure。

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案

tooconfigure hello 伺服器專案 toouse hello Node.js 或.NET 後端，執行下列 hello:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>下載並執行 hello Xamarin.Forms 方案

您可以下載 hello 方案中任一種方式。 下載 tooa Mac Xamarin Studio 中開啟或下載它 tooa Windows 電腦和 Visual Studio 中開啟建置 hello iOS 應用程式使用網路的 Mac。 如需詳細資訊，請參閱[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。

Mac 或 Windows 的電腦上，hello 遵循：

1. 移 toohello [Azure 入口網站]。

2. 在 hello**設定**刀鋒視窗中的行動應用程式下**行動**，選取**開始** > **Xamarin.Forms**。 在**步驟 3** 之下，選取 [建立新的應用程式]，然後選取 [下載]。

   這個動作會下載包含連線的 tooyour 行動裝置應用程式的用戶端應用程式的專案。 儲存 hello 壓縮的專案檔案 tooyour 本機電腦，並記下您儲存的位置。

3. 解壓縮您下載的 hello 專案，然後再將它開啟在 Xamarin Studio (Mac) 或 Visual Studio (Windows) 中。

   ![在 Xamarin Studio 中解壓縮的專案][9]

   ![在 Visual Studio 中解壓縮的專案][8]

## <a name="optional-run-hello-ios-project"></a>（選擇性）執行 hello iOS 專案
在本節中，您可以執行 hello Xamarin iOS 專案，適用於 iOS 裝置。 如果未使用 iOS 裝置，可以略過這一節。

#### <a name="in-xamarin-studio"></a>在 Xamarin Studio 中
1. Hello iOS 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。

2. 在 hello**執行**功能表上，選取**開始偵錯**toobuild hello 專案和 hello iPhone 模擬器中啟動 hello 應用程式。

#### <a name="in-visual-studio"></a>在 Visual Studio 中
1. Hello iOS 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。

2. 在 hello**建置**功能表上，選取**Configuration Manager**。

3. 在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**下一步 toohello iOS 專案的核取方塊。

4. toobuild hello 專案和 hello 應用程式開始在 hello iPhone 模擬器中，選取 hello **F5**索引鍵。

   > [!NOTE]
   > 如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。 快速入門專案可能會變慢 tooupdate toohello 最新版本。    
   >
   >

5. 在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。

    ![][10]

    這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。 Hello 要求的資料會插入至 hello TodoItem 資料表。 Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。

    > [!NOTE]
    > 您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。
    >
    >

## <a name="optional-run-hello-android-project"></a>（選擇性）執行 hello Android 專案
在本節中，您可以執行 hello Xamarin droid 專案 for Android。 如果未使用 Android 裝置，可以略過這一節。

#### <a name="in-xamarin-studio"></a>在 Xamarin Studio 中

1. Hello Android 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。

2. toobuild hello 專案並開始 hello 應用程式在 Android 模擬器中，在 hello**執行**功能表上，選取**開始偵錯**。

#### <a name="in-visual-studio"></a>在 Visual Studio 中

1. Hello Android (Droid) 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。

2. 在 hello**建置**功能表上，選取**Configuration Manager**。

3. 在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**核取方塊下一步 toohello Android 專案。

4. toobuild hello 專案並開始 hello 應用程式在 Android 模擬器中，選取 hello **F5**索引鍵。

   > [!NOTE]
   > 如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。 快速入門專案可能會變慢 tooupdate toohello 最新版本。    
   >
   >

5. 在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。

    ![][11]
    
    這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。 Hello 要求的資料會插入至 hello TodoItem 資料表。 Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。
    
    > [!NOTE]
    > 您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。
    >
    >

## <a name="optional-run-hello-windows-project"></a>（選擇性）執行 Windows hello 的專案

在本節中，您可以執行 hello Xamarin WinApp 專案，適用於 Windows 裝置。 如果未使用 Windows 裝置，可以略過這一節。

#### <a name="in-visual-studio"></a>在 Visual Studio 中

1. 任何 hello Windows 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。

2. 在 hello**建置**功能表上，選取**Configuration Manager**。

3. 在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**您選擇的核取方塊下一步 toohello Windows 專案。

4. toobuild hello 專案並開始 hello 應用程式在 Windows 模擬器中，選取 hello **F5**索引鍵。

   > [!NOTE]
   > 如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。 快速入門專案可能會變慢 tooupdate toohello 最新版本。    
   >
   >

5. 在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。

    這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。 Hello 要求的資料會插入至 hello TodoItem 資料表。 Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。
    
    ![][12]
    
    > [!NOTE]
    > 您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。
    >
    >

## <a name="next-steps"></a>後續步驟

* [新增驗證 tooyour 應用程式](app-service-mobile-xamarin-forms-get-started-users.md)  
  深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。

* [新增推播通知 tooyour 應用程式](app-service-mobile-xamarin-forms-get-started-push.md)  
  了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動應用程式後端 toouse Azure 通知中樞 toosend hello 推播通知。

* [啟用應用程式的離線同步處理](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  深入了解如何使用行動應用程式的應用程式的 tooadd 離線支援後端。 使用離線同步，即便在沒有網路連線的情況下，您也能檢視、新增或修改行動裝置應用程式的資料。

* [針對行動裝置應用程式使用 hello 受管理的用戶端](app-service-mobile-dotnet-how-to-use-client-library.md)  
  了解如何以 hello toowork 管理您的 Xamarin 應用程式中的用戶端 SDK。

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure 入口網站]: https://portal.azure.com/
