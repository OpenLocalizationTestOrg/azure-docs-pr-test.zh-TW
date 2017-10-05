---
title: "將推播通知新增至 Xamarin.Android 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure App Service 及 Azure 通知中樞將推播通知傳送到 Xamarin.Android 應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="7bc0c-103">將推播通知新增至 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="7bc0c-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="7bc0c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7bc0c-104">Overview</span></span>
<span data-ttu-id="7bc0c-105">在本教學課程中，您會將推播通知新增至 [Xamarin.Android 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便在每次插入一筆記錄時傳送推播通知至裝置。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="7bc0c-106">如果您不要使用下載的快速入門伺服器專案，將需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="7bc0c-107">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bc0c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7bc0c-108">Prerequisites</span></span>
<span data-ttu-id="7bc0c-109">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="7bc0c-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="7bc0c-110">有效的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-110">An active Google account.</span></span> <span data-ttu-id="7bc0c-111">您可以在 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)註冊 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="7bc0c-112">[Google Cloud Messaging 用戶端元件](http://components.xamarin.com/view/GCMClient/)。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="7bc0c-113"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="7bc0c-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="7bc0c-114"><a id="register"></a>啟用 Firebase 雲端傳訊</span><span class="sxs-lookup"><span data-stu-id="7bc0c-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="7bc0c-115">設定 Azure 來傳送推播要求</span><span class="sxs-lookup"><span data-stu-id="7bc0c-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="7bc0c-116"><a id="update-server"></a>更新伺服器專案以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="7bc0c-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="7bc0c-117"><a id="configure-app"></a>設定用於推播通知的用戶端專案</span><span class="sxs-lookup"><span data-stu-id="7bc0c-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="7bc0c-118"><a id="add-push"></a>將推播通知程式碼新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="7bc0c-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="7bc0c-119"><a name="test"></a>在應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="7bc0c-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="7bc0c-120">您可以在模擬器中使用虛擬裝置來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="7bc0c-121">在模擬器上執行時，您需要採取其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="7bc0c-122">針對您要部署的目的地虛擬裝置或偵錯的所在虛擬裝置，請確認該裝置具有已設定為目標的 Google API，如以下 Android 虛擬裝置管理員 (AVD) 所示。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="7bc0c-123">按一下 [應用程式] > [設定] > [新增帳戶] 將 Google 帳戶加入 Android 裝置，然後遵循提示。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="7bc0c-124">按照先前的方法執行 todolist 應用程式，然後插入新的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="7bc0c-125">這次，通知圖示會顯示在通知區域中。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="7bc0c-126">您可以開啟通知抽屜來檢視通知的完整內容。</span><span class="sxs-lookup"><span data-stu-id="7bc0c-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
