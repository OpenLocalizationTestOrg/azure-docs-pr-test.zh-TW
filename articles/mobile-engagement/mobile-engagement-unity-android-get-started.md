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
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>開始使用適用於 Unity Android 部署的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者 Unity 應用程式的部署 tooan Android 裝置時。
這個教學課程使用 hello 傳統 Unity 回復球教學課程為 hello 起始點。 您應該遵循這個 hello 步驟[教學課程](mobile-engagement-unity-roll-a-ball.md)hello Mobile Engagement 整合我們展示下列 hello 教學課程中繼續執行。 

本教學課程必須 hello 下列需求：

* [Unity 編輯器](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started)。
> 
> 

## <a id="setup-azme"></a>為您的 Android 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
### <a name="import-hello-unity-package"></a>匯入 hello Unity 套件
1. 下載 hello [Mobile Engagement Unity 套件](https://aka.ms/azmeunitysdk)並將它儲存 tooyour 本機電腦。 
2. 跳過**資產]-> [匯入封裝]-> [自訂封裝**和下載中的步驟上方 hello 選取 hello 封裝。 
   
    ![][70] 
3. 確定已選取所有檔案，然後按一下 [匯入]  按鈕。 
   
    ![][71] 
4. 一旦匯入成功時，您會看到匯入的 hello SDK 檔案專案中。  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>更新 hello EngagementConfiguration
1. 開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **ANDROID\_連接\_字串**hello 您取得的連接字串先前從 hello Azure 入口網站。  
   
    ![][73]
2. 儲存 hello 檔案 
3. 執行 [檔案]-> [Engagement]-> [產生 Android 資訊清單]。 這是加入 hello Mobile Engagement SDK 的 hello 外掛程式，並按一下它會自動更新您的專案設定。 
   
    ![][74]

> [!IMPORTANT]
> 請確定 tooexecute 這每次您更新 hello **EngagementConfiguration**檔案否則您的變更將不會反映在 hello 應用程式。 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>設定基本追蹤的 hello 應用程式
1. 開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。 
2. 新增 hello 下列 using 陳述式：
   
        using Microsoft.Azure.Engagement.Unity;
3. 新增下列 toohello hello`Start()`方法
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>部署和執行 hello 應用程式
請確定您具有在電腦上安裝，然後再嘗試 toodeploy 這個 Unity 應用程式 tooyour 裝置的 Android SDK。 

1. Android 裝置 tooyour 機器連線。 
2. 開啟 [檔案] -> [組建設定] 
   
    ![][40]
3. 選取 Android，然後按一下切換平台
   
    ![][51]
   
    ![][52]
4. 按一下 [播放器設定]  並提供有效的 [套件組合識別碼]。 
   
    ![][53]
5. 最後按一下 [建置並執行] 
   
    ![][54]
6. 您可能會要求您 tooprovide 資料夾名稱 toostore hello Android 套件。 
7. 如果一切正常運作，hello 封裝將會部署的 tooyour 連接裝置，且您應該會看到 Unity 遊戲手機上 ！ 

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>更新 hello EngagementConfiguration
1. 開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **ANDROID\_GOOGLE\_數目**以 hello **Google 專案數字**先前從 hello Google 雲端開發人員入口網站取得。 這是一個字串值，所以請確定 tooenclose 雙引號括住它。 
   
    ![][75]
2. 儲存 hello 檔案。 
3. 執行 [檔案]-> [Engagement]-> [產生 Android 資訊清單]。 這是加入 hello Mobile Engagement SDK 的 hello 外掛程式，並按一下它會自動更新您的專案設定。 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>設定 hello tooreceive 通知，應用程式
1. 開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。 
2. 新增下列 toohello hello`Start()`方法
   
        EngagementReachAgent.Initialize();
3. 既然 hello 應用程式更新時，部署和執行 hello 應用程式在裝置上每 hello 下面提供的指示。 

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
