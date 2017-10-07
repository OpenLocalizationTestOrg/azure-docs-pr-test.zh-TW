---
title: "aaaAzure Mobile Engagement 使用者介面-內容連接"
description: "了解如何在 Azure Mobile Engagement toomanage hello 唯一內容推播通知的 hello 不同類型的活動"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="997de-103">如何 toomanage hello hello 的推播通知活動的不同類型的唯一內容</span><span class="sxs-lookup"><span data-stu-id="997de-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="997de-104">您可以使用 hello 新觸達活動 toomodify hello 內容的宣告、 投票、 資料推入和磚 (僅限 Windows Phone) 的內容 > 一節。</span><span class="sxs-lookup"><span data-stu-id="997de-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="997de-105">hello 內容設定的推送活動的是特定 toohello 活動類型。</span><span class="sxs-lookup"><span data-stu-id="997de-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="997de-106">內容類型：</span><span class="sxs-lookup"><span data-stu-id="997de-106">Content types:</span></span>
* <span data-ttu-id="997de-107">通知</span><span class="sxs-lookup"><span data-stu-id="997de-107">Announcements</span></span>
* <span data-ttu-id="997de-108">投票</span><span class="sxs-lookup"><span data-stu-id="997de-108">Polls</span></span>
* <span data-ttu-id="997de-109">資料推送</span><span class="sxs-lookup"><span data-stu-id="997de-109">Data pushes</span></span>
* <span data-ttu-id="997de-110">磚 (僅限 Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="997de-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="997de-111">通知的內容</span><span class="sxs-lookup"><span data-stu-id="997de-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="997de-113">選擇宣告的 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="997de-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="997de-114">僅通知：這是簡單的標準通知。</span><span class="sxs-lookup"><span data-stu-id="997de-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="997de-115">這表示如果使用者按一下它，會出現任何其他檢視，但只有 hello 動作相關聯 tooit 就會發生。</span><span class="sxs-lookup"><span data-stu-id="997de-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="997de-116">文字公告： 它是既定 hello 使用者 toohave 看一下文字檢視通知。</span><span class="sxs-lookup"><span data-stu-id="997de-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="997de-117">Web 公告： 它是既定 hello 使用者 toohave 查看網頁檢視的通知。</span><span class="sxs-lookup"><span data-stu-id="997de-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="997de-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="997de-118">See also</span></span>
* <span data-ttu-id="997de-119">[觸達 - 作法 - 通知][Link 3]</span><span class="sxs-lookup"><span data-stu-id="997de-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="997de-120">關於 Web 檢視通知：</span><span class="sxs-lookup"><span data-stu-id="997de-120">About Web View Announcements:</span></span>
<span data-ttu-id="997de-121">Hello 模式 {"deviceid}"hello HTML 程式碼或 JavaScript 程式碼您在此處提供的項目會自動取代為由顯示 hello 公告 hello 裝置 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="997de-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="997de-122">這是外部輕鬆 tooretrieve Azure Mobile Engagement 裝置識別碼 web 程式後端辦公室託管的服務。</span><span class="sxs-lookup"><span data-stu-id="997de-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="997de-123">如果您想 toocreate 完整螢幕 web 檢視 （不含 hello 動作並結束提供預設按鈕我們） 您可以使用 hello web 檢視宣告的 JavaScript 程式碼中的下列功能：</span><span class="sxs-lookup"><span data-stu-id="997de-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="997de-124">執行 hello 公告： ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="997de-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="997de-125">結束 hello 公告： ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="997de-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="997de-126">選擇您的動作：</span><span class="sxs-lookup"><span data-stu-id="997de-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="997de-127">關於動作 URL：</span><span class="sxs-lookup"><span data-stu-id="997de-127">About Action URLs:</span></span>
<span data-ttu-id="997de-128">可由目標裝置的作業系統解譯的任何 URL 都可以用來做為動作 URL。</span><span class="sxs-lookup"><span data-stu-id="997de-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="997de-129">可能您的應用程式的所有專用 URL （例如 toomake 使用者跳 tooa 特定畫面） 的支援也可用以做為動作 URL。</span><span class="sxs-lookup"><span data-stu-id="997de-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="997de-130">Hello {deviceid} 模式每次發生自動取代為執行 hello hello 裝置 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="997de-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="997de-131">這可以是透過您的後端辦公室託管的外部 web 服務使用的 tooeasily 擷取 Azure Mobile Engagement 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="997de-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="997de-132">**Android + iOS 動作**</span><span class="sxs-lookup"><span data-stu-id="997de-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="997de-133">開啟網頁</span><span class="sxs-lookup"><span data-stu-id="997de-133">Open a web page</span></span>
  * <span data-ttu-id="997de-134">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="997de-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="997de-135">範例︰http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="997de-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="997de-136">傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="997de-136">Send an e-mail</span></span>
  * <span data-ttu-id="997de-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="997de-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="997de-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="997de-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="997de-139">傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="997de-139">Send a SMS</span></span>
  * <span data-ttu-id="997de-140">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="997de-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="997de-141">範例：sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="997de-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="997de-142">撥電話號碼</span><span class="sxs-lookup"><span data-stu-id="997de-142">Dial a phone number</span></span>
  * <span data-ttu-id="997de-143">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="997de-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="997de-144">範例：tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="997de-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="997de-145">**僅限 Android 的動作**</span><span class="sxs-lookup"><span data-stu-id="997de-145">**Android only actions**</span></span>
  * <span data-ttu-id="997de-146">下載 hello Play Store 上的應用程式</span><span class="sxs-lookup"><span data-stu-id="997de-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="997de-147">market://details?id=\[應用程式套件\]</span><span class="sxs-lookup"><span data-stu-id="997de-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="997de-148">範例：market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="997de-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="997de-149">開始地理當地化的搜尋</span><span class="sxs-lookup"><span data-stu-id="997de-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="997de-150">geo:0,0?q=\[搜尋查詢\]</span><span class="sxs-lookup"><span data-stu-id="997de-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="997de-151">範例：geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="997de-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="997de-152">**僅限 iOS 的動作**</span><span class="sxs-lookup"><span data-stu-id="997de-152">**iOS only actions**</span></span>
  * <span data-ttu-id="997de-153">下載 hello App Store 上的應用程式</span><span class="sxs-lookup"><span data-stu-id="997de-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="997de-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="997de-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="997de-155">範例︰http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="997de-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="997de-156">Windows 動作</span><span class="sxs-lookup"><span data-stu-id="997de-156">Windows Actions</span></span>
  * <span data-ttu-id="997de-157">開啟網頁</span><span class="sxs-lookup"><span data-stu-id="997de-157">Open a web page</span></span>
  * <span data-ttu-id="997de-158">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="997de-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="997de-159">範例︰http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="997de-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="997de-160">傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="997de-160">Send an e-mail</span></span>
  * <span data-ttu-id="997de-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="997de-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="997de-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="997de-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="997de-163">傳送簡訊 (需要 Skype 市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="997de-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="997de-164">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="997de-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="997de-165">範例：sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="997de-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="997de-166">撥電話號碼 (需要 Skype 市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="997de-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="997de-167">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="997de-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="997de-168">範例：tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="997de-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="997de-169">下載 hello Play Store 上的應用程式</span><span class="sxs-lookup"><span data-stu-id="997de-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="997de-170">ms-windows-store:PDP?PFN=\[app package ID\]</span><span class="sxs-lookup"><span data-stu-id="997de-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="997de-171">範例：ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="997de-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="997de-172">開始 bingmaps 搜尋</span><span class="sxs-lookup"><span data-stu-id="997de-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="997de-173">bingmaps:?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="997de-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="997de-174">範例：bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="997de-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="997de-175">使用自訂配置</span><span class="sxs-lookup"><span data-stu-id="997de-175">Use a custom scheme</span></span>
  * <span data-ttu-id="997de-176">\[custom scheme\]://\[custom scheme params\]</span><span class="sxs-lookup"><span data-stu-id="997de-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="997de-177">範例：myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="997de-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="997de-178">使用套件資料 (需要副檔名讀取的市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="997de-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="997de-179">\[folder\]\[data\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="997de-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="997de-180">範例：myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="997de-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="997de-181">建置追蹤 URL：</span><span class="sxs-lookup"><span data-stu-id="997de-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="997de-182">請參閱 hello 的 < 設定 > 一節的 hello<UI Documentation>的建置追蹤 URL 的指示，可讓使用者 toodownload 其中一個其他的應用程式。</span><span class="sxs-lookup"><span data-stu-id="997de-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="997de-183">定義宣告的 hello 文字</span><span class="sxs-lookup"><span data-stu-id="997de-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="997de-184">填寫 hello 標題、 內容和宣告的按鈕文字。</span><span class="sxs-lookup"><span data-stu-id="997de-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="997de-185">您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。</span><span class="sxs-lookup"><span data-stu-id="997de-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="997de-186">目標對象可以根據 hello 意見反應是否這個活動只推入，回覆，採取動作，或結束。</span><span class="sxs-lookup"><span data-stu-id="997de-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="997de-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="997de-187">See also</span></span>
* <span data-ttu-id="997de-188">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="997de-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="997de-189">投票的內容</span><span class="sxs-lookup"><span data-stu-id="997de-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="997de-191">填寫 hello 標題、 描述和宣告的按鈕文字。</span><span class="sxs-lookup"><span data-stu-id="997de-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="997de-192">接著，新增問題和選擇 hello 答案 tooyour 問題。</span><span class="sxs-lookup"><span data-stu-id="997de-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="997de-193">您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。</span><span class="sxs-lookup"><span data-stu-id="997de-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="997de-194">選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。</span><span class="sxs-lookup"><span data-stu-id="997de-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="997de-195">目標對象也可以根據輪詢回答意見反應，hello 問題與解答的選擇，當做準則。</span><span class="sxs-lookup"><span data-stu-id="997de-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="997de-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="997de-196">See also</span></span>
* <span data-ttu-id="997de-197">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="997de-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="997de-198">資料推送的內容</span><span class="sxs-lookup"><span data-stu-id="997de-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="997de-200">選擇資料的 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="997de-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="997de-201">文字</span><span class="sxs-lookup"><span data-stu-id="997de-201">Text</span></span>
* <span data-ttu-id="997de-202">二進位資料</span><span class="sxs-lookup"><span data-stu-id="997de-202">Binary data</span></span>
* <span data-ttu-id="997de-203">Base64 資料</span><span class="sxs-lookup"><span data-stu-id="997de-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="997de-204">定義資料的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="997de-204">Define hello content of your data</span></span>
* <span data-ttu-id="997de-205">如果您選取 toopush 文字資料，複製並貼上 hello 「 內容 」 中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="997de-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="997de-206">如果您選取 toopush 二進位或 base64 資料，請使用 [上傳您的檔案] 按鈕 tooupload hello 您的檔案。</span><span class="sxs-lookup"><span data-stu-id="997de-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="997de-207">您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。</span><span class="sxs-lookup"><span data-stu-id="997de-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="997de-208">選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。</span><span class="sxs-lookup"><span data-stu-id="997de-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="997de-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="997de-209">See also</span></span>
* <span data-ttu-id="997de-210">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="997de-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="997de-211">磚的內容 (僅限 Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="997de-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="997de-213">定義磚的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="997de-213">Define hello content of your tile</span></span>
<span data-ttu-id="997de-214">hello 磚裝載是顯示在 Windows Phone 裝置上的應用程式的 hello 磚中的 hello 文字 toobe。</span><span class="sxs-lookup"><span data-stu-id="997de-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="997de-215">圖格發送是適用於 Windows Phone 的原生推送 hello Microsoft 推播通知服務 (MPNS) 版本。</span><span class="sxs-lookup"><span data-stu-id="997de-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="997de-216">hello 磚推入型別是 hello 唯一發送類型沒有回應，因此 hello 觀眾的未來的活動無法建置 hello 結果的並排顯示推播宣傳活動。</span><span class="sxs-lookup"><span data-stu-id="997de-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="997de-217">另請參閱</span><span class="sxs-lookup"><span data-stu-id="997de-217">See also</span></span>
* <span data-ttu-id="997de-218">[API 文件 - 觸達 API - 原生推送][Link 4]</span><span class="sxs-lookup"><span data-stu-id="997de-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

