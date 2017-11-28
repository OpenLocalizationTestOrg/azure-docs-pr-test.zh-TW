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
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="4ed13-103">建立 Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ed13-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4ed13-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4ed13-104">Overview</span></span>
<span data-ttu-id="4ed13-105">本教學課程會示範如何 tooadd 雲端架構後端服務使用 Azure 行動應用程式後端的 tooa Xamarin.iOS 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ed13-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="4ed13-106">您會建立新的行動應用程式後端，以及可在 Azure 中儲存應用程式資料的簡易「待辦事項清單」 Xaamrin.iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ed13-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="4ed13-107">完成本教學課程是有關使用 Azure App Service 中的 hello 行動應用程式功能所有其他 Xamarin.iOS 教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="4ed13-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ed13-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="4ed13-108">Prerequisites</span></span>
<span data-ttu-id="4ed13-109">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="4ed13-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="4ed13-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ed13-110">An active Azure account.</span></span> <span data-ttu-id="4ed13-111">如果您沒有帳戶，註冊 Azure 的試用版，並啟動 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="4ed13-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="4ed13-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4ed13-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4ed13-113">Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="4ed13-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="4ed13-114">如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4ed13-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="4ed13-115">已安裝 Xcode v7.0 或更新版本以及 Xamarin Studio Community 的 Mac。</span><span class="sxs-lookup"><span data-stu-id="4ed13-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="4ed13-116">請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)及[針對 Mac 使用者的設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN)。</span><span class="sxs-lookup"><span data-stu-id="4ed13-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="4ed13-117">建立 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="4ed13-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="4ed13-118">請遵循這些步驟 toocreate 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="4ed13-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="4ed13-119">設定 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="4ed13-119">Configure hello server project</span></span>
<span data-ttu-id="4ed13-120">您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="4ed13-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="4ed13-121">接下來，下載簡單 「 todo 清單 」 的伺服器專案後端，將其發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4ed13-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="4ed13-122">請遵循下列步驟 tooconfigure hello 伺服器專案 toouse hello 任一 hello Node.js 或.NET 後端。</span><span class="sxs-lookup"><span data-stu-id="4ed13-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="4ed13-123">下載並執行 hello Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ed13-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="4ed13-124">開啟 hello [Azure 入口網站]瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="4ed13-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="4ed13-125">在您的行動裝置應用程式的 hello 設定刀鋒視窗，按一下 **開始** > **Xamarin.iOS**。</span><span class="sxs-lookup"><span data-stu-id="4ed13-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="4ed13-126">在步驟 3 中，按一下 [建立新的應用程式]  \(如果尚未選取的話)。</span><span class="sxs-lookup"><span data-stu-id="4ed13-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="4ed13-127">接下來按一下 [hello**下載**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4ed13-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="4ed13-128">連接 tooyour 行動後端的用戶端應用程式會下載。</span><span class="sxs-lookup"><span data-stu-id="4ed13-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="4ed13-129">Hello 壓縮的專案檔儲存到本機電腦，並記下您儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="4ed13-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="4ed13-130">解壓縮您下載的 hello 專案，然後再將它開啟 Xamarin Studio （或 Visual Studio） 中。</span><span class="sxs-lookup"><span data-stu-id="4ed13-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="4ed13-131">Hello F5 鍵 toobuild hello 專案，請按住 hello iPhone 模擬器中啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ed13-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="4ed13-132">在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，然後按一下hello  **+**   按鈕。</span><span class="sxs-lookup"><span data-stu-id="4ed13-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="4ed13-133">Hello 要求的資料會插入至 hello TodoItem 資料表。</span><span class="sxs-lookup"><span data-stu-id="4ed13-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="4ed13-134">Hello 行動裝置應用程式後端，所傳回項目儲存在 hello 資料表和資料會顯示 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="4ed13-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="4ed13-135">您可以檢閱會存取您的行動裝置應用程式後端 tooquery hello 程式碼，並且在 hello QSTodoService.cs C# 檔案中插入資料。</span><span class="sxs-lookup"><span data-stu-id="4ed13-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4ed13-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ed13-136">Next steps</span></span>
* [<span data-ttu-id="4ed13-137">新增離線同步 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ed13-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="4ed13-138">新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ed13-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="4ed13-139">新增推播通知 tooyour Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ed13-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="4ed13-140">Toouse hello 如何管理 Azure 行動應用程式的用戶端</span><span class="sxs-lookup"><span data-stu-id="4ed13-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
