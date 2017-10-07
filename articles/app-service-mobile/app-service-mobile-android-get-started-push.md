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
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="c26a1-103">加入推播通知 tooyour Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="c26a1-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="c26a1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c26a1-104">Overview</span></span>
<span data-ttu-id="c26a1-105">在本教學課程中，您將加入推播通知 toohello [Android 的快速入門]專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="c26a1-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="c26a1-106">如果您不要使用 hello 下載快速入門的伺服器專案，您需要 hello 推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="c26a1-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="c26a1-107">如需詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="c26a1-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c26a1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c26a1-108">Prerequisites</span></span>
<span data-ttu-id="c26a1-109">您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c26a1-109">You need hello following:</span></span>

* <span data-ttu-id="c26a1-110">根據您的專案後端的 IDE：</span><span class="sxs-lookup"><span data-stu-id="c26a1-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="c26a1-111">如果此應用程式有 Node.js 後端，則為 [Android Studio](https://developer.android.com/sdk/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c26a1-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="c26a1-112">如果此應用程式有 Microsoft .NET 後端，則為 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c26a1-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="c26a1-113">Android 2.3 或更新版本、Google Repository 版本 27 或更新版本，以及 Firebase 雲端傳訊適用的 Google Play 服務 9.0.2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c26a1-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="c26a1-114">完整的 hello [Android 的快速入門]。</span><span class="sxs-lookup"><span data-stu-id="c26a1-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="c26a1-115">建立支援 Firebase 雲端通訊的專案</span><span class="sxs-lookup"><span data-stu-id="c26a1-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="c26a1-116">設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="c26a1-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="c26a1-117">設定 Azure toosend 推播通知</span><span class="sxs-lookup"><span data-stu-id="c26a1-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="c26a1-118">啟用 hello 伺服器專案的推播通知</span><span class="sxs-lookup"><span data-stu-id="c26a1-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="c26a1-119">新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="c26a1-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="c26a1-120">在本節中，您會更新用戶端的 Android 應用程式 toohandle 推播通知。</span><span class="sxs-lookup"><span data-stu-id="c26a1-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="c26a1-121">驗證 Android SDK 版本</span><span class="sxs-lookup"><span data-stu-id="c26a1-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="c26a1-122">下一步是 tooinstall Google Play 服務 」。</span><span class="sxs-lookup"><span data-stu-id="c26a1-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="c26a1-123">Google Cloud Messaging 有最小 API 層級需求的開發和測試，哪些 hello **minSdkVersion** hello 資訊清單中的屬性必須符合。</span><span class="sxs-lookup"><span data-stu-id="c26a1-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="c26a1-124">如果您要測試的較舊的裝置，請參閱[設定總 Google 播放 Services SDK] toodetermine 如何低您可以設定此值，並適當地進行設定。</span><span class="sxs-lookup"><span data-stu-id="c26a1-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="c26a1-125">將 Google Play 服務 toohello 專案</span><span class="sxs-lookup"><span data-stu-id="c26a1-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="c26a1-126">新增程式碼</span><span class="sxs-lookup"><span data-stu-id="c26a1-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="c26a1-127">針對 hello 測試 hello 應用程式發行行動服務</span><span class="sxs-lookup"><span data-stu-id="c26a1-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="c26a1-128">藉由直接附加的 Android 手機，使用 USB 纜線，或使用虛擬裝置 hello 模擬器中，您可以測試 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c26a1-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c26a1-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c26a1-129">Next steps</span></span>
<span data-ttu-id="c26a1-130">現在，您完成本教學課程，請考慮 tooone hello 遵循教學課程的上繼續進行：</span><span class="sxs-lookup"><span data-stu-id="c26a1-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="c26a1-131">[新增驗證 tooyour Android 應用程式](app-service-mobile-android-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="c26a1-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="c26a1-132">了解 tooadd 驗證 toohello todolist 快速入門使用支援的身分識別提供者在 Android 上的專案。</span><span class="sxs-lookup"><span data-stu-id="c26a1-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="c26a1-133">[啟用 Android 應用程式的離線同步處理](app-service-mobile-android-get-started-offline-data.md)。</span><span class="sxs-lookup"><span data-stu-id="c26a1-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="c26a1-134">了解如何離線 tooadd 支援 tooyour 應用程式使用的行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="c26a1-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="c26a1-135">使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="c26a1-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android 的快速入門]: app-service-mobile-android-get-started.md

[設定總 Google 播放 Services SDK]:https://developers.google.com/android/guides/setup
