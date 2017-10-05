---
title: "Azure Mobile Engagement Web SDK 整合 | Microsoft Docs"
description: "Azure Mobile Engagement Web SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="83805-103">在 Web 應用程式中整合 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="83805-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83805-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="83805-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="83805-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="83805-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="83805-106">iOS</span><span class="sxs-lookup"><span data-stu-id="83805-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="83805-107">Android</span><span class="sxs-lookup"><span data-stu-id="83805-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="83805-108">本文中的程序說明在 Web 應用程式中，啟用 Azure Mobile Engagement 中分析與監視功能的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="83805-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="83805-109">遵循下列步驟來啟用進行下列動作所需的記錄檔報告：計算關於使用者、工作階段、活動、當機和技術的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="83805-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="83805-110">對於相依於應用程式的統計資料 (例如事件、錯誤及工作)，您必須使用 Azure Mobile Engagement API 手動啟用記錄檔報告。</span><span class="sxs-lookup"><span data-stu-id="83805-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="83805-111">如需詳細資訊，請了解 [如何在 Web 應用程式中使用進階的 Mobile Engagement 標記 API](mobile-engagement-web-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="83805-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="83805-112">簡介</span><span class="sxs-lookup"><span data-stu-id="83805-112">Introduction</span></span>
<span data-ttu-id="83805-113">[下載 Azure Mobile Engagement Web SDK](http://aka.ms/P7b453)。</span><span class="sxs-lookup"><span data-stu-id="83805-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="83805-114">Mobile Engagement Web SDK 是以單一 JavaScript 檔案 (azure-engagement.js) 隨附，您必須將它包含在網站或 Web 應用程式的每個頁面中。</span><span class="sxs-lookup"><span data-stu-id="83805-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83805-115">執行此指令碼之前，必須先執行您撰寫來為應用程式設定 Mobile Engagement 的指令碼或程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="83805-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="83805-116">瀏覽器相容性</span><span class="sxs-lookup"><span data-stu-id="83805-116">Browser compatibility</span></span>
<span data-ttu-id="83805-117">Mobile Engagement Web SDK 使用原生 JSON 編碼和解碼，以及跨網域 AJAX 要求 (仰賴 W3C CORS 規格)。</span><span class="sxs-lookup"><span data-stu-id="83805-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="83805-118">它與下列瀏覽器相容：</span><span class="sxs-lookup"><span data-stu-id="83805-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="83805-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="83805-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="83805-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="83805-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="83805-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="83805-121">Firefox 3.5+</span></span>
* <span data-ttu-id="83805-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="83805-122">Chrome 4+</span></span>
* <span data-ttu-id="83805-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="83805-123">Safari 6+</span></span>
* <span data-ttu-id="83805-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="83805-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="83805-125">設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="83805-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="83805-126">撰寫能建立全域 `azureEngagement` JavaScript 物件的指令碼，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="83805-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="83805-127">因為您的網站可能包含多個頁面，此範例假設這個指令碼包含於每個頁面中。</span><span class="sxs-lookup"><span data-stu-id="83805-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="83805-128">在此範例中，JavaScript 物件的名稱為 `azure-engagement-conf.js`。</span><span class="sxs-lookup"><span data-stu-id="83805-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="83805-129">適用於您應用程式的 `connectionString` 值會顯示於 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="83805-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="83805-130">`appVersionName` 和 `appVersionCode` 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="83805-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="83805-131">不過，我們建議您設定它們，讓分析可以處理版本資訊。</span><span class="sxs-lookup"><span data-stu-id="83805-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="83805-132">在頁面中包含 Mobile Engagement 指令碼</span><span class="sxs-lookup"><span data-stu-id="83805-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="83805-133">使用下列其中一種方式，將 Mobile Engagement 指令碼新增至您的頁面：</span><span class="sxs-lookup"><span data-stu-id="83805-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="83805-134">或是這個：</span><span class="sxs-lookup"><span data-stu-id="83805-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="83805-135">Alias</span><span class="sxs-lookup"><span data-stu-id="83805-135">Alias</span></span>
<span data-ttu-id="83805-136">載入 Mobile Engagement Web SDK 指令碼之後，它會建立 **engagement** 別名來存取 SDK API。</span><span class="sxs-lookup"><span data-stu-id="83805-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="83805-137">您無法使用此別名來定義 SDK 組態。</span><span class="sxs-lookup"><span data-stu-id="83805-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="83805-138">此別名將用來做為此文件中的參考。</span><span class="sxs-lookup"><span data-stu-id="83805-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="83805-139">請注意，如果預設別名與另一個來自您頁面的全域變數發生衝突，您可以在載入 Mobile Engagement Web SDK 之前，於組態中將它重新定義，如下所示：</span><span class="sxs-lookup"><span data-stu-id="83805-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="83805-140">基本報告</span><span class="sxs-lookup"><span data-stu-id="83805-140">Basic reporting</span></span>
<span data-ttu-id="83805-141">Mobile Engagement 中的基本報告涵蓋了工作階段層級的統計資料，例如使用者、工作階段、活動和當機的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="83805-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="83805-142">工作階段追蹤</span><span class="sxs-lookup"><span data-stu-id="83805-142">Session tracking</span></span>
<span data-ttu-id="83805-143">Mobile Engagement 工作階段被分成一系列活動，每一個都可透過名稱來識別。</span><span class="sxs-lookup"><span data-stu-id="83805-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="83805-144">在傳統網站中，我們建議您在每個網站頁面上宣告不同的活動。</span><span class="sxs-lookup"><span data-stu-id="83805-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="83805-145">對於目前頁面永遠不會變更的網站或 Web 應用程式，您可能想要追蹤較小範圍中的活動，例如，在該頁面內。</span><span class="sxs-lookup"><span data-stu-id="83805-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="83805-146">無論如何，若要開始或變更目前的使用者活動，請呼叫 `engagement.agent.startActivity` 函式。</span><span class="sxs-lookup"><span data-stu-id="83805-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="83805-147">例如：</span><span class="sxs-lookup"><span data-stu-id="83805-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="83805-148">Mobile Engagement 伺服器會在應用程式頁面關閉後，於三分鐘內自動結束開啟的工作階段。</span><span class="sxs-lookup"><span data-stu-id="83805-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="83805-149">或者，您可以呼叫 `engagement.agent.endActivity`手動結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="83805-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="83805-150">這會將目前的使用者活動設定為 'Idle'。</span><span class="sxs-lookup"><span data-stu-id="83805-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="83805-151">除非有新的 `engagement.agent.startActivity` 呼叫繼續執行工作階段，否則該工作階段將會在 10 秒後結束。</span><span class="sxs-lookup"><span data-stu-id="83805-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="83805-152">您可以在全域 engagement 物件中設定 10 秒延遲，如下所示：</span><span class="sxs-lookup"><span data-stu-id="83805-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="83805-153">您無法在 `onunload` 回呼中使用 `engagement.agent.endActivity`，因為您不能在這個階段進行 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="83805-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="83805-154">進階報告</span><span class="sxs-lookup"><span data-stu-id="83805-154">Advanced reporting</span></span>
<span data-ttu-id="83805-155">此外，如果您想要報告應用程式特定的事件、錯誤及工作，就必須使用 Mobile Engagement API。</span><span class="sxs-lookup"><span data-stu-id="83805-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="83805-156">您可以透過 `engagement.agent` 物件存取 Mobile Engagement API。</span><span class="sxs-lookup"><span data-stu-id="83805-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="83805-157">您可以在 Mobile Engagement API 中存取 Mobile Engagement 中所有的進階功能。</span><span class="sxs-lookup"><span data-stu-id="83805-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="83805-158">[如何在 Web 應用程式中使用進階的 Mobile Engagement 標記 API](mobile-engagement-web-use-engagement-api.md)文章中會詳述此 API。</span><span class="sxs-lookup"><span data-stu-id="83805-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="83805-159">自訂用於 AJAX 呼叫的 URL</span><span class="sxs-lookup"><span data-stu-id="83805-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="83805-160">您可以自訂 Mobile Engagement Web SDK 使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="83805-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="83805-161">例如，若要重新定義記錄檔 URL (用於記錄的 SDK 端點)，您可以透過下列方式複寫組態：</span><span class="sxs-lookup"><span data-stu-id="83805-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="83805-162">如果您的 URL 函式傳回開頭為 `/`、`//`、`http://` 或 `https://` 的字串，便代表沒有使用預設配置。</span><span class="sxs-lookup"><span data-stu-id="83805-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="83805-163">根據預設，這些 URL 會使用 `https://` 配置。</span><span class="sxs-lookup"><span data-stu-id="83805-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="83805-164">如果您想要自訂預設配置，請透過下列方式複寫組態：</span><span class="sxs-lookup"><span data-stu-id="83805-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
