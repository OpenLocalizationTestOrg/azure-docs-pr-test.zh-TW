---
title: "aaaGet Started with Xamarin.Android 的 Azure Mobile Engagement"
description: "深入了解如何使用分析及推播通知 Xamarin.Android 應用程式的 Azure Mobile Engagement toouse。"
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="59236-103">開始使用適用於 Xamarin.Android 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="59236-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="59236-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和 toosend 推播通知 toosegmented 使用者 Xamarin.Android 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="59236-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="59236-105">本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。</span><span class="sxs-lookup"><span data-stu-id="59236-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="59236-106">在本教學課程中，您將使用 Google 雲端通訊 (GCM)，建立可收集基本資料和接收推播通知的空白 Xamarin.Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59236-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="59236-107">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="59236-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="59236-108">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="59236-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="59236-109">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="59236-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="59236-110">[Xamarin Studio](http://xamarin.com/studio)。</span><span class="sxs-lookup"><span data-stu-id="59236-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="59236-111">您也可以使用 Visual Studio 搭配 Xamarin，但本教學課程會使用 Xamarin Studio。</span><span class="sxs-lookup"><span data-stu-id="59236-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="59236-112">如需安裝指示，請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59236-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="59236-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="59236-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="59236-114">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59236-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="59236-115">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="59236-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="59236-116">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="59236-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="59236-117"><a id="setup-azme"></a>為您的 Android 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="59236-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="59236-118"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="59236-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="59236-119">此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="59236-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="59236-120">我們將使用 Xamarin Studio toodemonstrate hello 整合來建立基本應用程式。</span><span class="sxs-lookup"><span data-stu-id="59236-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="59236-121">建立新的 Xamarin.Android 專案</span><span class="sxs-lookup"><span data-stu-id="59236-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="59236-122">啟動**Xamarin Studio**太移**檔案** -> **新增** -> **方案**</span><span class="sxs-lookup"><span data-stu-id="59236-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="59236-123">選取**Android 應用程式**確定選取的 hello 語言是**C#**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="59236-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="59236-124">填寫 hello**應用程式名稱**和 hello**組織識別碼**。</span><span class="sxs-lookup"><span data-stu-id="59236-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="59236-125">請確定 toocheckmark **Google Play 服務**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="59236-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="59236-126">更新 hello**專案名稱**，**方案名稱**和**位置**如果需要，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="59236-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="59236-127">Xamarin Studio 將會建立在其中，我們將會整合 Mobile Engagement hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59236-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="59236-128">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="59236-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="59236-129">以滑鼠右鍵按一下 hello**封裝**hello 方案 windows 和選取資料夾**新增套件...**</span><span class="sxs-lookup"><span data-stu-id="59236-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="59236-130">搜尋 hello **Microsoft Azure Mobile Engagement Xamarin SDK**並將它加入 tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="59236-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="59236-131">開啟**Weatherapp**並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="59236-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="59236-132">在 hello`OnCreate`方法中，新增下列 tooinitialize hello 連線與 Mobile Engagement 後端的 hello。</span><span class="sxs-lookup"><span data-stu-id="59236-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="59236-133">請確定 tooadd 您**ConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="59236-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="59236-134">新增權限和服務宣告</span><span class="sxs-lookup"><span data-stu-id="59236-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="59236-135">開啟 [hello **Manifest.xml** hello 屬性] 資料夾下的檔案。</span><span class="sxs-lookup"><span data-stu-id="59236-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="59236-136">選取來源 索引標籤，好讓您直接更新 hello XML 來源。</span><span class="sxs-lookup"><span data-stu-id="59236-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="59236-137">加入這些權限 toohello Manifest.xml (這可以在 hello 下找到**屬性**資料夾) 的專案之前或之後 hello`<application>`標記：</span><span class="sxs-lookup"><span data-stu-id="59236-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="59236-138">新增 hello 下列之間 hello`<application>`和`</application>`標記 toodeclare hello 代理程式服務：</span><span class="sxs-lookup"><span data-stu-id="59236-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="59236-139">在您剛才貼上 hello 程式碼，取代`"<Your application name>"`hello 標籤中。</span><span class="sxs-lookup"><span data-stu-id="59236-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="59236-140">這會顯示在 hello**設定**功能表的使用者可以查看 hello 裝置上執行服務的位置。</span><span class="sxs-lookup"><span data-stu-id="59236-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="59236-141">您可以加入 hello word 「 服務 」，例如在該標籤。</span><span class="sxs-lookup"><span data-stu-id="59236-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="59236-142">傳送螢幕 tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="59236-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="59236-143">在訂單 toostart 傳送資料，並確保 hello 的使用者，您必須傳送至少一個螢幕 toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="59236-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="59236-144">執行此作業-請確認該 hello`MainActivity`繼承自`EngagementActivity`而不是`Activity`。</span><span class="sxs-lookup"><span data-stu-id="59236-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="59236-145">或者，如果您無法繼承自 `EngagementActivity`，則必須分別在 `OnResume` 和 `OnPause` 中新增 `.StartActivity` 和 `.EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="59236-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="59236-146"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="59236-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="59236-147"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="59236-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="59236-148">Mobile Engagement 可讓您與 toointeract，並連線到您的推播通知及應用程式內訊息的活動 hello 內容中的使用者。</span><span class="sxs-lookup"><span data-stu-id="59236-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="59236-149">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="59236-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="59236-150">下列各節的 hello 設定您的應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="59236-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
