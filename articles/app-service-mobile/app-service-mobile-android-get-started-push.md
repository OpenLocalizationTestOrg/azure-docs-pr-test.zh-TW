---
title: "使用 Mobile Apps 將推播通知新增至 Android 應用程式 | Microsoft Docs"
description: "了解如何使用 Mobile Apps 將推播通知傳送至 Android 應用程式。"
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="6e4ce-103">將推播通知新增至 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="6e4ce-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="6e4ce-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6e4ce-104">Overview</span></span>
<span data-ttu-id="6e4ce-105">在本教學課程中，您會將推播通知新增至 [Android 快速入門]專案，以便在每次插入一筆記錄時傳送推播通知至裝置。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="6e4ce-106">如果您不要使用下載的快速入門伺服器專案，則需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="6e4ce-107">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e4ce-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6e4ce-108">Prerequisites</span></span>
<span data-ttu-id="6e4ce-109">您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6e4ce-109">You need the following:</span></span>

* <span data-ttu-id="6e4ce-110">根據您的專案後端的 IDE：</span><span class="sxs-lookup"><span data-stu-id="6e4ce-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="6e4ce-111">如果此應用程式有 Node.js 後端，則為 [Android Studio](https://developer.android.com/sdk/index.html)。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="6e4ce-112">如果此應用程式有 Microsoft .NET 後端，則為 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="6e4ce-113">Android 2.3 或更新版本、Google Repository 版本 27 或更新版本，以及 Firebase 雲端傳訊適用的 Google Play 服務 9.0.2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="6e4ce-114">完成 [Android 快速入門]。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="6e4ce-115">建立支援 Firebase 雲端通訊的專案</span><span class="sxs-lookup"><span data-stu-id="6e4ce-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="6e4ce-116">設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="6e4ce-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="6e4ce-117">設定 Azure 來傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="6e4ce-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="6e4ce-118">啟用伺服器專案的推播通知</span><span class="sxs-lookup"><span data-stu-id="6e4ce-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="6e4ce-119">將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="6e4ce-119">Add push notifications to your app</span></span>
<span data-ttu-id="6e4ce-120">本節中，您必須更新用戶端 Android 應用程式，以處理推播通知。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="6e4ce-121">驗證 Android SDK 版本</span><span class="sxs-lookup"><span data-stu-id="6e4ce-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="6e4ce-122">下一個步驟是安裝 Google Play 服務。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="6e4ce-123">Google 雲端通訊在開發和測試方面有一些 API 層級的最低需求，這些是資訊清單中的 **minSdkVersion** 屬性所必須遵守。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="6e4ce-124">如果您要以較舊的裝置進行測試，請參考[設定 Google Play 服務 SDK]，以確認此值可以設得多低，並加以適當設定。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="6e4ce-125">新增 Google Play 服務至專案</span><span class="sxs-lookup"><span data-stu-id="6e4ce-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="6e4ce-126">新增程式碼</span><span class="sxs-lookup"><span data-stu-id="6e4ce-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="6e4ce-127">對已發佈的行動服務進行應用程式測試</span><span class="sxs-lookup"><span data-stu-id="6e4ce-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="6e4ce-128">您可以使用 USB 纜線直接連接 Android 手機，或使用模擬器中的虛擬裝置，對應用程式進行測試。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e4ce-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e4ce-129">Next steps</span></span>
<span data-ttu-id="6e4ce-130">現在您已經完成了這個教學課程，可以考慮繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="6e4ce-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="6e4ce-131">[在 Android 應用程式中新增驗證](app-service-mobile-android-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="6e4ce-132">了解如何使用支援的識別提供者，在 Android 上的 TodoList 快速入門專案中新增驗證。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="6e4ce-133">[啟用 Android 應用程式的離線同步處理](app-service-mobile-android-get-started-offline-data.md)。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="6e4ce-134">了解如何使用 Mobile Apps 後端，將離線支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="6e4ce-135">使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="6e4ce-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="6e4ce-136">[Android 快速入門]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="6e4ce-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="6e4ce-137">[設定 Google Play 服務 SDK]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="6e4ce-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
