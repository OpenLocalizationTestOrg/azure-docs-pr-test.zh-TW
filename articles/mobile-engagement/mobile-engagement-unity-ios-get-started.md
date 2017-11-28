---
title: "Unity iOS 部署 aaaGet Started with Azure Mobile Engagement"
description: "深入了解如何針對 Unity 應用程式部署 tooiOS 裝置 toouse 與分析及推播通知的 Azure Mobile Engagement。"
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="5b770-103">開始使用適用於 Unity iOS 部署的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5b770-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="5b770-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者 Unity 應用程式的部署 tooan iOS 裝置時。</span><span class="sxs-lookup"><span data-stu-id="5b770-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="5b770-105">這個教學課程使用 hello 傳統 Unity 回復球教學課程為 hello 起始點。</span><span class="sxs-lookup"><span data-stu-id="5b770-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="5b770-106">您應該遵循這個 hello 步驟[教學課程](mobile-engagement-unity-roll-a-ball.md)hello Mobile Engagement 整合我們展示下列 hello 教學課程中繼續執行。</span><span class="sxs-lookup"><span data-stu-id="5b770-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="5b770-107">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="5b770-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="5b770-108">Unity 編輯器</span><span class="sxs-lookup"><span data-stu-id="5b770-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="5b770-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="5b770-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="5b770-110">XCode 編輯器</span><span class="sxs-lookup"><span data-stu-id="5b770-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="5b770-111">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b770-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5b770-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b770-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5b770-113">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="5b770-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="5b770-114"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5b770-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="5b770-115"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="5b770-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="5b770-116">匯入 hello Unity 套件</span><span class="sxs-lookup"><span data-stu-id="5b770-116">Import hello Unity package</span></span>
1. <span data-ttu-id="5b770-117">下載 hello [Mobile Engagement Unity 套件](https://aka.ms/azmeunitysdk)並將它儲存 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="5b770-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="5b770-118">跳過**資產]-> [匯入封裝]-> [自訂封裝**和下載中的步驟上方 hello 選取 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="5b770-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="5b770-119">確定已選取所有檔案，然後按一下 [匯入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b770-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="5b770-120">一旦匯入成功時，您會看到匯入的 hello SDK 檔案專案中。</span><span class="sxs-lookup"><span data-stu-id="5b770-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="5b770-121">更新 hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="5b770-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="5b770-122">開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **IOS\_連接\_字串**hello 您稍早取得的連接字串從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5b770-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="5b770-123">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5b770-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="5b770-124">設定基本追蹤的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5b770-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="5b770-125">開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。</span><span class="sxs-lookup"><span data-stu-id="5b770-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="5b770-126">新增 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="5b770-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="5b770-127">新增下列 toohello hello`Start()`方法</span><span class="sxs-lookup"><span data-stu-id="5b770-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="5b770-128">部署和執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5b770-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="5b770-129">連線的 iOS 裝置 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="5b770-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="5b770-130">開啟 [檔案] -> [組建設定]</span><span class="sxs-lookup"><span data-stu-id="5b770-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="5b770-131">選取 iOS，然後按一下切換平台</span><span class="sxs-lookup"><span data-stu-id="5b770-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="5b770-132">按一下 [播放器設定]  並提供有效的 [套件組合識別碼]。</span><span class="sxs-lookup"><span data-stu-id="5b770-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="5b770-133">最後按一下 [建置並執行] </span><span class="sxs-lookup"><span data-stu-id="5b770-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="5b770-134">您可能會要求您 tooprovide 資料夾名稱 toostore hello iOS 套件。</span><span class="sxs-lookup"><span data-stu-id="5b770-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="5b770-135">一切正常，然後 hello 專案會編譯和您應該開啟它在 XCode 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b770-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="5b770-136">請確定該 hello**配套識別碼**hello 專案中正確無誤。</span><span class="sxs-lookup"><span data-stu-id="5b770-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="5b770-137">現在，因此 hello 封裝部署的 tooyour 連接的裝置，且您應該查看手機上的 Unity 遊戲，請在 XCode 中執行 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="5b770-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="5b770-138"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="5b770-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="5b770-139"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="5b770-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="5b770-140">Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。</span><span class="sxs-lookup"><span data-stu-id="5b770-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="5b770-141">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5b770-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="5b770-142">Toodo 任何額外的設定中沒有您的應用程式 tooreceive 通知，它已經為它的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5b770-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
