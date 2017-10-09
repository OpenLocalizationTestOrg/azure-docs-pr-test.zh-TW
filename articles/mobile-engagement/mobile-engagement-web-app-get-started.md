---
title: "Azure Mobile Engagement aaaGet 啟動 Web 應用程式 |Microsoft 文件"
description: "深入了解如何 toouse Azure Mobile Engagement 的 Web 應用程式的分析和推播通知。"
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>開始使用適用於 Web Apps 的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您 Web 應用程式的使用量。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

本教學課程必須 hello 下列需求：

* Visual Studio 2015 或您選擇的其他任何編輯器
* [Web SDK](http://aka.ms/P7b453)

此 Web SDK 處於預覽狀態只在 hello 時刻支援分析和尚不支援傳送瀏覽器或應用程式中的推播通知。 

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started)。
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>為 Web 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 「 基本整合，」 即 hello 所需的最小集合 toocollect 資料。

雖然您可以依照 hello 步驟也建立 Visual Studio 外部的任何 web 應用程式，我們會建立基本 web 應用程式與 Visual Studio toodemonstrate hello 整合。 

### <a name="create-a-new-web-app"></a>建立新的 Web 應用程式
hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。 

1. 啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。
2. 在 hello 快顯視窗中，選取  **Web** -> **ASP.Net Web 應用程式**。 填寫 hello 應用程式**名稱**，**位置**和**方案名稱**，然後按一下**確定**。
3. 在 hello**選取範本**快顯視窗，選取**空**下**ASP.Net 4.5 範本**按一下**確定**。 

您現在已建立新的空白 Web 應用程式專案到其中，我們將會整合 hello Azure Mobile Engagement Web SDK。

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 建立新資料夾，稱為**javascript**方案中新增 hello Web SDK JS 檔案**azure engagement.js**到其中。 
2. 加入新的檔案稱為**main.js**以下列程式碼的 hello 這個 javascript 資料夾中。 請確定 tooupdate hello 連接字串。 這`azureEngagement`物件將會使用的 tooaccess Web SDK 方法。 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio 和 js 檔案][1]

## <a name="enable-real-time-monitoring"></a>啟用即時監視
在訂單 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個活動 toohello Mobile Engagement 後端。 Hello 內容 web 應用程式中的活動是網頁。 

1. 建立新的頁面稱為**home.html**中您的方案和做為 hello 啟動 web 應用程式頁面上的設定。 
2. 包含 hello 兩個 javascripts 我們稍早在此頁面中加入加 hello 下列 hello body 標記內。 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. 更新 hello 主體標記 toocall EngagementAgent 的`startActivity`方法
   
        <body onload="engagement.agent.startActivity('Home')">
4. 您的 **home.html** 看起來會像下面這樣
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>將應用程式與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>擴充分析
以下是所有 hello 方法目前提供的 Web SDK 可讓您進行分析：

1. 活動/網頁︰
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. 事件
   
        engagement.agent.sendEvent(name, extras);
3. 錯誤數
   
        engagement.agent.sendError(name, extras);
4. 作業
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

