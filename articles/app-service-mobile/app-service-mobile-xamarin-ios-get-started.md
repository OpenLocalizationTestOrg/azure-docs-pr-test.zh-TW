---
title: "在 Xamarin.iOS 應用程式中開始使用 Azure App Service Mobile Apps | Microsoft Docs"
description: "遵循本教學課程，開始使用 Mobile Apps 進行 Xamarin.iOS 開發。"
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
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="957de-103">建立 Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="957de-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="957de-104">概觀</span><span class="sxs-lookup"><span data-stu-id="957de-104">Overview</span></span>
<span data-ttu-id="957de-105">本教學課程說明如何使用 Azure 行動 app 後端，將雲端型後端服務加入至 Xamarin.iOS 行動 app。</span><span class="sxs-lookup"><span data-stu-id="957de-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="957de-106">您會建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Xaamrin.iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="957de-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="957de-107">您必須先完成此教學課程，才能進行所有其他在 Azure App Service 中使用 Mobile Apps 的 Xamarin.iOS 相關教學課程。</span><span class="sxs-lookup"><span data-stu-id="957de-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="957de-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="957de-108">Prerequisites</span></span>
<span data-ttu-id="957de-109">若要完成本教學課程，您需要下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="957de-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="957de-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="957de-110">An active Azure account.</span></span> <span data-ttu-id="957de-111">如果您沒有帳戶，請註冊 Azure 試用版並取得最多 10 個免費的行動應用程式，即使在試用期結束之後仍可繼續使用這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="957de-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="957de-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="957de-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="957de-113">Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="957de-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="957de-114">如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="957de-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="957de-115">已安裝 Xcode v7.0 或更新版本以及 Xamarin Studio Community 的 Mac。</span><span class="sxs-lookup"><span data-stu-id="957de-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="957de-116">請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)及[針對 Mac 使用者的設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN)。</span><span class="sxs-lookup"><span data-stu-id="957de-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="957de-117">建立 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="957de-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="957de-118">依照下列步驟建立行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="957de-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="957de-119">設定伺服器專案</span><span class="sxs-lookup"><span data-stu-id="957de-119">Configure the server project</span></span>
<span data-ttu-id="957de-120">您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="957de-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="957de-121">接下來，下載簡易「待辦事項清單」後端的伺服器專案，然後將專案發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="957de-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="957de-122">請遵循下列步驟，將伺服器專案設定為使用 Node.js 或 .NET 後端。</span><span class="sxs-lookup"><span data-stu-id="957de-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="957de-123">下載並執行 Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="957de-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="957de-124">在瀏覽器視窗中開啟 [Azure 入口網站] 。</span><span class="sxs-lookup"><span data-stu-id="957de-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="957de-125">在行動應用程式的設定刀鋒視窗上，按一下 [開始使用]  >  [Xamarin.iOS]。</span><span class="sxs-lookup"><span data-stu-id="957de-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="957de-126">在步驟 3 中，按一下 [建立新的應用程式]  \(如果尚未選取的話)。</span><span class="sxs-lookup"><span data-stu-id="957de-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="957de-127">接著按一下 [下載]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="957de-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="957de-128">已下載連接到您的行動後端的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="957de-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="957de-129">將此壓縮專案檔案儲存到您的本機電腦，並記錄儲存位置。</span><span class="sxs-lookup"><span data-stu-id="957de-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="957de-130">將您下載的專案解壓縮，並在 Xamarin Studio (或 Visual Studio) 中開啟。</span><span class="sxs-lookup"><span data-stu-id="957de-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="957de-131">按 F5 鍵，以建置專案並在 iPhone 模擬器中啟動 app。</span><span class="sxs-lookup"><span data-stu-id="957de-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="957de-132">在應用程式中，輸入有意義的文字 (例如「了解 Xamarin」)，然後按一下 **+** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="957de-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="957de-133">要求中的資料會插入 TodoItem 資料表中。</span><span class="sxs-lookup"><span data-stu-id="957de-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="957de-134">行動應用程式後端會傳回資料表中儲存的項目，而該資料會顯示在清單中。</span><span class="sxs-lookup"><span data-stu-id="957de-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="957de-135">您可以在 QSTodoService.cs C# 檔案中檢閱用來存取行動應用程式後端以查詢和插入資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="957de-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="957de-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="957de-136">Next steps</span></span>
* [<span data-ttu-id="957de-137">將離線同步處理新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="957de-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="957de-138">在您的應用程式中新增驗證 </span><span class="sxs-lookup"><span data-stu-id="957de-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="957de-139">將推播通知新增至您的 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="957de-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="957de-140">如何針對 Azure Mobile Apps 使用受管理的用戶端</span><span class="sxs-lookup"><span data-stu-id="957de-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
<span data-ttu-id="957de-141">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="957de-141">[Azure portal]: https://portal.azure.com/</span></span>
