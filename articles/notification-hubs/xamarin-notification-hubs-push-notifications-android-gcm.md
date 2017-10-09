---
title: "aaaGet Xamarin.Android 應用程式入門通知中心 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooa Xamarin Android 應用程式。"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="6cc0a-103">開始使用適用於 Android 應用程式的通知中樞</span><span class="sxs-lookup"><span data-stu-id="6cc0a-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6cc0a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6cc0a-104">Overview</span></span>
<span data-ttu-id="6cc0a-105">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa Xamarin.Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="6cc0a-106">您將建立可使用 Google Cloud Messaging (GCM) 接收推播通知的空白 Xamarin.Android app。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="6cc0a-107">完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="6cc0a-108">hello 完成會提供程式碼 hello[通知中樞應用程式][ GitHub]範例。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="6cc0a-109">本教學課程示範 hello 簡單廣播的案例中使用通知中樞。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6cc0a-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="6cc0a-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="6cc0a-111">hello 完成本教學課程中的程式碼可以在 GitHub 上找到[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cc0a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="6cc0a-112">Prerequisites</span></span>
<span data-ttu-id="6cc0a-113">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6cc0a-114">Windows 的 Visual Studio 與 Xamarin 或 Mac OS X 的 Xamarin Studio。完整的安裝指示位於[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="6cc0a-115">有效的 Google 帳戶</span><span class="sxs-lookup"><span data-stu-id="6cc0a-115">Active Google account</span></span>
* <span data-ttu-id="6cc0a-116">[Azure 訊息元件]</span><span class="sxs-lookup"><span data-stu-id="6cc0a-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="6cc0a-117">[Google Cloud Messaging 用戶端元件]</span><span class="sxs-lookup"><span data-stu-id="6cc0a-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="6cc0a-118">完成本教學課程是 Xamarin.Android 應用程式所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cc0a-119">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6cc0a-120">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6cc0a-121">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="6cc0a-122">啟用 Google 雲端通訊</span><span class="sxs-lookup"><span data-stu-id="6cc0a-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="6cc0a-123">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="6cc0a-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="6cc0a-124">按一下 hello<b>設定</b>hello 頂端索引標籤上，輸入 hello <b>API 金鑰</b>hello 上一節，取得值，然後按一下<b>儲存</b>。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="6cc0a-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="6cc0a-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="6cc0a-126">通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 連接字串 tooboth 註冊您的應用程式 tooreceive 通知和 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="6cc0a-127">連接您的應用程式 toohello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="6cc0a-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="6cc0a-128">建立新專案</span><span class="sxs-lookup"><span data-stu-id="6cc0a-128">Create a new project</span></span>
1. <span data-ttu-id="6cc0a-129">在 Xamarin Studio 中，依序按一下 [新增方案]、[Android 應用程式] 和 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="6cc0a-130">輸入您的**應用程式名稱**和**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="6cc0a-131">按一下 hello**目標平台**toosupport 然後再按一下**下一步**和**建立**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="6cc0a-132">這會建立新的 Android 專案。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="6cc0a-133">Hello 方案檢視中新的專案上按一下滑鼠右鍵，然後選擇開啟 hello 專案屬性**選項**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="6cc0a-134">選取 hello **Android 應用程式**hello 中的項目**建置**> 一節。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="6cc0a-135">請確定該 hello 第一個字母您**封裝名稱**是小寫。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6cc0a-136">hello 的 hello 封裝名稱的第一個字母必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="6cc0a-137">否則，當您在下文為推播通知註冊 **BroadcastReceiver** 和 **IntentFilter** 時，將收到應用程式資訊清單錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="6cc0a-138">（選擇性） 組 hello **Android 最小版本**tooanother API 層級。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="6cc0a-139">（選擇性） 組 hello**目標 Android 版本**toohello 想的 tootarget （必須是應用程式開發介面層級 8 或更新版本） 的另一個應用程式開發介面版本。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="6cc0a-140">按一下**確定**和關閉 hello 專案選項 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="6cc0a-141">加入 hello 必要的元件 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="6cc0a-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="6cc0a-142">hello Google 雲端訊息用戶端 hello Xamarin 元件存放區提供簡化 Xamarin.Android 支援推播通知的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="6cc0a-143">Xamarin.Android 應用程式中的 hello Components 資料夾上按一下滑鼠右鍵，然後選擇 **取得多元件**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="6cc0a-144">搜尋 hello **Azure 訊息**元件並將它加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="6cc0a-145">搜尋 hello **Google 雲端訊息用戶端**元件並將它加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="6cc0a-146">在專案中設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="6cc0a-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="6cc0a-147">收集下列資訊 Android 應用程式與通知中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="6cc0a-148">**GoogleProjectNumber**： 取得此專案數字值從 hello hello Google 開發人員入口網站上的應用程式的概觀。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="6cc0a-149">記下這個值前面的 hello 入口網站上建立 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="6cc0a-150">**接聽的連接字串**: hello 儀表板中 hello [Azure 傳統入口網站]，按一下 **檢視連接字串**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="6cc0a-151">複製 hello *DefaultListenSharedAccessSignature*連接字串，這個值。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="6cc0a-152">**中樞名稱**： 這是您的中樞，從 hello hello 名稱[Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="6cc0a-153">例如， *mynotificationhub2*。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="6cc0a-154">建立**Constants.cs** Xamarin 專案的類別，並定義下列 hello 類別中的常數值的 hello。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="6cc0a-155">Hello 預留位置取代為您的值。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="6cc0a-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="6cc0a-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="6cc0a-157">}</span><span class="sxs-lookup"><span data-stu-id="6cc0a-157">}</span></span>
2. <span data-ttu-id="6cc0a-158">新增 hello 下列 using 陳述式太**Weatherapp**:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="6cc0a-159">新增執行個體變數 toohello `MainActivity` hello 應用程式執行時，將會使用的 tooshow 警示 對話方塊的類別：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="6cc0a-160">建立下列方法在 hello hello **MainActivity**類別：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="6cc0a-161">在 hello`OnCreate`方法**Weatherapp**，初始化 hello`instance`變數和太加入呼叫`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="6cc0a-162">建立新類別 **MyBroadcastReceiver**。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cc0a-163">我們將在下文中從頭逐步建立 **BroadcastReceiver** 類別。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="6cc0a-164">不過，快速替代 toomanually 建立**MyBroadcastReceiver.cs**是 toorefer toohello **GcmService.cs**隨附 hello hello範例Xamarin.Android專案中找到檔案[通知中樞範例][GitHub]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="6cc0a-165">複製**GcmService.cs**和變更類別名稱可以是很好 toostart 以及。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="6cc0a-166">新增 hello 下列 using 陳述式太**MyBroadcastReceiver.cs** （toohello 元件，並針對您先前加入的組件參考）：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="6cc0a-167">在**MyBroadcastReceiver.cs**，新增下列權限要求之間 hello hello**使用**陳述式和 hello**命名空間**宣告：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="6cc0a-168">在**MyBroadcastReceiver.cs**，變更 hello **MyBroadcastReceiver**類別 toomatch hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="6cc0a-169">在 **MyBroadcastReceiver.cs** 中，新增另一個衍生自 **GcmServiceBase** 且名稱為 **PushHandlerService** 的類別。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="6cc0a-170">請確定 tooapply hello**服務**屬性 toohello 類別：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="6cc0a-171">**GcmServiceBase** 實作 **OnRegistered()**、**OnUnRegistered()**、**OnMessage()**、**OnRecoverableError()** 和 **OnError()** 等方法。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="6cc0a-172">我們**PushHandlerService**實作類別必須覆寫這些方法，而且這些方法會引發在回應 toointeracting 與 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="6cc0a-173">覆寫 hello **OnRegistered()**方法中的**PushHandlerService**使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="6cc0a-174">在 hello **OnRegistered()**上述程式碼，您應該會注意到 hello 能力 toospecify 標記 tooregister 特定訊息的通道。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="6cc0a-175">覆寫 hello **OnMessage**方法中的**PushHandlerService**使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="6cc0a-176">新增下列 hello **createNotification**和**dialogNotify**方法太**PushHandlerService**收到通知時，通知使用者。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6cc0a-177">Android 5.0 版與更新版本中的通知設計，與先前版本有極大的不同。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="6cc0a-178">如果您測試 Android 5.0 或更新版本，hello 應用程式需要 toobe 執行 tooreceive hello 通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="6cc0a-179">如需詳細資訊，請參閱 [Android 通知](http://go.microsoft.com/fwlink/?LinkId=615880)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="6cc0a-180">覆寫抽象成員 **OnUnRegistered()**、**OnRecoverableError()** 和 **OnError()**，以便您的程式碼進行編譯：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="6cc0a-181">Hello 模擬器中執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="6cc0a-181">Run your app in hello emulator</span></span>
<span data-ttu-id="6cc0a-182">如果您在 hello 模擬器中執行此應用程式，請確定您使用 Android 虛擬裝置 (AVD) 支援 Google 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cc0a-183">在順序 tooreceive 推播通知，您必須設定 Android 虛擬裝置上的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="6cc0a-184">(在 hello 模擬器中，瀏覽過**設定**按一下**新增帳戶**。)此外，請確定該 hello 模擬器連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="6cc0a-185">Android 5.0 版與更新版本中的通知設計，與先前版本有極大的不同。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="6cc0a-186">如需詳細資訊，請參閱 [Android 通知](http://go.microsoft.com/fwlink/?LinkId=615880)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="6cc0a-187">從 工具 中，按一下 Open Android Emulator Manager，選取您的裝置，然後按一下Edit。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="6cc0a-188">在 目標 中選取 Google API，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="6cc0a-189">Hello 頂端工具列上，按一下**執行**，然後選取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="6cc0a-190">這會啟動 hello 模擬器，並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="6cc0a-191">hello 應用程式擷取 hello *registrationId*從 GCM 以及與 hello 通知中樞的暫存器。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="6cc0a-192">從後端傳送通知</span><span class="sxs-lookup"><span data-stu-id="6cc0a-192">Send notifications from your backend</span></span>
<span data-ttu-id="6cc0a-193">您可以測試應用程式中接收通知，傳送通知給 hello 以[Azure 傳統入口網站]hello 透過偵錯索引標籤上 hello 通知中樞，囉 」 畫面下方所示。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="6cc0a-194">推播通知通常會在後端服務 (例如行動服務) 中或透過相容程式庫的 ASP.NET 傳送。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="6cc0a-195">您也可以使用 hello REST API 直接 toosend 通知訊息，如果文件庫不適用於您的後端。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="6cc0a-196">以下是一些您可能想要 tooreview 傳送通知的教學課程清單：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="6cc0a-197">ASP.NET: 請參閱 <<c0> [ 使用通知中樞 toopush 通知 toousers]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="6cc0a-198">Azure 通知中樞 Java SDK： 請參閱[如何 toouse 通知中樞，從 Java](notification-hubs-java-push-notification-tutorial.md)從 Java 傳送通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="6cc0a-199">這已在 Eclipse for Android Development 中測試。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="6cc0a-200">PHP： 請參閱[如何 toouse 通知中樞，從 PHP](notification-hubs-php-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="6cc0a-201">Hello hello 教學課程的下一個小節，您會傳送通知，藉由使用.NET 主控台應用程式和使用透過節點指令碼的行動服務。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="6cc0a-202">(選用) 使用 .NET 應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="6cc0a-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="6cc0a-203">在本節中，您將使用 .NET 主控台應用程式來傳送通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="6cc0a-204">建立新的 Visual C# 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="6cc0a-205">在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="6cc0a-206">這是 Visual Studio 中顯示 hello Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="6cc0a-207">在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cc0a-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="6cc0a-208">這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="6cc0a-209">開啟 hello Program.cs 檔案並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="6cc0a-210">在您`Program`類別中，新增下列方法 hello。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="6cc0a-211">更新 hello 預留位置文字，與您*DefaultFullSharedAccessSignature*連接字串和中樞名稱，從 hello [Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="6cc0a-212">新增下列幾行中的 hello 您**Main**方法：</span><span class="sxs-lookup"><span data-stu-id="6cc0a-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="6cc0a-213">按 F5 鍵 toorun hello 應用程式 hello。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="6cc0a-214">您應該在 hello 應用程式會收到通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="6cc0a-215">(選用) 使用行動服務傳送通知</span><span class="sxs-lookup"><span data-stu-id="6cc0a-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="6cc0a-216">依照 [開始使用行動服務]執行作業。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="6cc0a-217">登入 toohello [Azure 傳統入口網站]，然後選取您的行動服務。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="6cc0a-218">選取 hello**排程器**hello 最上層顯示 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="6cc0a-219">建立新的排定工作、插入名稱，然後選取 [隨選] 。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="6cc0a-220">建立 hello 作業時，按一下 hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="6cc0a-221">然後按一下 [hello**指令碼**hello 頂端列] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="6cc0a-222">插入 hello 遵循您的排程器函式內的指令碼。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="6cc0a-223">請確定 tooreplace hello 預留位置取代通知中樞名稱和 hello 的連接字串*DefaultFullSharedAccessSignature*您稍早取得。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="6cc0a-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="6cc0a-225">按一下**執行一次**hello 下方列上。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="6cc0a-226">您應會收到快顯通知。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cc0a-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cc0a-227">Next steps</span></span>
<span data-ttu-id="6cc0a-228">在這個簡單的範例中，您傳播通知 tooall 您的 Android 裝置。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="6cc0a-229">在排序 tootarget 特定使用者，請參閱 toohello 教學課程[ 使用通知中樞 toopush 通知 toousers]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="6cc0a-230">如果您想 toosegment 您感興趣群組的使用者，您可以閱讀[使用通知中樞 toosend 最新消息]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="6cc0a-231">深入了解如何 toouse 中的通知中樞[通知中樞指引]在 hello[通知中心如何 toofor Android]。</span><span class="sxs-lookup"><span data-stu-id="6cc0a-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[開始使用行動服務]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Azure 傳統入口網站]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[通知中心如何 toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[ 使用通知中樞 toopush 通知 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[使用通知中樞 toosend 最新消息]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging 用戶端元件]: http://components.xamarin.com/view/GCMClient/
[Azure 訊息元件]: http://components.xamarin.com/view/azure-messaging
