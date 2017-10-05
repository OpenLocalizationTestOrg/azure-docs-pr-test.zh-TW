---
title: "Azure Mobile Engagement 使用者介面 - 觸達內容"
description: "了解如何在 Azure Mobile Engagement 管理不同類型推播通知活動的指定內容"
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
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="df650-103">如何管理不同類型推播通知活動的指定內容</span><span class="sxs-lookup"><span data-stu-id="df650-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="df650-104">您可以使用新觸達活動的 [內容] 區段修改通知、投票、資料推送和磚 (僅限 Windows Phone) 的內容。</span><span class="sxs-lookup"><span data-stu-id="df650-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="df650-105">推播活動的內容設定與活動類型有關。</span><span class="sxs-lookup"><span data-stu-id="df650-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="df650-106">內容類型：</span><span class="sxs-lookup"><span data-stu-id="df650-106">Content types:</span></span>
* <span data-ttu-id="df650-107">通知</span><span class="sxs-lookup"><span data-stu-id="df650-107">Announcements</span></span>
* <span data-ttu-id="df650-108">投票</span><span class="sxs-lookup"><span data-stu-id="df650-108">Polls</span></span>
* <span data-ttu-id="df650-109">資料推送</span><span class="sxs-lookup"><span data-stu-id="df650-109">Data pushes</span></span>
* <span data-ttu-id="df650-110">磚 (僅限 Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="df650-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="df650-111">通知的內容</span><span class="sxs-lookup"><span data-stu-id="df650-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="df650-113">選擇通知的類型：</span><span class="sxs-lookup"><span data-stu-id="df650-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="df650-114">僅通知：這是簡單的標準通知。</span><span class="sxs-lookup"><span data-stu-id="df650-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="df650-115">表示如果使用者按一下通知，不會出現任何其他檢視，但是會發生與它關聯的動作。</span><span class="sxs-lookup"><span data-stu-id="df650-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="df650-116">文字通知：這是一種吸引使用者查看文字檢視的通知。</span><span class="sxs-lookup"><span data-stu-id="df650-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="df650-117">Web 通知：這是一種吸引使用者查看 Web 檢視的通知。</span><span class="sxs-lookup"><span data-stu-id="df650-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="df650-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df650-118">See also</span></span>
* <span data-ttu-id="df650-119">[觸達 - 作法 - 通知][Link 3]</span><span class="sxs-lookup"><span data-stu-id="df650-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="df650-120">關於 Web 檢視通知：</span><span class="sxs-lookup"><span data-stu-id="df650-120">About Web View Announcements:</span></span>
<span data-ttu-id="df650-121">您在此處提供的每個 "{deviceid}" 字樣 (在 HTML 程式碼或 JavaScript 程式碼中) 將會自動取代為顯示通知的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="df650-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="df650-122">這個簡單的方法可以擷取您後端系統裝載的外部 Web 服務中的 Azure Mobile Engagement 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="df650-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="df650-123">如果您想要建立全螢幕的 Web 檢視 (不含我們提供的預設 [動作] 和 [離開] 按鈕)，您可以從 Web 檢視通知的 JavaScript 程式碼中使用下列函式：</span><span class="sxs-lookup"><span data-stu-id="df650-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="df650-124">執行通知動作：ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="df650-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="df650-125">離開通知：ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="df650-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="df650-126">選擇您的動作：</span><span class="sxs-lookup"><span data-stu-id="df650-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="df650-127">關於動作 URL：</span><span class="sxs-lookup"><span data-stu-id="df650-127">About Action URLs:</span></span>
<span data-ttu-id="df650-128">可由目標裝置的作業系統解譯的任何 URL 都可以用來做為動作 URL。</span><span class="sxs-lookup"><span data-stu-id="df650-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="df650-129">應用程式可能支援的任何專用 URL (例如讓使用者跳至特定畫面) 也可用來做為動作 URL。</span><span class="sxs-lookup"><span data-stu-id="df650-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="df650-130">每個 {deviceid} 字樣的項目都會自動取代為執行動作的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="df650-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="df650-131">透過您後端系統裝載的外部 Web 服務，這可用來輕鬆擷取 Azure Mobile Engagement 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="df650-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="df650-132">**Android + iOS 動作**</span><span class="sxs-lookup"><span data-stu-id="df650-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="df650-133">開啟網頁</span><span class="sxs-lookup"><span data-stu-id="df650-133">Open a web page</span></span>
  * <span data-ttu-id="df650-134">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="df650-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="df650-135">範例︰http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="df650-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="df650-136">傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="df650-136">Send an e-mail</span></span>
  * <span data-ttu-id="df650-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="df650-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="df650-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="df650-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="df650-139">傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="df650-139">Send a SMS</span></span>
  * <span data-ttu-id="df650-140">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="df650-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="df650-141">範例：sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="df650-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="df650-142">撥電話號碼</span><span class="sxs-lookup"><span data-stu-id="df650-142">Dial a phone number</span></span>
  * <span data-ttu-id="df650-143">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="df650-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="df650-144">範例：tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="df650-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="df650-145">**僅限 Android 的動作**</span><span class="sxs-lookup"><span data-stu-id="df650-145">**Android only actions**</span></span>
  * <span data-ttu-id="df650-146">下載 Play 商店上的應用程式</span><span class="sxs-lookup"><span data-stu-id="df650-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="df650-147">market://details?id=\[應用程式套件\]</span><span class="sxs-lookup"><span data-stu-id="df650-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="df650-148">範例：market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="df650-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="df650-149">開始地理當地化的搜尋</span><span class="sxs-lookup"><span data-stu-id="df650-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="df650-150">geo:0,0?q=\[搜尋查詢\]</span><span class="sxs-lookup"><span data-stu-id="df650-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="df650-151">範例：geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="df650-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="df650-152">**僅限 iOS 的動作**</span><span class="sxs-lookup"><span data-stu-id="df650-152">**iOS only actions**</span></span>
  * <span data-ttu-id="df650-153">下載 App Store 上的應用程式</span><span class="sxs-lookup"><span data-stu-id="df650-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="df650-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="df650-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="df650-155">範例︰http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="df650-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="df650-156">Windows 動作</span><span class="sxs-lookup"><span data-stu-id="df650-156">Windows Actions</span></span>
  * <span data-ttu-id="df650-157">開啟網頁</span><span class="sxs-lookup"><span data-stu-id="df650-157">Open a web page</span></span>
  * <span data-ttu-id="df650-158">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="df650-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="df650-159">範例︰http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="df650-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="df650-160">傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="df650-160">Send an e-mail</span></span>
  * <span data-ttu-id="df650-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="df650-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="df650-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="df650-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="df650-163">傳送簡訊 (需要 Skype 市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="df650-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="df650-164">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="df650-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="df650-165">範例：sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="df650-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="df650-166">撥電話號碼 (需要 Skype 市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="df650-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="df650-167">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="df650-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="df650-168">範例：tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="df650-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="df650-169">下載 Play 商店上的應用程式</span><span class="sxs-lookup"><span data-stu-id="df650-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="df650-170">ms-windows-store:PDP?PFN=\[app package ID\]</span><span class="sxs-lookup"><span data-stu-id="df650-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="df650-171">範例：ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="df650-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="df650-172">開始 bingmaps 搜尋</span><span class="sxs-lookup"><span data-stu-id="df650-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="df650-173">bingmaps:?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="df650-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="df650-174">範例：bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="df650-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="df650-175">使用自訂配置</span><span class="sxs-lookup"><span data-stu-id="df650-175">Use a custom scheme</span></span>
  * <span data-ttu-id="df650-176">\[custom scheme\]://\[custom scheme params\]</span><span class="sxs-lookup"><span data-stu-id="df650-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="df650-177">範例：myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="df650-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="df650-178">使用套件資料 (需要副檔名讀取的市集應用程式)</span><span class="sxs-lookup"><span data-stu-id="df650-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="df650-179">\[folder\]\[data\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="df650-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="df650-180">範例：myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="df650-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="df650-181">建置追蹤 URL：</span><span class="sxs-lookup"><span data-stu-id="df650-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="df650-182">請參閱 <UI Documentation> 的＜設定＞一節，了解建置可讓使用者下載其他應用程式之追蹤 URL 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="df650-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="df650-183">定義您的通知文字：</span><span class="sxs-lookup"><span data-stu-id="df650-183">Define the texts of your announcement</span></span>
<span data-ttu-id="df650-184">填寫通知的標題、內容和按鈕文字。</span><span class="sxs-lookup"><span data-stu-id="df650-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="df650-185">您可以根據使用者如何回應此活動的觸達意見反應，找出未來的活動對象。</span><span class="sxs-lookup"><span data-stu-id="df650-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="df650-186">選取目標對象可以根據此活動是否已推送、回覆、採取動作或離開的意見反應。</span><span class="sxs-lookup"><span data-stu-id="df650-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="df650-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df650-187">See also</span></span>
* <span data-ttu-id="df650-188">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="df650-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="df650-189">投票的內容</span><span class="sxs-lookup"><span data-stu-id="df650-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="df650-191">填寫通知的標題、描述和按鈕文字。</span><span class="sxs-lookup"><span data-stu-id="df650-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="df650-192">然後，新增問題和問題的答案選項。</span><span class="sxs-lookup"><span data-stu-id="df650-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="df650-193">您可以根據使用者如何回應此活動的觸達意見反應，找出未來的活動對象。</span><span class="sxs-lookup"><span data-stu-id="df650-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="df650-194">選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。</span><span class="sxs-lookup"><span data-stu-id="df650-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="df650-195">選取目標對象時也可以根據投票答案的意見反應，將其中的問題和答案選項做為準則。</span><span class="sxs-lookup"><span data-stu-id="df650-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="df650-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df650-196">See also</span></span>
* <span data-ttu-id="df650-197">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="df650-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="df650-198">資料推送的內容</span><span class="sxs-lookup"><span data-stu-id="df650-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="df650-200">選擇您的資料類型：</span><span class="sxs-lookup"><span data-stu-id="df650-200">Choose the type of your data:</span></span>
* <span data-ttu-id="df650-201">文字</span><span class="sxs-lookup"><span data-stu-id="df650-201">Text</span></span>
* <span data-ttu-id="df650-202">二進位資料</span><span class="sxs-lookup"><span data-stu-id="df650-202">Binary data</span></span>
* <span data-ttu-id="df650-203">Base64 資料</span><span class="sxs-lookup"><span data-stu-id="df650-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="df650-204">定義資料的內容</span><span class="sxs-lookup"><span data-stu-id="df650-204">Define the content of your data</span></span>
* <span data-ttu-id="df650-205">如果您選取推送文字資料，請複製文字並貼到 [內容] 方塊。</span><span class="sxs-lookup"><span data-stu-id="df650-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="df650-206">如果您選取推送二進位或 base64 資料，請使用 [上傳您的檔案] 按鈕上傳您的檔案。</span><span class="sxs-lookup"><span data-stu-id="df650-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="df650-207">您可以根據使用者如何回應此活動的觸達意見反應，找出未來的活動對象。</span><span class="sxs-lookup"><span data-stu-id="df650-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="df650-208">選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。</span><span class="sxs-lookup"><span data-stu-id="df650-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="df650-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df650-209">See also</span></span>
* <span data-ttu-id="df650-210">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="df650-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="df650-211">磚的內容 (僅限 Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="df650-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="df650-213">定義磚的內容</span><span class="sxs-lookup"><span data-stu-id="df650-213">Define the content of your tile</span></span>
<span data-ttu-id="df650-214">磚承載是在 Windows Phone 裝置上應用程式磚中顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="df650-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="df650-215">磚推送是適用於 Windows Phone 之原生推送的 Microsoft 推播通知服務 (MPNS) 版本。</span><span class="sxs-lookup"><span data-stu-id="df650-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="df650-216">磚推送類型是唯一沒有回應的推播類型，因此無法依據磚推播活動的結果建置未來活動的對象。</span><span class="sxs-lookup"><span data-stu-id="df650-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="df650-217">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df650-217">See also</span></span>
* <span data-ttu-id="df650-218">[API 文件 - 觸達 API - 原生推送][Link 4]</span><span class="sxs-lookup"><span data-stu-id="df650-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

