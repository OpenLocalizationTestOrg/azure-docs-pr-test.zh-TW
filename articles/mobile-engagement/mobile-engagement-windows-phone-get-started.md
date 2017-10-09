---
title: "aaaGet 開始使用 Azure Mobile Engagement 的 Windows Phone Silverlight 應用程式"
description: "深入了解如何 toouse Azure Mobile Engagement 與為 Windows Phone Silverlight 應用程式的分析和推播通知。"
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="439b7-103">開始使用適用於 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="439b7-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="439b7-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者的 Windows Phone Silverlight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="439b7-105">本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。</span><span class="sxs-lookup"><span data-stu-id="439b7-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="439b7-106">在課程中，您將建立一個空白的 Windows Phone Silverlight 應用程式，以使用 Microsoft 推播通知服務 (MPNS) 來收集基本資料及接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="439b7-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-107">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="439b7-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="439b7-108">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="439b7-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-109">Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="439b7-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="439b7-110">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="439b7-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-111">如果您的目標 Windows Phone 8.1 (非 Silverlight)，請參閱 toohello [Windows 通用的教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="439b7-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="439b7-112">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="439b7-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="439b7-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="439b7-113">Visual Studio 2013</span></span>
* <span data-ttu-id="439b7-114">[MicrosoftAzure.MobileEngagement] Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="439b7-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="439b7-115">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="439b7-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="439b7-116">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="439b7-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="439b7-117">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started)。</span><span class="sxs-lookup"><span data-stu-id="439b7-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="439b7-118"><a id="setup-azme"></a>設定 Windows Phone 應用程式的 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="439b7-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="439b7-119"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="439b7-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="439b7-120">此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="439b7-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="439b7-121">hello 完整的整合文件可以在 hello [Mobile Engagement Windows Phone SDK 整合](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="439b7-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="439b7-122">我們會建立基本應用程式與 Visual Studio toodemonstrate hello 整合。</span><span class="sxs-lookup"><span data-stu-id="439b7-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="439b7-123">建立新的 Windows Phone Silverlight 專案</span><span class="sxs-lookup"><span data-stu-id="439b7-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="439b7-124">hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。</span><span class="sxs-lookup"><span data-stu-id="439b7-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="439b7-125">啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。</span><span class="sxs-lookup"><span data-stu-id="439b7-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="439b7-126">在 hello 快顯視窗中，選取  **Windows 8** -> **Windows Phone** -> **空白應用程式 (Windows Phone Silverlight)**。</span><span class="sxs-lookup"><span data-stu-id="439b7-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="439b7-127">Hello 應用程式中填滿**名稱**和**方案名稱**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="439b7-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="439b7-128">您可以選擇 tootarget 或是**Windows Phone 8.0**或**Windows Phone 8.1**。</span><span class="sxs-lookup"><span data-stu-id="439b7-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="439b7-129">您現在已建立新的 Windows Phone Silverlight 應用程式，我們將會在其中整合 hello Azure Mobile Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="439b7-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="439b7-130">連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="439b7-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="439b7-131">安裝 hello [MicrosoftAzure.MobileEngagement]專案中的 nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="439b7-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="439b7-132">開啟`WMAppManifest.xml`（hello 屬性 資料夾） 下，並確定 hello 下列宣告 （加入它們如果不是） 在 hello`<Capabilities />`標記：</span><span class="sxs-lookup"><span data-stu-id="439b7-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="439b7-133">現在貼上您先前複製您的 Mobile Engagement 應用程式的 hello 連接字串，並將它貼在 hello `Resources\EngagementConfiguration.xml` hello 之間的檔案，`<connectionString>`和`</connectionString>`標記：</span><span class="sxs-lookup"><span data-stu-id="439b7-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="439b7-134">在 hello`App.xaml.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="439b7-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="439b7-135">a.</span><span class="sxs-lookup"><span data-stu-id="439b7-135">a.</span></span> <span data-ttu-id="439b7-136">新增 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="439b7-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="439b7-137">b.</span><span class="sxs-lookup"><span data-stu-id="439b7-137">b.</span></span> <span data-ttu-id="439b7-138">初始化 hello SDK 中 hello`Application_Launching`方法：</span><span class="sxs-lookup"><span data-stu-id="439b7-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="439b7-139">c.</span><span class="sxs-lookup"><span data-stu-id="439b7-139">c.</span></span> <span data-ttu-id="439b7-140">在 hello 中插入下列 hello `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="439b7-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="439b7-141"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="439b7-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="439b7-142">在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="439b7-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="439b7-143">在 hello MainPage.xaml.cs，新增 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="439b7-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="439b7-144">取代 hello 基底類別**MainPage**，這是之前**PhoneApplicationPage**，與**EngagementPage**。</span><span class="sxs-lookup"><span data-stu-id="439b7-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="439b7-145">在您的 `MainPage.xml` 檔案中：</span><span class="sxs-lookup"><span data-stu-id="439b7-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="439b7-146">a.</span><span class="sxs-lookup"><span data-stu-id="439b7-146">a.</span></span> <span data-ttu-id="439b7-147">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="439b7-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="439b7-148">b.</span><span class="sxs-lookup"><span data-stu-id="439b7-148">b.</span></span> <span data-ttu-id="439b7-149">取代`phone:PhoneApplicationPage`hello XML 標記名稱與`engagement:EngagementPage`。</span><span class="sxs-lookup"><span data-stu-id="439b7-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="439b7-150"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="439b7-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="439b7-151"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="439b7-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="439b7-152">Mobile Engagement 可讓您 toointeract，並連線到您推播通知與 hello 內容的活動中的應用程式內訊息的使用者。</span><span class="sxs-lookup"><span data-stu-id="439b7-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="439b7-153">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="439b7-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="439b7-154">hello 下列各節將設定您的應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="439b7-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="439b7-155">啟用您的應用程式 tooreceive MPNS 的推播通知</span><span class="sxs-lookup"><span data-stu-id="439b7-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="439b7-156">加入新的功能 tooyour`WMAppManifest.xml`檔案：</span><span class="sxs-lookup"><span data-stu-id="439b7-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="439b7-157">初始化 hello REACH SDK</span><span class="sxs-lookup"><span data-stu-id="439b7-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="439b7-158">在`App.xaml.cs`，呼叫`EngagementReach.Instance.Init();`在 hello **Application_Launching**函式，後面 hello 代理程式初始化：</span><span class="sxs-lookup"><span data-stu-id="439b7-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="439b7-159">在`App.xaml.cs`，呼叫`EngagementReach.Instance.OnActivated(e);`在 hello **Application_Activated**函式，後面 hello 代理程式初始化：</span><span class="sxs-lookup"><span data-stu-id="439b7-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="439b7-160">您全都準備好了。</span><span class="sxs-lookup"><span data-stu-id="439b7-160">You're all set.</span></span> <span data-ttu-id="439b7-161">現在我們要驗證您已正確完成這項基本整合。</span><span class="sxs-lookup"><span data-stu-id="439b7-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="439b7-162"><a id="send"></a>傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="439b7-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="439b7-163">您現在應該會看到通知將會顯示您裝置上以應用程式內通知是否 hello 應用程式開啟否則當做快顯通知 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="439b7-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
