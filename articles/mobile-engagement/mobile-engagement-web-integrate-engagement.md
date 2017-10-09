---
title: "Mobile Engagement Web SDK 整合 aaaAzure |Microsoft 文件"
description: "hello 最新更新和 hello Azure Mobile Engagement Web SDK 的程序"
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
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="d392e-103">在 Web 應用程式中整合 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d392e-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d392e-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d392e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="d392e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d392e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d392e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d392e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d392e-107">Android</span><span class="sxs-lookup"><span data-stu-id="d392e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="d392e-108">本文章中的 hello 程序描述 hello 最簡單方式 tooactivate hello 分析和監視 Azure Mobile Engagement 中 web 應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="d392e-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="d392e-109">請遵循 hello 步驟 tooactivate hello 記錄報表所需的 toocompute 有關使用者、 工作階段、 活動、 當機，以及 technicals 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="d392e-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="d392e-110">應用程式相關的統計資料，例如事件、 錯誤和工作，您必須啟動記錄報表以手動方式使用 hello Azure Mobile Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="d392e-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="d392e-111">如需詳細資訊，了解[toouse hello 進階 Mobile Engagement 應用程式開發介面中的 web 應用程式所標記的方式](mobile-engagement-web-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d392e-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="d392e-112">簡介</span><span class="sxs-lookup"><span data-stu-id="d392e-112">Introduction</span></span>
<span data-ttu-id="d392e-113">[下載 hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453)。</span><span class="sxs-lookup"><span data-stu-id="d392e-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="d392e-114">Mobile Engagement Web SDK 隨附為單一的 JavaScript 檔案的 hello，azure-engagement.js，您擁有 tooinclude 網站或 web 應用程式的每一頁中。</span><span class="sxs-lookup"><span data-stu-id="d392e-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d392e-115">執行這個指令碼之前，您必須執行指令碼或程式碼片段，您必須撰寫 tooconfigure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d392e-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="d392e-116">瀏覽器相容性</span><span class="sxs-lookup"><span data-stu-id="d392e-116">Browser compatibility</span></span>
<span data-ttu-id="d392e-117">hello Mobile Engagement Web SDK 會使用原生的 JSON 編碼和解碼，此外 （依賴 hello W3C CORS 規格） 的 toocross 網域 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="d392e-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="d392e-118">它是與 hello 下列瀏覽器相容：</span><span class="sxs-lookup"><span data-stu-id="d392e-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="d392e-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="d392e-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="d392e-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="d392e-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="d392e-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="d392e-121">Firefox 3.5+</span></span>
* <span data-ttu-id="d392e-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="d392e-122">Chrome 4+</span></span>
* <span data-ttu-id="d392e-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="d392e-123">Safari 6+</span></span>
* <span data-ttu-id="d392e-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="d392e-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="d392e-125">設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d392e-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="d392e-126">撰寫指令碼建立的全域`azureEngagement`JavaScript 物件，如下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d392e-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="d392e-127">因為您的網站可能包含多個頁面，此範例假設這個指令碼包含於每個頁面中。</span><span class="sxs-lookup"><span data-stu-id="d392e-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="d392e-128">在此範例中，名為 hello JavaScript 物件`azure-engagement-conf.js`。</span><span class="sxs-lookup"><span data-stu-id="d392e-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="d392e-129">hello`connectionString`值，您的應用程式會顯示 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d392e-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d392e-130">`appVersionName` 和 `appVersionCode` 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d392e-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="d392e-131">不過，我們建議您設定它們，讓分析可以處理版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d392e-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="d392e-132">在頁面中包含 Mobile Engagement 指令碼</span><span class="sxs-lookup"><span data-stu-id="d392e-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="d392e-133">其中一種 hello 下列方式加入 Mobile Engagement 指令碼 tooyour 頁面：</span><span class="sxs-lookup"><span data-stu-id="d392e-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="d392e-134">或是這個：</span><span class="sxs-lookup"><span data-stu-id="d392e-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="d392e-135">Alias</span><span class="sxs-lookup"><span data-stu-id="d392e-135">Alias</span></span>
<span data-ttu-id="d392e-136">載入 hello Mobile Engagement Web SDK 指令碼之後，它會建立 hello **engagement**別名 tooaccess hello SDK Api。</span><span class="sxs-lookup"><span data-stu-id="d392e-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="d392e-137">您無法使用此別名 toodefine hello SDK 組態。</span><span class="sxs-lookup"><span data-stu-id="d392e-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="d392e-138">此別名將用來做為此文件中的參考。</span><span class="sxs-lookup"><span data-stu-id="d392e-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="d392e-139">請注意，是否與另一個全域變數，從您網頁衝突 hello 預設別名，您可以重新定義它 hello 組態中，如下所示載入 hello Mobile Engagement Web SDK 之前：</span><span class="sxs-lookup"><span data-stu-id="d392e-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="d392e-140">基本報告</span><span class="sxs-lookup"><span data-stu-id="d392e-140">Basic reporting</span></span>
<span data-ttu-id="d392e-141">Mobile Engagement 中的基本報告涵蓋了工作階段層級的統計資料，例如使用者、工作階段、活動和當機的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="d392e-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="d392e-142">工作階段追蹤</span><span class="sxs-lookup"><span data-stu-id="d392e-142">Session tracking</span></span>
<span data-ttu-id="d392e-143">Mobile Engagement 工作階段被分成一系列活動，每一個都可透過名稱來識別。</span><span class="sxs-lookup"><span data-stu-id="d392e-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="d392e-144">在傳統網站中，我們建議您在每個網站頁面上宣告不同的活動。</span><span class="sxs-lookup"><span data-stu-id="d392e-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="d392e-145">為網站或 web 應用程式中的 hello 本頁永遠不會變更，您可能想 tootrack hello 活動規模較小，例如 hello 網頁內。</span><span class="sxs-lookup"><span data-stu-id="d392e-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="d392e-146">是，toostart 或變更 hello 目前的使用者活動，呼叫 hello`engagement.agent.startActivity`函式。</span><span class="sxs-lookup"><span data-stu-id="d392e-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="d392e-147">例如：</span><span class="sxs-lookup"><span data-stu-id="d392e-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="d392e-148">hello Mobile Engagement 伺服器自動結束 hello 應用程式頁面上關閉後的 3 分鐘內開啟的工作階段。</span><span class="sxs-lookup"><span data-stu-id="d392e-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="d392e-149">或者，您可以呼叫 `engagement.agent.endActivity`手動結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="d392e-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="d392e-150">這會將目前使用者活動 too'Idle hello。 '</span><span class="sxs-lookup"><span data-stu-id="d392e-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="d392e-151">hello 工作階段會結束 10 秒之後，除非新太呼叫`engagement.agent.startActivity`繼續 hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d392e-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="d392e-152">您可以在 hello 全域 engagement 物件設定 hello 10 秒鐘的延遲，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d392e-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="d392e-153">您無法使用`engagement.agent.endActivity`在 hello`onunload`回呼因為您無法進行 AJAX 呼叫在這個階段。</span><span class="sxs-lookup"><span data-stu-id="d392e-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="d392e-154">進階報告</span><span class="sxs-lookup"><span data-stu-id="d392e-154">Advanced reporting</span></span>
<span data-ttu-id="d392e-155">（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您會需要 toouse hello Mobile Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="d392e-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="d392e-156">您可以透過 hello 存取 hello Mobile Engagement 應用程式開發介面`engagement.agent`物件。</span><span class="sxs-lookup"><span data-stu-id="d392e-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="d392e-157">您可以存取所有進階功能在 Mobile Engagement hello Mobile Engagement 應用程式開發介面中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d392e-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="d392e-158">hello API hello 文件中詳述[toouse hello 進階 Mobile Engagement 應用程式開發介面中的 web 應用程式所標記的方式](mobile-engagement-web-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d392e-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="d392e-159">自訂使用 AJAX 呼叫的 hello Url</span><span class="sxs-lookup"><span data-stu-id="d392e-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="d392e-160">您可以自訂 Url Mobile Engagement Web SDK 會使用該 hello。</span><span class="sxs-lookup"><span data-stu-id="d392e-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="d392e-161">例如，tooredefine hello 記錄 URL （hello SDK 結束點的記錄），您可以覆寫 hello 組態如下所示：</span><span class="sxs-lookup"><span data-stu-id="d392e-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="d392e-162">您的 URL 函式會傳回字串的開頭`/`， `//`， `http://`，或`https://`，不是 hello 預設配置。</span><span class="sxs-lookup"><span data-stu-id="d392e-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="d392e-163">根據預設，hello`https://`配置用於這些 Url。</span><span class="sxs-lookup"><span data-stu-id="d392e-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="d392e-164">如果您想 toocustomize hello 預設配置，來覆寫 hello 組態，像這樣：</span><span class="sxs-lookup"><span data-stu-id="d392e-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
