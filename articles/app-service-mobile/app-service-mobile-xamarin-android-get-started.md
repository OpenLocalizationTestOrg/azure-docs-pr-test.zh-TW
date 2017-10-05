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
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="a890a-103">建立 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="a890a-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a890a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a890a-104">Overview</span></span>
<span data-ttu-id="a890a-105">本教學課程將示範如何將雲端後端服務加入至 Xamarin.Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a890a-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="a890a-106">如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。</span><span class="sxs-lookup"><span data-stu-id="a890a-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="a890a-107">以下是完成之應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="a890a-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="a890a-108">完成本教學課程是 Xamarin Android 應用程式所有其他行動應用程式教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="a890a-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a890a-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="a890a-109">Prerequisites</span></span>
<span data-ttu-id="a890a-110">若要完成本教學課程，您需要下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="a890a-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="a890a-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a890a-111">An active Azure account.</span></span> <span data-ttu-id="a890a-112">如果您沒有帳戶，請註冊 Azure 試用版並取得最多 10 個免費的 Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="a890a-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="a890a-113">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a890a-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a890a-114">Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="a890a-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="a890a-115">如需相關指示，請參閱 [設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="a890a-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="a890a-116">建立 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="a890a-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="a890a-117">依照下列步驟建立行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="a890a-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="a890a-118">您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="a890a-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="a890a-119">接下來，下載簡易「待辦事項清單」後端的伺服器專案，然後將專案發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="a890a-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="a890a-120">設定伺服器專案</span><span class="sxs-lookup"><span data-stu-id="a890a-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="a890a-121">下載並執行 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="a890a-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="a890a-122">在 [下載並執行 Xamarin.Android 專案] 底下，按 [下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a890a-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="a890a-123">將此壓縮專案檔案儲存到您的本機電腦，並記錄儲存位置。</span><span class="sxs-lookup"><span data-stu-id="a890a-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="a890a-124">按 **F5** 鍵，以重建專案並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="a890a-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="a890a-125">在應用程式中輸入有意義的文字 (例如 Complete the tutorial)，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a890a-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="a890a-126">要求中的資料會插入 TodoItem 資料表中。</span><span class="sxs-lookup"><span data-stu-id="a890a-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="a890a-127">行動應用程式後端會傳回資料表中儲存的項目，而該資料會顯示在清單中。</span><span class="sxs-lookup"><span data-stu-id="a890a-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a890a-128">您可以檢閱存取行動應用程式後端以查詢與插入資料的程式碼，您可在 ToDoActivity.cs C# 檔案中找到此程式碼。</span><span class="sxs-lookup"><span data-stu-id="a890a-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="a890a-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a890a-129">Next steps</span></span>
* [<span data-ttu-id="a890a-130">將離線同步處理新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a890a-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="a890a-131">在您的應用程式中新增驗證 </span><span class="sxs-lookup"><span data-stu-id="a890a-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="a890a-132">將推播通知新增至您的 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="a890a-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="a890a-133">如何針對 Azure Mobile Apps 使用受管理的用戶端</span><span class="sxs-lookup"><span data-stu-id="a890a-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
