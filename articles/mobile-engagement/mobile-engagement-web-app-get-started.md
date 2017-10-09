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
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="fca5f-103">開始使用適用於 Web Apps 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fca5f-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="fca5f-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您 Web 應用程式的使用量。</span><span class="sxs-lookup"><span data-stu-id="fca5f-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="fca5f-105">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="fca5f-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="fca5f-106">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="fca5f-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="fca5f-107">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="fca5f-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="fca5f-108">Visual Studio 2015 或您選擇的其他任何編輯器</span><span class="sxs-lookup"><span data-stu-id="fca5f-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="fca5f-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="fca5f-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="fca5f-110">此 Web SDK 處於預覽狀態只在 hello 時刻支援分析和尚不支援傳送瀏覽器或應用程式中的推播通知。</span><span class="sxs-lookup"><span data-stu-id="fca5f-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="fca5f-111">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fca5f-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="fca5f-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fca5f-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fca5f-113">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started)。</span><span class="sxs-lookup"><span data-stu-id="fca5f-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="fca5f-114">為 Web 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fca5f-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="fca5f-115"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="fca5f-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="fca5f-116">此教學課程提供 「 基本整合，」 即 hello 所需的最小集合 toocollect 資料。</span><span class="sxs-lookup"><span data-stu-id="fca5f-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="fca5f-117">雖然您可以依照 hello 步驟也建立 Visual Studio 外部的任何 web 應用程式，我們會建立基本 web 應用程式與 Visual Studio toodemonstrate hello 整合。</span><span class="sxs-lookup"><span data-stu-id="fca5f-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="fca5f-118">建立新的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fca5f-118">Create a new Web App</span></span>
<span data-ttu-id="fca5f-119">hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。</span><span class="sxs-lookup"><span data-stu-id="fca5f-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="fca5f-120">啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。</span><span class="sxs-lookup"><span data-stu-id="fca5f-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="fca5f-121">在 hello 快顯視窗中，選取  **Web** -> **ASP.Net Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fca5f-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="fca5f-122">填寫 hello 應用程式**名稱**，**位置**和**方案名稱**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="fca5f-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="fca5f-123">在 hello**選取範本**快顯視窗，選取**空**下**ASP.Net 4.5 範本**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="fca5f-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="fca5f-124">您現在已建立新的空白 Web 應用程式專案到其中，我們將會整合 hello Azure Mobile Engagement Web SDK。</span><span class="sxs-lookup"><span data-stu-id="fca5f-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="fca5f-125">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="fca5f-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="fca5f-126">建立新資料夾，稱為**javascript**方案中新增 hello Web SDK JS 檔案**azure engagement.js**到其中。</span><span class="sxs-lookup"><span data-stu-id="fca5f-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="fca5f-127">加入新的檔案稱為**main.js**以下列程式碼的 hello 這個 javascript 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="fca5f-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="fca5f-128">請確定 tooupdate hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="fca5f-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="fca5f-129">這`azureEngagement`物件將會使用的 tooaccess Web SDK 方法。</span><span class="sxs-lookup"><span data-stu-id="fca5f-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio 和 js 檔案][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="fca5f-131">啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="fca5f-131">Enable real-time monitoring</span></span>
<span data-ttu-id="fca5f-132">在訂單 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個活動 toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="fca5f-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="fca5f-133">Hello 內容 web 應用程式中的活動是網頁。</span><span class="sxs-lookup"><span data-stu-id="fca5f-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="fca5f-134">建立新的頁面稱為**home.html**中您的方案和做為 hello 啟動 web 應用程式頁面上的設定。</span><span class="sxs-lookup"><span data-stu-id="fca5f-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="fca5f-135">包含 hello 兩個 javascripts 我們稍早在此頁面中加入加 hello 下列 hello body 標記內。</span><span class="sxs-lookup"><span data-stu-id="fca5f-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="fca5f-136">更新 hello 主體標記 toocall EngagementAgent 的`startActivity`方法</span><span class="sxs-lookup"><span data-stu-id="fca5f-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="fca5f-137">您的 **home.html** 看起來會像下面這樣</span><span class="sxs-lookup"><span data-stu-id="fca5f-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="fca5f-138">將應用程式與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="fca5f-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="fca5f-139">擴充分析</span><span class="sxs-lookup"><span data-stu-id="fca5f-139">Extend analytics</span></span>
<span data-ttu-id="fca5f-140">以下是所有 hello 方法目前提供的 Web SDK 可讓您進行分析：</span><span class="sxs-lookup"><span data-stu-id="fca5f-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="fca5f-141">活動/網頁︰</span><span class="sxs-lookup"><span data-stu-id="fca5f-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="fca5f-142">事件</span><span class="sxs-lookup"><span data-stu-id="fca5f-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="fca5f-143">錯誤數</span><span class="sxs-lookup"><span data-stu-id="fca5f-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="fca5f-144">作業</span><span class="sxs-lookup"><span data-stu-id="fca5f-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

