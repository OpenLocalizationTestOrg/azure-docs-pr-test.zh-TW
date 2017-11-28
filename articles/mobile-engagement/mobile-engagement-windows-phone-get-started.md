---
title: "開始使用適用於 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement"
description: "了解如何使用適用於 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement 執行分析和傳送推播通知。"
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
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="7a358-103">開始使用適用於 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7a358-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="7a358-104">本主題說明如何使用 Azure Mobile Engagement 了解您的應用程式使用狀況，以及傳送推播通知給 Windows Phone Silverlight 應用程式的分佈使用者。</span><span class="sxs-lookup"><span data-stu-id="7a358-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="7a358-105">本教學課程將示範使用 Mobile Engagement 的簡單廣播案例。</span><span class="sxs-lookup"><span data-stu-id="7a358-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="7a358-106">在課程中，您將建立一個空白的 Windows Phone Silverlight 應用程式，以使用 Microsoft 推播通知服務 (MPNS) 來收集基本資料及接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="7a358-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="7a358-107">Azure Mobile Engagement 服務將於 2018 年 3 月淘汰，目前僅供現有客戶使用。</span><span class="sxs-lookup"><span data-stu-id="7a358-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="7a358-108">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="7a358-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="7a358-109">Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="7a358-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="7a358-110">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="7a358-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="7a358-111">如果您的目標是 Windows Phone 8.1 (非 Silverlight)，請參閱 [Windows 通用教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7a358-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="7a358-112">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="7a358-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="7a358-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7a358-113">Visual Studio 2013</span></span>
* <span data-ttu-id="7a358-114">[MicrosoftAzure.MobileEngagement] Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="7a358-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="7a358-115">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a358-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7a358-116">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a358-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7a358-117">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started)。</span><span class="sxs-lookup"><span data-stu-id="7a358-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="7a358-118"><a id="setup-azme"></a>設定 Windows Phone 應用程式的 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7a358-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="7a358-119"><a id="connecting-app"></a>將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="7a358-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="7a358-120">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知時必要的最低設定。</span><span class="sxs-lookup"><span data-stu-id="7a358-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="7a358-121">您可以在 [Mobile Engagement Windows Phone SDK 整合](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7a358-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="7a358-122">我們將會使用 Visual Studio 建立基本應用程式來示範整合。</span><span class="sxs-lookup"><span data-stu-id="7a358-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="7a358-123">建立新的 Windows Phone Silverlight 專案</span><span class="sxs-lookup"><span data-stu-id="7a358-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="7a358-124">即使下列步驟與舊版 Visual Studio 中的步驟類似，但這些步驟假設使用的是 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="7a358-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="7a358-125">啟動 Visual Studio，並在 [首頁] 畫面上選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="7a358-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="7a358-126">在快顯視窗中，依序選取 [Windows 8] -> [Windows Phone] ->  -> [空白應用程式 (Windows Phone Silverlight)]。</span><span class="sxs-lookup"><span data-stu-id="7a358-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="7a358-127">輸入應用程式的 [名稱] 和 [方案名稱]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a358-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="7a358-128">您可以選擇要將目標設為 **Windows Phone 8.0** 或 **Windows Phone 8.1**。</span><span class="sxs-lookup"><span data-stu-id="7a358-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="7a358-129">現在已建立新的 Windows Phone Silverlight 應用程式，接著我們要將 Azure Mobile Engagement SDK 整合至其中。</span><span class="sxs-lookup"><span data-stu-id="7a358-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="7a358-130">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="7a358-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="7a358-131">在您的專案中安裝 [MicrosoftAzure.MobileEngagement] NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="7a358-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="7a358-132">在 Properties 資料夾中開啟 `WMAppManifest.xml`，然後確認 `<Capabilities />` 標記中已宣告下列項目 (如果沒有宣告，請自行新增)：</span><span class="sxs-lookup"><span data-stu-id="7a358-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="7a358-133">現在貼上您稍早為 Mobile Engagement 應用程式複製的連接字串，並將該字串貼在 `Resources\EngagementConfiguration.xml` 檔案中的 `<connectionString>` 和 `</connectionString>` 標記之間：</span><span class="sxs-lookup"><span data-stu-id="7a358-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="7a358-134">在 `App.xaml.cs` 檔案中：</span><span class="sxs-lookup"><span data-stu-id="7a358-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="7a358-135">a.</span><span class="sxs-lookup"><span data-stu-id="7a358-135">a.</span></span> <span data-ttu-id="7a358-136">新增 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7a358-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="7a358-137">b.</span><span class="sxs-lookup"><span data-stu-id="7a358-137">b.</span></span> <span data-ttu-id="7a358-138">在 `Application_Launching` 方法中初始化 SDK：</span><span class="sxs-lookup"><span data-stu-id="7a358-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="7a358-139">c.</span><span class="sxs-lookup"><span data-stu-id="7a358-139">c.</span></span> <span data-ttu-id="7a358-140">在 `Application_Activated` 中插入以下內容：</span><span class="sxs-lookup"><span data-stu-id="7a358-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="7a358-141"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="7a358-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="7a358-142">若要開始傳送資料並確定使用者正在使用，您必須至少傳送一個畫面 (活動) 到 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="7a358-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="7a358-143">在 MainPage.xaml.cs 中，加入 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7a358-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="7a358-144">請以 **EngagementPage** 取代 **MainPage** 的基礎類別 (在 **PhoneApplicationPage** 之前)。</span><span class="sxs-lookup"><span data-stu-id="7a358-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="7a358-145">在您的 `MainPage.xml` 檔案中：</span><span class="sxs-lookup"><span data-stu-id="7a358-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="7a358-146">a.</span><span class="sxs-lookup"><span data-stu-id="7a358-146">a.</span></span> <span data-ttu-id="7a358-147">新增命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="7a358-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="7a358-148">b.</span><span class="sxs-lookup"><span data-stu-id="7a358-148">b.</span></span> <span data-ttu-id="7a358-149">以 `engagement:EngagementPage` 取代 XML 標記名稱內的 `phone:PhoneApplicationPage`。</span><span class="sxs-lookup"><span data-stu-id="7a358-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="7a358-150"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="7a358-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="7a358-151"><a id="integrate-push"></a>啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="7a358-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="7a358-152">Mobile Engagement 可讓您透過「推播通知」和「應用程式內傳訊」，於活動進行時與使用者互動和觸達。</span><span class="sxs-lookup"><span data-stu-id="7a358-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="7a358-153">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="7a358-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="7a358-154">以下各節將設定您的用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="7a358-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="7a358-155">啟用您的應用程式接收 MPNS 推播通知</span><span class="sxs-lookup"><span data-stu-id="7a358-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="7a358-156">新增「功能」到您的 `WMAppManifest.xml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="7a358-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="7a358-157">初始化 REACH SDK</span><span class="sxs-lookup"><span data-stu-id="7a358-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="7a358-158">在 `App.xaml.cs` 中，於代理程式初始化後，在 **Application_Launching** 函式中呼叫 `EngagementReach.Instance.Init();`：</span><span class="sxs-lookup"><span data-stu-id="7a358-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="7a358-159">在 `App.xaml.cs` 中，於代理程式初始化後，在 **Application_Activated** 函式中呼叫 `EngagementReach.Instance.OnActivated(e);`：</span><span class="sxs-lookup"><span data-stu-id="7a358-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="7a358-160">您全都準備好了。</span><span class="sxs-lookup"><span data-stu-id="7a358-160">You're all set.</span></span> <span data-ttu-id="7a358-161">現在我們要驗證您已正確完成這項基本整合。</span><span class="sxs-lookup"><span data-stu-id="7a358-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="7a358-162"><a id="send"></a>傳送通知至應用程式</span><span class="sxs-lookup"><span data-stu-id="7a358-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="7a358-163">您現在應該會在裝置上看到通知，其會顯示為應用程式內通知 (如果應用程式已開啟)，否則會顯示為快顯通知，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7a358-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="7a358-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="7a358-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
