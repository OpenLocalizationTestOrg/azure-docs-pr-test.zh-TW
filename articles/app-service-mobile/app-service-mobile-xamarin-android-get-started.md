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
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="ca2a6-103">建立 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca2a6-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ca2a6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ca2a6-104">Overview</span></span>
<span data-ttu-id="ca2a6-105">本教學課程會示範如何 tooadd 雲端架構後端服務 tooa Xamarin.Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="ca2a6-106">如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="ca2a6-107">從完成的 hello 應用程式螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="ca2a6-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="ca2a6-108">完成本教學課程是 Xamarin Android 應用程式所有其他行動應用程式教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca2a6-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ca2a6-109">Prerequisites</span></span>
<span data-ttu-id="ca2a6-110">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="ca2a6-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="ca2a6-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-111">An active Azure account.</span></span> <span data-ttu-id="ca2a6-112">如果您還沒有帳戶，註冊試用 Azure，並啟動 too10 可用行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="ca2a6-113">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ca2a6-114">Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="ca2a6-115">如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="ca2a6-116">建立 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="ca2a6-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="ca2a6-117">請遵循這些步驟 toocreate 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="ca2a6-118">您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="ca2a6-119">接下來，下載簡單 「 todo 清單 」 的伺服器專案後端，將其發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="ca2a6-120">設定 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="ca2a6-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="ca2a6-121">下載並執行 hello Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca2a6-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="ca2a6-122">在下**下載並執行您的 Xamarin.Android 專案**，按一下 hello**下載** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="ca2a6-123">儲存 hello 壓縮的專案檔案 tooyour 本機電腦，並記下您儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="ca2a6-124">按 hello **F5**鍵 toobuild hello 專案，然後啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="ca2a6-125">在 hello 應用程式中，輸入有意義的文字，例如*完成 hello 教學課程*然後按一下hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="ca2a6-126">Hello 要求的資料會插入至 hello TodoItem 資料表。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="ca2a6-127">Hello 資料表中儲存的項目所傳回 hello 行動裝置應用程式後端，而且資料會出現在 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ca2a6-128">您可以檢閱會存取您的行動裝置應用程式後端 tooquery hello 程式碼，並插入 hello ToDoActivity.cs C# 檔案中找到的資料。</span><span class="sxs-lookup"><span data-stu-id="ca2a6-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="ca2a6-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca2a6-129">Next steps</span></span>
* [<span data-ttu-id="ca2a6-130">新增離線同步 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca2a6-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="ca2a6-131">新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca2a6-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="ca2a6-132">新增推播通知 tooyour Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca2a6-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="ca2a6-133">Toouse hello 如何管理 Azure 行動應用程式的用戶端</span><span class="sxs-lookup"><span data-stu-id="ca2a6-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
