---
title: "為 Azure Application Insights 中的 Analytics 進行疑難排解 | Microsoft Docs"
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
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="fcdfb-104">疑難排解 Application Insights 中的分析</span><span class="sxs-lookup"><span data-stu-id="fcdfb-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="fcdfb-105">有關於 [Application Insights 分析](app-insights-analytics.md)的問題嗎？</span><span class="sxs-lookup"><span data-stu-id="fcdfb-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="fcdfb-106">從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-106">Start here.</span></span> <span data-ttu-id="fcdfb-107">「分析」是強大的 Azure Application Insights 搜尋工具。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="fcdfb-108">限制</span><span class="sxs-lookup"><span data-stu-id="fcdfb-108">Limits</span></span>
* <span data-ttu-id="fcdfb-109">目前，查詢結果受限於僅只過去一週的資料。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="fcdfb-110">我們測試的瀏覽器︰最新版本的 Chrome、Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="fcdfb-111">已知不相容的瀏覽器擴充功能</span><span class="sxs-lookup"><span data-stu-id="fcdfb-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="fcdfb-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="fcdfb-112">Ghostery</span></span>

<span data-ttu-id="fcdfb-113">停用擴充功能或使用不同的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="fcdfb-114"><a name="e-a"></a> 「未預期的錯誤」</span><span class="sxs-lookup"><span data-stu-id="fcdfb-114"><a name="e-a"></a> "Unexpected error"</span></span>
![[未預期的錯誤] 畫面](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="fcdfb-116">在入口網站執行階段期間發生的內部錯誤 – 未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="fcdfb-117">清除瀏覽器的快取。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="fcdfb-118"><a name="e-b"></a>403 ... 請嘗試重新載入</span><span class="sxs-lookup"><span data-stu-id="fcdfb-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403 ... 請嘗試重新載入](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="fcdfb-120">發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="fcdfb-121">若未變更瀏覽器設定，入口網站可能無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="fcdfb-122">確認已在瀏覽器中 [啟用協力廠商 Cookie](#cookies) 。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="fcdfb-123"><a name="authentication"></a>403 ... 確認安全性區域</span><span class="sxs-lookup"><span data-stu-id="fcdfb-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403 ... 確認安全性區域](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="fcdfb-125">發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="fcdfb-126">若未變更瀏覽器設定，入口網站可能無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="fcdfb-127">確認已在瀏覽器中 [啟用協力廠商 Cookie](#cookies) 。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="fcdfb-128">您使用我的最愛、書籤或儲存的連結來開啟分析入口網站嗎？</span><span class="sxs-lookup"><span data-stu-id="fcdfb-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="fcdfb-129">您登入時所使用的認證與您儲存連結時使用的認證不同嗎？</span><span class="sxs-lookup"><span data-stu-id="fcdfb-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="fcdfb-130">嘗試使用 InPrivate/incognito 瀏覽器視窗 (關閉所有這類視窗之後)。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="fcdfb-131">您必須提供認證。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="fcdfb-132">開啟另一個 (一般) 瀏覽器視窗並前往 [Azure](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="fcdfb-133">登出。然後開啟您的連結並使用正確的認證登入。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="fcdfb-134">Edge 和 Internet Explorer 的使用者也會在不支援信任的區域設定時收到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="fcdfb-135">確認[分析入口網站](https://analytics.applicationinsights.io)和 [Azure Active Directory 入口網站](https://portal.azure.com)位於相同的安全性區域：</span><span class="sxs-lookup"><span data-stu-id="fcdfb-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="fcdfb-136">在 Internet Explorer 中，開啟 [網際網路選項]、[安全性]、[信任的網站]、[網站]：</span><span class="sxs-lookup"><span data-stu-id="fcdfb-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![[網際網路選項] 對話方塊，將網站新增到信任的網站](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="fcdfb-138">在 [網站] 清單中，如果包含下列任一個 URL，請確定也會包含其他的 URL：</span><span class="sxs-lookup"><span data-stu-id="fcdfb-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="fcdfb-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="fcdfb-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="fcdfb-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="fcdfb-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="fcdfb-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="fcdfb-141">https://login.windows.net</span></span>

## <span data-ttu-id="fcdfb-142"><a name="e-d"></a>404 ...找不到資源</span><span class="sxs-lookup"><span data-stu-id="fcdfb-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... 找不到資源](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="fcdfb-144">應用程式資源已從 Application Insights 中刪除，且不再提供。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="fcdfb-145">這可能會在您將 URL 儲存到 [分析] 頁面時發生。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="fcdfb-146"><a name="e-e"></a>403 ...沒有授權</span><span class="sxs-lookup"><span data-stu-id="fcdfb-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... 未獲授權](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="fcdfb-148">您沒有權限可在分析中開啟此應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="fcdfb-149">您的連結是由其他人所提供嗎？</span><span class="sxs-lookup"><span data-stu-id="fcdfb-149">Did you get the link from someone else?</span></span> <span data-ttu-id="fcdfb-150">要求他們確認您是 [這個資源群組的讀取者或參與者](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="fcdfb-151">您使用不同的認證來儲存連結嗎？</span><span class="sxs-lookup"><span data-stu-id="fcdfb-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="fcdfb-152">開啟 [Azure 入口網站](https://portal.azure.com)、登出，然後提供正確的認證再試一次連結。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="fcdfb-153"><a name="html-storage"></a>403 ...HTML5 儲存體</span><span class="sxs-lookup"><span data-stu-id="fcdfb-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="fcdfb-154">我們的入口網站會使用 HTML5 localStorage 和 sessionStorage。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="fcdfb-155">Chrome︰設定、隱私權、內容設定。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="fcdfb-156">Internet Explorer︰網際網路選項、進階索引標籤、安全性、啟用 DOM 儲存</span><span class="sxs-lookup"><span data-stu-id="fcdfb-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403 ... 嘗試啟用 HTML5 儲存體](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="fcdfb-158"><a name="e-g"></a>404 ...找不到訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fcdfb-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ...找不到訂用帳戶](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="fcdfb-160">URL 無效。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-160">The URL is invalid.</span></span> 

* <span data-ttu-id="fcdfb-161">開啟 [Application Insights 入口網站](https://portal.azure.com)中的應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="fcdfb-162">然後使用 [分析] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="fcdfb-163"><a name="e-h"></a>404 ... 頁面不存在</span><span class="sxs-lookup"><span data-stu-id="fcdfb-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ...頁面不存在](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="fcdfb-165">URL 無效。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-165">The URL is invalid.</span></span>

* <span data-ttu-id="fcdfb-166">開啟 [Application Insights 入口網站](https://portal.azure.com)中的應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="fcdfb-167">然後使用 [分析] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="fcdfb-168"><a name="cookies"></a>啟用協力廠商 cookie</span><span class="sxs-lookup"><span data-stu-id="fcdfb-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="fcdfb-169">請參閱 [如何停用協力廠商 Cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)，但請注意，我們需要 **啟用** 它們。</span><span class="sxs-lookup"><span data-stu-id="fcdfb-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

