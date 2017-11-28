---
title: "在 Azure Application Insights 中分析 aaaTroubleshoot |Microsoft 文件"
description: "有關於 Application Insights 分析的問題嗎？ 從這裡開始。 "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="03f91-104">疑難排解 Application Insights 中的分析</span><span class="sxs-lookup"><span data-stu-id="03f91-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="03f91-105">有關於 [Application Insights 分析](app-insights-analytics.md)的問題嗎？</span><span class="sxs-lookup"><span data-stu-id="03f91-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="03f91-106">從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="03f91-106">Start here.</span></span> <span data-ttu-id="03f91-107">分析是 Azure Application Insights hello 功能強大的搜尋工具。</span><span class="sxs-lookup"><span data-stu-id="03f91-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="03f91-108">限制</span><span class="sxs-lookup"><span data-stu-id="03f91-108">Limits</span></span>
* <span data-ttu-id="03f91-109">目前，查詢結果會以有限的 toojust 超過一週的過去的資料。</span><span class="sxs-lookup"><span data-stu-id="03f91-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="03f91-110">我們測試的瀏覽器︰最新版本的 Chrome、Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="03f91-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="03f91-111">已知不相容的瀏覽器擴充功能</span><span class="sxs-lookup"><span data-stu-id="03f91-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="03f91-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="03f91-112">Ghostery</span></span>

