---
title: "Unity Android 部署 aaaGet Started with Azure Mobile Engagement"
description: "深入了解如何針對 Unity 應用程式部署 tooiOS 裝置 toouse 與分析及推播通知的 Azure Mobile Engagement。"
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="d4d0d-103">開始使用適用於 Unity Android 部署的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d4d0d-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d4d0d-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者 Unity 應用程式的部署 tooan Android 裝置時。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="d4d0d-105">這個教學課程使用 hello 傳統 Unity 回復球教學課程為 hello 起始點。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="d4d0d-106">您應該遵循這個 hello 步驟[教學課程](mobile-engagement-unity-roll-a-ball.md)hello Mobile Engagement 整合我們展示下列 hello 教學課程中繼續執行。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="d4d0d-107">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="d4d0d-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="d4d0d-108">Unity 編輯器</span><span class="sxs-lookup"><span data-stu-id="d4d0d-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="d4d0d-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="d4d0d-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="d4d0d-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="d4d0d-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="d4d0d-111">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d4d0d-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d4d0d-113">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="d4d0d-114"><a id="setup-azme"></a>為您的 Android 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d4d0d-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d4d0d-115"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="d4d0d-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="d4d0d-116">匯入 hello Unity 套件</span><span class="sxs-lookup"><span data-stu-id="d4d0d-116">Import hello Unity package</span></span>
1. <span data-ttu-id="d4d0d-117">下載 hello [Mobile Engagement Unity 套件](https://aka.ms/azmeunitysdk)並將它儲存 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="d4d0d-118">跳過**資產]-> [匯入封裝]-> [自訂封裝**和下載中的步驟上方 hello 選取 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="d4d0d-119">確定已選取所有檔案，然後按一下 [匯入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="d4d0d-120">一旦匯入成功時，您會看到匯入的 hello SDK 檔案專案中。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="d4d0d-121">更新 hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4d0d-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="d4d0d-122">開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **ANDROID\_連接\_字串**hello 您取得的連接字串先前從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="d4d0d-123">儲存 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="d4d0d-123">Save hello file</span></span> 
3. <span data-ttu-id="d4d0d-124">執行 [檔案]-> [Engagement]-> [產生 Android 資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="d4d0d-125">這是加入 hello Mobile Engagement SDK 的 hello 外掛程式，並按一下它會自動更新您的專案設定。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="d4d0d-126">請確定 tooexecute 這每次您更新 hello **EngagementConfiguration**檔案否則您的變更將不會反映在 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="d4d0d-127">設定基本追蹤的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d4d0d-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="d4d0d-128">開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="d4d0d-129">新增 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="d4d0d-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="d4d0d-130">新增下列 toohello hello`Start()`方法</span><span class="sxs-lookup"><span data-stu-id="d4d0d-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="d4d0d-131">部署和執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d4d0d-131">Deploy and run hello app</span></span>
<span data-ttu-id="d4d0d-132">請確定您具有在電腦上安裝，然後再嘗試 toodeploy 這個 Unity 應用程式 tooyour 裝置的 Android SDK。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="d4d0d-133">Android 裝置 tooyour 機器連線。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="d4d0d-134">開啟 [檔案] -> [組建設定]</span><span class="sxs-lookup"><span data-stu-id="d4d0d-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="d4d0d-135">選取 Android，然後按一下切換平台</span><span class="sxs-lookup"><span data-stu-id="d4d0d-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="d4d0d-136">按一下 [播放器設定]  並提供有效的 [套件組合識別碼]。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="d4d0d-137">最後按一下 [建置並執行] </span><span class="sxs-lookup"><span data-stu-id="d4d0d-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="d4d0d-138">您可能會要求您 tooprovide 資料夾名稱 toostore hello Android 套件。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="d4d0d-139">如果一切正常運作，hello 封裝將會部署的 tooyour 連接裝置，且您應該會看到 Unity 遊戲手機上 ！</span><span class="sxs-lookup"><span data-stu-id="d4d0d-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="d4d0d-140"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="d4d0d-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d4d0d-141"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="d4d0d-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="d4d0d-142">更新 hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4d0d-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="d4d0d-143">開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **ANDROID\_GOOGLE\_數目**以 hello **Google 專案數字**先前從 hello Google 雲端開發人員入口網站取得。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="d4d0d-144">這是一個字串值，所以請確定 tooenclose 雙引號括住它。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="d4d0d-145">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-145">Save hello file.</span></span> 
3. <span data-ttu-id="d4d0d-146">執行 [檔案]-> [Engagement]-> [產生 Android 資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="d4d0d-147">這是加入 hello Mobile Engagement SDK 的 hello 外掛程式，並按一下它會自動更新您的專案設定。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="d4d0d-148">設定 hello tooreceive 通知，應用程式</span><span class="sxs-lookup"><span data-stu-id="d4d0d-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="d4d0d-149">開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="d4d0d-150">新增下列 toohello hello`Start()`方法</span><span class="sxs-lookup"><span data-stu-id="d4d0d-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="d4d0d-151">既然 hello 應用程式更新時，部署和執行 hello 應用程式在裝置上每 hello 下面提供的指示。</span><span class="sxs-lookup"><span data-stu-id="d4d0d-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
