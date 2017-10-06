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
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>開始使用適用於 Unity iOS 部署的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者 Unity 應用程式的部署 tooan iOS 裝置時。
這個教學課程使用 hello 傳統 Unity 回復球教學課程為 hello 起始點。 您應該遵循這個 hello 步驟[教學課程](mobile-engagement-unity-roll-a-ball.md)hello Mobile Engagement 整合我們展示下列 hello 教學課程中繼續執行。 

本教學課程必須 hello 下列需求：

* [Unity 編輯器](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* XCode 編輯器

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started)。
> 
> 

## <a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement
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
1. 開啟 hello **EngagementConfiguration**指令碼檔案，從 hello SDK 資料夾，然後更新 hello **IOS\_連接\_字串**hello 您稍早取得的連接字串從 hello Azure 入口網站。  
   
    ![][73]
2. 儲存 hello 檔案。 

### <a name="configure-hello-app-for-basic-tracking"></a>設定基本追蹤的 hello 應用程式
1. 開啟 hello **PlayerController**指令碼附加 toohello Player 物件以供編輯。 
2. 新增 hello 下列 using 陳述式：
   
        using Microsoft.Azure.Engagement.Unity;
3. 新增下列 toohello hello`Start()`方法
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>部署和執行 hello 應用程式
1. 連線的 iOS 裝置 tooyour 機器。 
2. 開啟 [檔案] -> [組建設定] 
   
    ![][40]
3. 選取 iOS，然後按一下切換平台
   
    ![][41]
   
    ![][42]
4. 按一下 [播放器設定]  並提供有效的 [套件組合識別碼]。 
   
    ![][53]
5. 最後按一下 [建置並執行] 
   
    ![][54]
6. 您可能會要求您 tooprovide 資料夾名稱 toostore hello iOS 套件。 
   
    ![][43]
7. 一切正常，然後 hello 專案會編譯和您應該開啟它在 XCode 應用程式。 
8. 請確定該 hello**配套識別碼**hello 專案中正確無誤。  
   
    ![][75]
9. 現在，因此 hello 封裝部署的 tooyour 連接的裝置，且您應該查看手機上的 Unity 遊戲，請在 XCode 中執行 hello 應用程式 ！ 

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
Toodo 任何額外的設定中沒有您的應用程式 tooreceive 通知，它已經為它的安裝程式。

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
