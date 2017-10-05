---
title: "開始使用 Windows 通用 App Azure Mobile Engagement"
description: "了解如何使用適用於 Windows 通用 App 的 Azure Mobile Engagement 執行分析和傳送推播通知。"
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="e12c4-103">開始使用適用於 Windows 通用 App 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e12c4-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e12c4-104">本主題說明如何使用 Azure Mobile Engagement 了解您的應用程式使用狀況，以及將推播通知傳送給 Windows 通用應用程式的分段使用者。</span><span class="sxs-lookup"><span data-stu-id="e12c4-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="e12c4-105">本教學課程將示範使用 Mobile Engagement 的簡單廣播案例。</span><span class="sxs-lookup"><span data-stu-id="e12c4-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="e12c4-106">您建立一個空白的 Windows 通用應用程式，以使用 Windows 通知服務 (WNS) 來收集基本的應用程式使用資料及接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="e12c4-107">Azure Mobile Engagement 服務將於 2018 年 3 月淘汰，目前僅供現有客戶使用。</span><span class="sxs-lookup"><span data-stu-id="e12c4-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="e12c4-108">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="e12c4-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e12c4-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e12c4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="e12c4-110">設定 Windows 通用應用程式的 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e12c4-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e12c4-111"><a id="connecting-app"></a>將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="e12c4-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="e12c4-112">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知所需的最低設定。</span><span class="sxs-lookup"><span data-stu-id="e12c4-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="e12c4-113">您可以在 [Mobile Engagement Windows 通用 SDK 整合](mobile-engagement-windows-store-sdk-overview.md)中找到完整的整合文件。</span><span class="sxs-lookup"><span data-stu-id="e12c4-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="e12c4-114">您使用 Visual Studio 建立基本應用程式來示範整合。</span><span class="sxs-lookup"><span data-stu-id="e12c4-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="e12c4-115">建立一個 Windows 通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="e12c4-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="e12c4-116">即使下列步驟與舊版 Visual Studio 中的步驟類似，但這些步驟假設使用的是 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="e12c4-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="e12c4-117">啟動 Visual Studio，並在 [首頁] 畫面上選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="e12c4-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="e12c4-118">在快顯視窗中，選取 [Windows] -> [通用] -> [空白應用程式 (通用 Windows)]。</span><span class="sxs-lookup"><span data-stu-id="e12c4-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="e12c4-119">輸入應用程式的 [名稱] 和 [方案名稱]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e12c4-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="e12c4-120">現在已建立 Windows 通用應用程式專案，接著您要將 Azure Mobile Engagement SDK 整合至其中。</span><span class="sxs-lookup"><span data-stu-id="e12c4-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="e12c4-121">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="e12c4-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="e12c4-122">在您的專案中安裝 [MicrosoftAzure.MobileEngagement] Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="e12c4-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="e12c4-123">如果您是以 Windows 和 Windows Phone 兩個平台為目標，您就必須對這些專案執行此操作。</span><span class="sxs-lookup"><span data-stu-id="e12c4-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="e12c4-124">對於 Windows 8.x 和 Windows Phone 8.1，相同的 Nuget 封裝會在每個專案中放置正確的平台專屬二進位檔。</span><span class="sxs-lookup"><span data-stu-id="e12c4-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="e12c4-125">開啟 **Package.appxmanifest** ，並確定已在該處新增下列功能：</span><span class="sxs-lookup"><span data-stu-id="e12c4-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="e12c4-126">現在複製您稍早為 Mobile Engagement App 複製的連接字串，並將該字串貼在 `Resources\EngagementConfiguration.xml` 檔案中的 `<connectionString>` 和 `</connectionString>` 標記之間：</span><span class="sxs-lookup"><span data-stu-id="e12c4-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="e12c4-127">如果您的應用程式以 Windows 和 Windows Phone 兩個平台為目標，那麼您仍應該建立兩個 Mobile Engagment 應用程式，讓每個支援的平台各使用一個。</span><span class="sxs-lookup"><span data-stu-id="e12c4-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="e12c4-128">建立兩個應用程式可以確保您建立正確的對象區隔，以及正確地針對各平台傳送目標式通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e12c4-129">NuGet 目前不會自動複製 Windows 10 UWP 應用程式中的 SDK 資源。</span><span class="sxs-lookup"><span data-stu-id="e12c4-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="e12c4-130">在安裝 Nuget 套件時，您必須遵循顯示的步驟 (readme.txt) 手動進行。</span><span class="sxs-lookup"><span data-stu-id="e12c4-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="e12c4-131">在 `App.xaml.cs` 檔案中：</span><span class="sxs-lookup"><span data-stu-id="e12c4-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="e12c4-132">a.</span><span class="sxs-lookup"><span data-stu-id="e12c4-132">a.</span></span> <span data-ttu-id="e12c4-133">新增 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="e12c4-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="e12c4-134">b.</span><span class="sxs-lookup"><span data-stu-id="e12c4-134">b.</span></span> <span data-ttu-id="e12c4-135">新增初始化 Engagement 的方法：</span><span class="sxs-lookup"><span data-stu-id="e12c4-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="e12c4-136">c.</span><span class="sxs-lookup"><span data-stu-id="e12c4-136">c.</span></span> <span data-ttu-id="e12c4-137">在 **OnLaunched** 方法中初始化 SDK：</span><span class="sxs-lookup"><span data-stu-id="e12c4-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="e12c4-138">c.</span><span class="sxs-lookup"><span data-stu-id="e12c4-138">c.</span></span> <span data-ttu-id="e12c4-139">在 **OnActivated** 方法中插入下列內容，並新增該方法 (如果它尚未存在)：</span><span class="sxs-lookup"><span data-stu-id="e12c4-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="e12c4-140"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="e12c4-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="e12c4-141">若要開始傳送資料並確定使用者正在使用，您必須至少傳送一個畫面 (活動) 到 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="e12c4-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e12c4-142">在 **MainPage.xaml.cs`using` 中，新增下列**  陳述式：</span><span class="sxs-lookup"><span data-stu-id="e12c4-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="e12c4-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="e12c4-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="e12c4-144">將 **MainPage** 的基底類別從 **Page** 變更為 **EngagementPageOverlay**：</span><span class="sxs-lookup"><span data-stu-id="e12c4-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="e12c4-145">在 `MainPage.xaml` 檔案中：</span><span class="sxs-lookup"><span data-stu-id="e12c4-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="e12c4-146">a.</span><span class="sxs-lookup"><span data-stu-id="e12c4-146">a.</span></span> <span data-ttu-id="e12c4-147">新增命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="e12c4-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="e12c4-148">b.</span><span class="sxs-lookup"><span data-stu-id="e12c4-148">b.</span></span> <span data-ttu-id="e12c4-149">使用 **engagement:EngagementPageOverlay** 來取代 XML 標記名稱中的 **Page**</span><span class="sxs-lookup"><span data-stu-id="e12c4-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e12c4-150">如果您的頁面會覆寫 `OnNavigatedTo` 方法，請務必呼叫 `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="e12c4-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="e12c4-151">否則不會報告活動 (`EngagementPage` 會在其 `OnNavigatedTo` 方法內呼叫 `StartActivity`)。</span><span class="sxs-lookup"><span data-stu-id="e12c4-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="e12c4-152">這在預設範本含有 `OnNavigatedTo` 方法的 Windows Phone 專案中特別重要。</span><span class="sxs-lookup"><span data-stu-id="e12c4-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="e12c4-153">對於 **Windows 10 通用應用程式**，請使用[使用 Windows 通用 App Engagement SDK 的進階報告](mobile-engagement-windows-store-advanced-reporting.md)之「建議使用的方法：多載您的 Page 類別」一節的建議方法，而非先前所述方法。</span><span class="sxs-lookup"><span data-stu-id="e12c4-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="e12c4-154"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="e12c4-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e12c4-155"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="e12c4-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e12c4-156">Mobile Engagement 可讓您透過推播通知和應用程式內傳訊，於活動進行時與使用者互動和觸達。</span><span class="sxs-lookup"><span data-stu-id="e12c4-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="e12c4-157">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="e12c4-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="e12c4-158">以下各節將設定您的用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="e12c4-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="e12c4-159">啟用您的應用程式接收 WNS 推播通知</span><span class="sxs-lookup"><span data-stu-id="e12c4-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="e12c4-160">在 `Package.appxmanifest` 檔案中，於 [應用程式] 索引標籤的 [通知] 下方，將 [支援快顯通知:] 設為 [是]</span><span class="sxs-lookup"><span data-stu-id="e12c4-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="e12c4-161">初始化 REACH SDK</span><span class="sxs-lookup"><span data-stu-id="e12c4-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="e12c4-162">在 `App.xaml.cs` 中，於代理程式初始化之後，立即在 **InitEngagement** 函式中呼叫 **EngagementReach.Instance.Init(e);**：</span><span class="sxs-lookup"><span data-stu-id="e12c4-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="e12c4-163">您現在可以開始傳送快顯通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-163">You're ready to send a toast.</span></span> <span data-ttu-id="e12c4-164">接下來我們要驗證您已正確完成這項基本整合。</span><span class="sxs-lookup"><span data-stu-id="e12c4-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="e12c4-165">授與 Mobile Engagement 存取權以傳送通知</span><span class="sxs-lookup"><span data-stu-id="e12c4-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="e12c4-166">在網頁瀏覽器中開啟 [Windows 市集開發人員中心] ，視需要登入和建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="e12c4-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="e12c4-167">按一下右上角的 [儀表板]，然後按一下左面板功能表中的 [建立新的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e12c4-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="e12c4-168">建立您的應用程式並保留其名稱。</span><span class="sxs-lookup"><span data-stu-id="e12c4-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="e12c4-169">建立應用程式之後，從左側功能表瀏覽至 [服務] -> [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="e12c4-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="e12c4-170">在 [推播通知] 區段中按一下 [Live 服務網站]  連結。</span><span class="sxs-lookup"><span data-stu-id="e12c4-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="e12c4-171">您會瀏覽至推送認證區段。</span><span class="sxs-lookup"><span data-stu-id="e12c4-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="e12c4-172">請確定您位於 [應用程式設定] 區段中，然後複製您的 [套件 SID] 和 [用戶端密碼]</span><span class="sxs-lookup"><span data-stu-id="e12c4-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="e12c4-173">瀏覽到 Mobile Engagement 入口網站的 [設定]，然後按一下左側的 [原生推送] 區段。</span><span class="sxs-lookup"><span data-stu-id="e12c4-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="e12c4-174">然後，按一下 [編輯] 按鈕來輸入您的 [套件安全性識別碼 (SID)] 和 [秘密金鑰]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e12c4-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="e12c4-175">最後確定您的 Visual Studio 應用程式與在應用程式市集中建立的此應用程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="e12c4-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="e12c4-176">按一下 Visual Studio 中的 [建立應用程式與市集關聯]  。</span><span class="sxs-lookup"><span data-stu-id="e12c4-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="e12c4-177"><a id="send"></a>傳送通知至應用程式</span><span class="sxs-lookup"><span data-stu-id="e12c4-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="e12c4-178">如果應用程式正在執行，您會看到應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="e12c4-179">如果應用程式已關閉，則會看到快顯通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="e12c4-180">如果您看見的是應用程式內通知而不是快顯通知，而且您正在 Visual Studio 中的偵錯模式下執行應用程式，則可嘗試執行工具列中的 [週期事件] -> [暫止]，以確保應用程式會暫止。</span><span class="sxs-lookup"><span data-stu-id="e12c4-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="e12c4-181">如果您在 Visual Studio 中偵錯應用程式時按了 [首頁] 按鈕，則應用程式不一定會暫止，而且您會看見應用程式內通知，它不會顯示為快顯通知。</span><span class="sxs-lookup"><span data-stu-id="e12c4-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="e12c4-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="e12c4-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="e12c4-183">[Windows 市集開發人員中心]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="e12c4-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
