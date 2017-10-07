---
title: "開始使用 Windows 通用應用程式 Azure Mobile Engagement aaaGet"
description: "深入了解如何 toouse Azure Mobile Engagement 與為 Windows 通用應用程式的分析和推播通知。"
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
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="d8808-103">開始使用適用於 Windows 通用 App 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8808-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d8808-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者的 Windows 通用應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8808-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="d8808-105">本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。</span><span class="sxs-lookup"><span data-stu-id="d8808-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="d8808-106">您建立一個空白的 Windows 通用應用程式，以使用 Windows 通知服務 (WNS) 來收集基本的應用程式使用資料及接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="d8808-107">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="d8808-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="d8808-108">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="d8808-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8808-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d8808-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="d8808-110">設定 Windows 通用應用程式的 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8808-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d8808-111"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="d8808-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d8808-112">此教學課程提供 < 基本整合，"hello 最小設定必要的 toocollect 資料及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="d8808-113">hello 完整的整合文件可以在 hello [Mobile Engagement Windows 通用 SDK 整合](mobile-engagement-windows-store-sdk-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d8808-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="d8808-114">您可以建立基本應用程式與 Visual Studio toodemonstrate hello 整合。</span><span class="sxs-lookup"><span data-stu-id="d8808-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="d8808-115">建立一個 Windows 通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="d8808-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="d8808-116">hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。</span><span class="sxs-lookup"><span data-stu-id="d8808-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="d8808-117">啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。</span><span class="sxs-lookup"><span data-stu-id="d8808-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="d8808-118">在 hello 快顯視窗中，選取  **Windows** -> **通用** -> **空白應用程式 (通用 Windows)**。</span><span class="sxs-lookup"><span data-stu-id="d8808-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="d8808-119">Hello 應用程式中填滿**名稱**和**方案名稱**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="d8808-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="d8808-120">您現在已建立在其中您接下來整合 hello Azure Mobile Engagement SDK 的 Windows 通用應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="d8808-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="d8808-121">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="d8808-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="d8808-122">安裝 hello [MicrosoftAzure.MobileEngagement]專案中的 Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="d8808-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="d8808-123">如果您將目標設定 Windows 和 Windows Phone 平台，您需要 toodo 這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="d8808-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="d8808-124">適用於 Windows 8.x 和 Windows Phone 8.1，hello 相同 Nuget 封裝上的芳鄰 hello 正確平台專屬的二進位檔案中的每個專案。</span><span class="sxs-lookup"><span data-stu-id="d8808-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="d8808-125">開啟**Package.appxmanifest**並確定已那里加入該 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="d8808-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="d8808-126">現在將 hello 您之前複製您的 Mobile Engagement 應用程式的連接字串複製並貼入 hello `Resources\EngagementConfiguration.xml` hello 之間的檔案，`<connectionString>`和`</connectionString>`標記：</span><span class="sxs-lookup"><span data-stu-id="d8808-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="d8808-127">如果您的應用程式以 Windows 和 Windows Phone 兩個平台為目標，那麼您仍應該建立兩個 Mobile Engagment 應用程式，讓每個支援的平台各使用一個。</span><span class="sxs-lookup"><span data-stu-id="d8808-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="d8808-128">有兩個應用程式，可確保您可以建立正確的分割 hello 對象，並將每個平台的適當目標的通知傳送。</span><span class="sxs-lookup"><span data-stu-id="d8808-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d8808-129">NuGet 不會自動複製 hello SDK 資源，以在 Windows 10 UWP 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d8808-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="d8808-130">您將 toodo 它手動遵循 (readme.txt) hello Nuget 封裝安裝時，顯示 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d8808-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="d8808-131">在 hello`App.xaml.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="d8808-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="d8808-132">a.</span><span class="sxs-lookup"><span data-stu-id="d8808-132">a.</span></span> <span data-ttu-id="d8808-133">新增 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="d8808-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="d8808-134">b.</span><span class="sxs-lookup"><span data-stu-id="d8808-134">b.</span></span> <span data-ttu-id="d8808-135">加入的方法，初始化 hello Engagement:</span><span class="sxs-lookup"><span data-stu-id="d8808-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="d8808-136">c.</span><span class="sxs-lookup"><span data-stu-id="d8808-136">c.</span></span> <span data-ttu-id="d8808-137">初始化 hello SDK 中 hello **OnLaunched**方法：</span><span class="sxs-lookup"><span data-stu-id="d8808-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="d8808-138">c.</span><span class="sxs-lookup"><span data-stu-id="d8808-138">c.</span></span> <span data-ttu-id="d8808-139">插入 hello hello 下列**OnActivated**方法並加入 hello 方法，如果尚不存在：</span><span class="sxs-lookup"><span data-stu-id="d8808-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="d8808-140"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="d8808-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="d8808-141">toostart 傳送資料和 hello 使用者都已使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="d8808-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d8808-142">在 hello **MainPage.xaml.cs**，加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="d8808-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="d8808-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="d8808-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="d8808-144">變更 hello 基底類別**MainPage**從**頁面**太**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="d8808-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="d8808-145">在 hello`MainPage.xaml`檔案：</span><span class="sxs-lookup"><span data-stu-id="d8808-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="d8808-146">a.</span><span class="sxs-lookup"><span data-stu-id="d8808-146">a.</span></span> <span data-ttu-id="d8808-147">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="d8808-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="d8808-148">b.</span><span class="sxs-lookup"><span data-stu-id="d8808-148">b.</span></span> <span data-ttu-id="d8808-149">取代 hello**頁面**hello XML 標記名稱與**engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="d8808-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8808-150">如果您的頁面會覆寫 hello`OnNavigatedTo`方法，是確定 toocall `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="d8808-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="d8808-151">否則，hello 活動不會報告`EngagementPage`呼叫`StartActivity`內其`OnNavigatedTo`方法)。</span><span class="sxs-lookup"><span data-stu-id="d8808-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="d8808-152">這點特別重要，在 Windows Phone 專案顯示 hello 預設範本已`OnNavigatedTo`方法。</span><span class="sxs-lookup"><span data-stu-id="d8808-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="d8808-153">**Windows 10 通用應用程式**，使用 hello 方法建議 hello"建議使用的方法： 多載網頁類別 」 一節[進階報告功能與 hello Windows 通用應用程式 Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md)而不是 hello 其中一個上面所述。</span><span class="sxs-lookup"><span data-stu-id="d8808-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="d8808-154"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="d8808-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d8808-155"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="d8808-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d8808-156">Mobile Engagement 可讓您 toointeract，並連線到您的推播通知及應用程式內訊息的活動 hello 內容中的使用者。</span><span class="sxs-lookup"><span data-stu-id="d8808-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="d8808-157">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d8808-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d8808-158">hello 下列各節將設定您的應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="d8808-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="d8808-159">啟用您的應用程式 tooreceive WNS 推播通知</span><span class="sxs-lookup"><span data-stu-id="d8808-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="d8808-160">在 hello`Package.appxmanifest`檔案，請在 hello**應用程式**索引標籤，在**通知**，將**支援快顯通知：**太**是**</span><span class="sxs-lookup"><span data-stu-id="d8808-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="d8808-161">初始化 hello REACH SDK</span><span class="sxs-lookup"><span data-stu-id="d8808-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="d8808-162">在`App.xaml.cs`，呼叫**EngagementReach.Instance.Init(e);**在 hello **InitEngagement** hello 代理程式初始化之後函式：</span><span class="sxs-lookup"><span data-stu-id="d8808-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="d8808-163">您已準備好 toosend 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-163">You're ready toosend a toast.</span></span> <span data-ttu-id="d8808-164">接下來我們要驗證您已正確完成這項基本整合。</span><span class="sxs-lookup"><span data-stu-id="d8808-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="d8808-165">授與存取 tooMobile Engagement toosend 通知</span><span class="sxs-lookup"><span data-stu-id="d8808-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="d8808-166">在網頁瀏覽器中開啟 [Windows 市集開發人員中心] ，視需要登入和建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8808-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="d8808-167">按一下**儀表板**在 hello 右上角，然後按一下**建立新的應用程式**hello 左的面板功能表。</span><span class="sxs-lookup"><span data-stu-id="d8808-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="d8808-168">建立您的應用程式並保留其名稱。</span><span class="sxs-lookup"><span data-stu-id="d8808-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="d8808-169">一旦建立 hello 應用程式之後，瀏覽過**服務]-> [推播通知**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="d8808-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="d8808-170">在 [hello 推播通知] 區段中，按一下 hello **Live 服務 」 站台**連結。</span><span class="sxs-lookup"><span data-stu-id="d8808-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="d8808-171">您瀏覽 toohello 推播認證 > 一節。</span><span class="sxs-lookup"><span data-stu-id="d8808-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="d8808-172">請確定您是在 hello**應用程式設定**區段，然後複製您**封裝 SID**和**用戶端密碼**</span><span class="sxs-lookup"><span data-stu-id="d8808-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="d8808-173">瀏覽 toohello**設定**Mobile Engagement 入口網站，按一下 hello**原生推送**hello 左側的 > 一節。</span><span class="sxs-lookup"><span data-stu-id="d8808-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="d8808-174">然後，按一下 hello**編輯**按鈕 tooenter 您**封裝安全性識別碼 (SID)**和您**秘密金鑰**所示：</span><span class="sxs-lookup"><span data-stu-id="d8808-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="d8808-175">最後請確定您已經與 hello 應用程式存放區中此建立應用程式關聯您的 Visual Studio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8808-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="d8808-176">按一下 Visual Studio 中的 [建立應用程式與市集關聯]  。</span><span class="sxs-lookup"><span data-stu-id="d8808-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="d8808-177"><a id="send"></a>傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8808-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="d8808-178">如果 hello 應用程式正在執行，您會看到應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="d8808-179">否則如果 hello 應用程式已關閉，您會看到快顯通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="d8808-180">如果您看到的應用程式內通知，但不是快顯通知，而且您在 Visual Studio 中偵錯模式執行 hello 應用程式，然後再試一次**生命週期事件]-> [暫止**hello 工具列 tooensure 該 hello 應用程式會暫停。</span><span class="sxs-lookup"><span data-stu-id="d8808-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="d8808-181">如果您在偵錯 Visual Studio 中的 hello 應用程式時按一下 hello 首頁 按鈕，然後它不會永遠被暫停，而您為應用程式中看到 hello 通知，它不會顯示為快顯通知。</span><span class="sxs-lookup"><span data-stu-id="d8808-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows 市集開發人員中心]: https://dev.windows.com
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