<span data-ttu-id="03f91-113">停用 hello 擴充功能，或使用不同的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="03f91-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="03f91-114"><a name="e-a"></a> 「未預期的錯誤」</span><span class="sxs-lookup"><span data-stu-id="03f91-114"><a name="e-a"></a> "Unexpected error"</span></span>
![[未預期的錯誤] 畫面](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="03f91-116">在入口網站執行階段期間發生的內部錯誤 – 未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="03f91-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="03f91-117">清除 hello 瀏覽器的快取。</span><span class="sxs-lookup"><span data-stu-id="03f91-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="03f91-118"><a name="e-b"></a>403...請再試一次 tooreload</span><span class="sxs-lookup"><span data-stu-id="03f91-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403...請再試一次 tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="03f91-120">發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。</span><span class="sxs-lookup"><span data-stu-id="03f91-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="03f91-121">hello 入口網站可能沒有太復原，而不變更瀏覽器設定的方法。</span><span class="sxs-lookup"><span data-stu-id="03f91-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="03f91-122">確認[啟用第三方 cookie](#cookies) hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="03f91-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="03f91-123"><a name="authentication"></a>403 ... 確認安全性區域</span><span class="sxs-lookup"><span data-stu-id="03f91-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403 ... 確認安全性區域](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="03f91-125">發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。</span><span class="sxs-lookup"><span data-stu-id="03f91-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="03f91-126">hello 入口網站可能沒有太復原，而不變更瀏覽器設定的方法。</span><span class="sxs-lookup"><span data-stu-id="03f91-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="03f91-127">確認[啟用第三方 cookie](#cookies) hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="03f91-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="03f91-128">是否使用最愛、 書籤或儲存的連結 tooopen hello Analytics 入口網站？</span><span class="sxs-lookup"><span data-stu-id="03f91-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="03f91-129">您登入您儲存 hello 連結時，使用不同的認證嗎？</span><span class="sxs-lookup"><span data-stu-id="03f91-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="03f91-130">嘗試使用 InPrivate/incognito 瀏覽器視窗 (關閉所有這類視窗之後)。</span><span class="sxs-lookup"><span data-stu-id="03f91-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="03f91-131">您將有 tooprovide 您的認證。</span><span class="sxs-lookup"><span data-stu-id="03f91-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="03f91-132">開啟另一個 （一般） 的瀏覽器視窗，並移過[Azure](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="03f91-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="03f91-133">登出。然後開啟您的連結，並使用 hello 正確的認證登入。</span><span class="sxs-lookup"><span data-stu-id="03f91-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="03f91-134">Edge 和 Internet Explorer 的使用者也會在不支援信任的區域設定時收到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="03f91-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="03f91-135">同時確認[Analytics 入口網站](https://analytics.applicationinsights.io)和[Azure Active Directory 網站](https://portal.azure.com)hello 中相同的安全性區域：</span><span class="sxs-lookup"><span data-stu-id="03f91-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="03f91-136">在 Internet Explorer 中，開啟 [網際網路選項]、[安全性]、[信任的網站]、[網站]：</span><span class="sxs-lookup"><span data-stu-id="03f91-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![網際網路選項 對話方塊，新增站台 tooTrusted 站台](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="03f91-138">在 hello 網站清單中，如果包含了任何 hello 下列 Url，請確定該 hello 其他人也會包含：</span><span class="sxs-lookup"><span data-stu-id="03f91-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="03f91-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="03f91-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="03f91-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="03f91-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="03f91-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="03f91-141">https://login.windows.net</span></span>

## <span data-ttu-id="03f91-142"><a name="e-d"></a>404 ...找不到資源</span><span class="sxs-lookup"><span data-stu-id="03f91-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... 找不到資源](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="03f91-144">應用程式資源已從 Application Insights 中刪除，且不再提供。</span><span class="sxs-lookup"><span data-stu-id="03f91-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="03f91-145">如果您儲存 hello URL toohello 分析 頁面上，也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="03f91-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="03f91-146"><a name="e-e"></a>403 ...沒有授權</span><span class="sxs-lookup"><span data-stu-id="03f91-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... 未獲授權](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="03f91-148">您沒有權限 tooopen 此應用程式在分析中。</span><span class="sxs-lookup"><span data-stu-id="03f91-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="03f91-149">您從別處取得 hello 連結？</span><span class="sxs-lookup"><span data-stu-id="03f91-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="03f91-150">請確定您是在 hello toomake 要求他們[讀者或參與者的這個資源群組](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="03f91-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="03f91-151">您沒有儲存 hello 連結使用不同的認證嗎？</span><span class="sxs-lookup"><span data-stu-id="03f91-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="03f91-152">開啟 hello [Azure 入口網站](https://portal.azure.com)、 登出，然後再次嘗試此連結，提供 hello 正確的認證。</span><span class="sxs-lookup"><span data-stu-id="03f91-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="03f91-153"><a name="html-storage"></a>403 ...HTML5 儲存體</span><span class="sxs-lookup"><span data-stu-id="03f91-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="03f91-154">我們的入口網站會使用 HTML5 localStorage 和 sessionStorage。</span><span class="sxs-lookup"><span data-stu-id="03f91-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="03f91-155">Chrome︰設定、隱私權、內容設定。</span><span class="sxs-lookup"><span data-stu-id="03f91-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="03f91-156">Internet Explorer︰網際網路選項、進階索引標籤、安全性、啟用 DOM 儲存</span><span class="sxs-lookup"><span data-stu-id="03f91-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403...再試一次 tooenable HTML5 儲存體](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="03f91-158"><a name="e-g"></a>404 ...找不到訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="03f91-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ...找不到訂用帳戶](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="03f91-160">hello URL 無效。</span><span class="sxs-lookup"><span data-stu-id="03f91-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="03f91-161">開啟中的 hello 應用程式資源[Application Insights 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="03f91-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="03f91-162">然後使用 hello 分析按鈕。</span><span class="sxs-lookup"><span data-stu-id="03f91-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="03f91-163"><a name="e-h"></a>404 ... 頁面不存在</span><span class="sxs-lookup"><span data-stu-id="03f91-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ...頁面不存在](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="03f91-165">hello URL 無效。</span><span class="sxs-lookup"><span data-stu-id="03f91-165">hello URL is invalid.</span></span>

* <span data-ttu-id="03f91-166">開啟中的 hello 應用程式資源[Application Insights 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="03f91-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="03f91-167">然後使用 hello 分析按鈕。</span><span class="sxs-lookup"><span data-stu-id="03f91-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="03f91-168"><a name="cookies"></a>啟用協力廠商 cookie</span><span class="sxs-lookup"><span data-stu-id="03f91-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="03f91-169">請參閱[如何 toodisable 協力廠商 cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)，但請注意，我們需要**啟用**它們。</span><span class="sxs-lookup"><span data-stu-id="03f91-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

