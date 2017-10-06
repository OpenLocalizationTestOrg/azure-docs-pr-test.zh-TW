---
title: "aaaAdd 推播通知 tooyour Xamarin.Android 應用程式 |Microsoft 文件"
description: "了解如何 toouse Azure App Service 與 Azure 通知中樞 toosend 推播通知 tooyour Xamarin.Android 應用程式"
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="0ab85-103">新增推播通知 tooyour Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ab85-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0ab85-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0ab85-104">Overview</span></span>
<span data-ttu-id="0ab85-105">在本教學課程中，您將加入推播通知 toohello [Xamarin.Android 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="0ab85-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="0ab85-106">如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="0ab85-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="0ab85-107">請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0ab85-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ab85-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="0ab85-108">Prerequisites</span></span>
<span data-ttu-id="0ab85-109">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="0ab85-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0ab85-110">有效的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ab85-110">An active Google account.</span></span> <span data-ttu-id="0ab85-111">您可以在 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)註冊 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ab85-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="0ab85-112">[Google Cloud Messaging 用戶端元件](http://components.xamarin.com/view/GCMClient/)。</span><span class="sxs-lookup"><span data-stu-id="0ab85-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="0ab85-113"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="0ab85-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="0ab85-114"><a id="register"></a>啟用 Firebase 雲端傳訊</span><span class="sxs-lookup"><span data-stu-id="0ab85-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="0ab85-115">設定 Azure toosend 推播要求</span><span class="sxs-lookup"><span data-stu-id="0ab85-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="0ab85-116"><a id="update-server"></a>更新 hello 伺服器專案 toosend 推播通知</span><span class="sxs-lookup"><span data-stu-id="0ab85-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="0ab85-117"><a id="configure-app"></a>設定推播通知的 hello 用戶端專案</span><span class="sxs-lookup"><span data-stu-id="0ab85-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="0ab85-118"><a id="add-push"></a>新增推播通知的程式碼 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ab85-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="0ab85-119"><a name="test"></a>在應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="0ab85-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="0ab85-120">您可以使用虛擬裝置 hello 模擬器中測試 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ab85-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="0ab85-121">在模擬器上執行時，您需要採取其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="0ab85-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="0ab85-122">請確定您要部署 tooor 偵錯包含 Google Api 將設為 hello 目標，如下所示 hello Android Virtual Device (AVD) manager 中的虛擬裝置上。</span><span class="sxs-lookup"><span data-stu-id="0ab85-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="0ab85-123">按一下 新增 Google 帳戶 toohello Android 裝置**應用程式** > **設定** > **將帳戶加入**，然後依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="0ab85-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="0ab85-124">執行 hello todolist 應用程式做之前，插入新的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="0ab85-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="0ab85-125">此時，通知圖示會顯示 hello 通知區域中。</span><span class="sxs-lookup"><span data-stu-id="0ab85-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="0ab85-126">您可以開啟 hello 通知抽屜 tooview hello 全文檢索的 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="0ab85-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
