---
title: "Azure Mobile Engagement 使用者介面 - 觸達活動"
description: "了解如何使用 Azure Mobile Engagement 建立和管理推播通知活動。"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="80472-103">如何建立和管理推播通知活動。</span><span class="sxs-lookup"><span data-stu-id="80472-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="80472-104">您可以使用 UI 的 [觸達] 區段，提供傳送推播通知所需的所有資訊，建立具有複雜公式的新推播活動。</span><span class="sxs-lookup"><span data-stu-id="80472-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="80472-105">觸達活動的選項根據四種活動類型而有所不同：通知、投票、資料推送和磚 (僅 Windows Phone)。</span><span class="sxs-lookup"><span data-stu-id="80472-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="80472-106">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-106">Option Applies to:</span></span>
* <span data-ttu-id="80472-107">語言：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-108">活動：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-109">通知：通知、投票</span><span class="sxs-lookup"><span data-stu-id="80472-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="80472-110">內容：每種活動類型都不同</span><span class="sxs-lookup"><span data-stu-id="80472-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="80472-111">對象：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-112">時間範圍：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="80472-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="80472-113">測試：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="80472-115">語言</span><span class="sxs-lookup"><span data-stu-id="80472-115">Languages</span></span>
<span data-ttu-id="80472-116">您可以使用 [語言] 下拉式功能表，將不同版本的推播傳送至設定使用不同語言的裝置。</span><span class="sxs-lookup"><span data-stu-id="80472-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="80472-117">無論裝置設定使用的語言為何，所有裝置預設都會收到相同的推播。</span><span class="sxs-lookup"><span data-stu-id="80472-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="80472-118">將裝置設定使用不同語言的使用者會收到預設語言版本的推播。</span><span class="sxs-lookup"><span data-stu-id="80472-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="80472-119">大部分的推播活動選項都可讓您針對每個額外選取的其他語言，來指定不同的內容。</span><span class="sxs-lookup"><span data-stu-id="80472-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="80472-121">語言差異適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-121">Language differences apply to:</span></span>
* <span data-ttu-id="80472-122">語言：除了預設語言之外，還可以選取其他指定的的語言</span><span class="sxs-lookup"><span data-stu-id="80472-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="80472-123">活動：所有語言都相同</span><span class="sxs-lookup"><span data-stu-id="80472-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="80472-124">通知：不只預設語言，可針對個別語言來指定</span><span class="sxs-lookup"><span data-stu-id="80472-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="80472-125">內容：不只預設語言，可針對個別語言來指定</span><span class="sxs-lookup"><span data-stu-id="80472-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="80472-126">對象：可根據個別的語言準則來篩選</span><span class="sxs-lookup"><span data-stu-id="80472-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="80472-127">時間範圍：所有語言都相同</span><span class="sxs-lookup"><span data-stu-id="80472-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="80472-128">測試：一次可以傳送給一種語言</span><span class="sxs-lookup"><span data-stu-id="80472-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="80472-129">支援的語言：</span><span class="sxs-lookup"><span data-stu-id="80472-129">Supported Languages:</span></span>
* <span data-ttu-id="80472-130">阿拉伯文 (ar)</span><span class="sxs-lookup"><span data-stu-id="80472-130">Arabic (ar)</span></span> 
* <span data-ttu-id="80472-131">保加利亞文 (bg)</span><span class="sxs-lookup"><span data-stu-id="80472-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="80472-132">卡達隆尼亞文 (ca)</span><span class="sxs-lookup"><span data-stu-id="80472-132">Catalan (ca)</span></span> 
* <span data-ttu-id="80472-133">中文 (zh)</span><span class="sxs-lookup"><span data-stu-id="80472-133">Chinese (zh)</span></span> 
* <span data-ttu-id="80472-134">克羅埃西亞文 (hr)</span><span class="sxs-lookup"><span data-stu-id="80472-134">Croatian (hr)</span></span> 
* <span data-ttu-id="80472-135">捷克文 (cs)</span><span class="sxs-lookup"><span data-stu-id="80472-135">Czech (cs)</span></span> 
* <span data-ttu-id="80472-136">丹麥文 (da)</span><span class="sxs-lookup"><span data-stu-id="80472-136">Danish (da)</span></span> 
* <span data-ttu-id="80472-137">荷蘭文 (nl)</span><span class="sxs-lookup"><span data-stu-id="80472-137">Dutch (nl)</span></span> 
* <span data-ttu-id="80472-138">英文 (en)</span><span class="sxs-lookup"><span data-stu-id="80472-138">English (en)</span></span> 
* <span data-ttu-id="80472-139">芬蘭文 (fi)</span><span class="sxs-lookup"><span data-stu-id="80472-139">Finnish (fi)</span></span> 
* <span data-ttu-id="80472-140">法文 (fr)</span><span class="sxs-lookup"><span data-stu-id="80472-140">French (fr)</span></span> 
* <span data-ttu-id="80472-141">德文 (de)</span><span class="sxs-lookup"><span data-stu-id="80472-141">German (de)</span></span> 
* <span data-ttu-id="80472-142">希臘文 (el)</span><span class="sxs-lookup"><span data-stu-id="80472-142">Greek (el)</span></span> 
* <span data-ttu-id="80472-143">希伯來文 (he)</span><span class="sxs-lookup"><span data-stu-id="80472-143">Hebrew (he)</span></span> 
* <span data-ttu-id="80472-144">印度文 (hi)</span><span class="sxs-lookup"><span data-stu-id="80472-144">Hindi (hi)</span></span> 
* <span data-ttu-id="80472-145">匈牙利文 (hu)</span><span class="sxs-lookup"><span data-stu-id="80472-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="80472-146">印尼文 (id)</span><span class="sxs-lookup"><span data-stu-id="80472-146">Indonesian (id)</span></span> 
* <span data-ttu-id="80472-147">義大利文 (it)</span><span class="sxs-lookup"><span data-stu-id="80472-147">Italian (it)</span></span> 
* <span data-ttu-id="80472-148">日文 (ja)</span><span class="sxs-lookup"><span data-stu-id="80472-148">Japanese (ja)</span></span> 
* <span data-ttu-id="80472-149">韓文 (ko)</span><span class="sxs-lookup"><span data-stu-id="80472-149">Korean (ko)</span></span> 
* <span data-ttu-id="80472-150">拉脫維亞文 (lv)</span><span class="sxs-lookup"><span data-stu-id="80472-150">Latvian (lv)</span></span> 
* <span data-ttu-id="80472-151">立陶宛文 (lt)</span><span class="sxs-lookup"><span data-stu-id="80472-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="80472-152">馬來文 (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="80472-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="80472-153">挪威文 (巴克摩) (nb)</span><span class="sxs-lookup"><span data-stu-id="80472-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="80472-154">波蘭文 (pl)</span><span class="sxs-lookup"><span data-stu-id="80472-154">Polish (pl)</span></span> 
* <span data-ttu-id="80472-155">葡萄牙文 (pt)</span><span class="sxs-lookup"><span data-stu-id="80472-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="80472-156">羅馬尼亞文 (ro)</span><span class="sxs-lookup"><span data-stu-id="80472-156">Romanian (ro)</span></span> 
* <span data-ttu-id="80472-157">俄文 (ru)</span><span class="sxs-lookup"><span data-stu-id="80472-157">Russian (ru)</span></span> 
* <span data-ttu-id="80472-158">塞爾維亞文 (sr)</span><span class="sxs-lookup"><span data-stu-id="80472-158">Serbian (sr)</span></span> 
* <span data-ttu-id="80472-159">斯洛伐克文 (sk)</span><span class="sxs-lookup"><span data-stu-id="80472-159">Slovak (sk)</span></span> 
* <span data-ttu-id="80472-160">斯洛維尼亞文 (sl)</span><span class="sxs-lookup"><span data-stu-id="80472-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="80472-161">西班牙文 (es)</span><span class="sxs-lookup"><span data-stu-id="80472-161">Spanish (es)</span></span> 
* <span data-ttu-id="80472-162">瑞典文 (sv)</span><span class="sxs-lookup"><span data-stu-id="80472-162">Swedish (sv)</span></span> 
* <span data-ttu-id="80472-163">塔加拉族文 (tl)</span><span class="sxs-lookup"><span data-stu-id="80472-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="80472-164">泰文 (th)</span><span class="sxs-lookup"><span data-stu-id="80472-164">Thai (th)</span></span> 
* <span data-ttu-id="80472-165">土耳其文 (tr)</span><span class="sxs-lookup"><span data-stu-id="80472-165">Turkish (tr)</span></span> 
* <span data-ttu-id="80472-166">烏克蘭文 (uk)</span><span class="sxs-lookup"><span data-stu-id="80472-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="80472-167">越南文 (vi)</span><span class="sxs-lookup"><span data-stu-id="80472-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="80472-168">活動</span><span class="sxs-lookup"><span data-stu-id="80472-168">Campaign</span></span>
<span data-ttu-id="80472-169">您可以使用 [活動] 區段設定活動的名稱和類別，如果您計劃忽略推播活動的對象區段，並改為透過觸達 API (以及使用低階推播 API 的部份元素) 傳送此活動，也可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="80472-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="80472-170">類別可以搭配自訂的通知範本一起使用，以便根據預先定義的設定控制應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="80472-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="80472-171">您可以透過觸達 API 取得一份您現有的「類別」清單。</span><span class="sxs-lookup"><span data-stu-id="80472-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="80472-172">如果您在觸達活動的 [活動] 區段中使用 [略過對象，推送將透過 API 傳送給使用者] 選項，活動將不會自動傳送，您必須以手動方式透過「觸達 API」傳送活動。</span><span class="sxs-lookup"><span data-stu-id="80472-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="80472-174">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-174">Option Applies to:</span></span>
* <span data-ttu-id="80472-175">名稱：全部</span><span class="sxs-lookup"><span data-stu-id="80472-175">Name:    All</span></span>
* <span data-ttu-id="80472-176">類別：通知、投票</span><span class="sxs-lookup"><span data-stu-id="80472-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="80472-177">略過對象，推播將透過 API 傳送給使用者：全部</span><span class="sxs-lookup"><span data-stu-id="80472-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="80472-178">通知</span><span class="sxs-lookup"><span data-stu-id="80472-178">Notification</span></span>
<span data-ttu-id="80472-179">您可以使用 [通知] 區段設定推播的基本設定，包括：推送的標題、訊息、應用程式內影像，或者它是否可關閉。</span><span class="sxs-lookup"><span data-stu-id="80472-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="80472-180">許多通知設定都和您使用的裝置平台有關。</span><span class="sxs-lookup"><span data-stu-id="80472-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="80472-181">您可以選取要在「應用程式內」或「應用程式外」或兩者傳送您的推播。</span><span class="sxs-lookup"><span data-stu-id="80472-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="80472-182">(請留意，對於「應用程式外」的推播，使用者可以在裝置的作業系統層級「選擇加入」或「選擇退出」，Azure Mobile Engagement 無法覆寫這項設定。</span><span class="sxs-lookup"><span data-stu-id="80472-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="80472-183">另請留意，觸達 API 可處理「應用程式內」和「應用程式外」推播。</span><span class="sxs-lookup"><span data-stu-id="80472-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="80472-184">推播 API 也可用來處理「應用程式外」推播)。推播可使用圖片或 HTML 內容加以自訂，包括連結到您應用程式之外，或連結到您應用程式內其他位置的深層連結 (需要 Android SDK 2.1.0 或更新版本的類別)。</span><span class="sxs-lookup"><span data-stu-id="80472-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="80472-185">您可以變更圖示或 iOS 徽章，並傳送文字或 Web 內容 (有 html 內容和 URL 連結的快顯，可連結到應用程式內部或外部的其他位置)。</span><span class="sxs-lookup"><span data-stu-id="80472-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="80472-186">您也可以使用推播讓 Android 裝置響鈴或震動。</span><span class="sxs-lookup"><span data-stu-id="80472-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="80472-187">(請留意，您需要在 Android 資訊清單檔案中有正確的 SDK 權限，才能讓裝置響鈴或震動)。Android 的「大型圖片」尺寸目前沒有任何業界標準，因為每個裝置使用不同的螢幕尺寸，不過 400x100 的圖片幾乎可在所有的螢幕尺寸上運作。</span><span class="sxs-lookup"><span data-stu-id="80472-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="80472-188">傳遞類型：</span><span class="sxs-lookup"><span data-stu-id="80472-188">Delivery Types:</span></span>
* <span data-ttu-id="80472-189">僅限應用程式外：當使用者不使用應用程式時，就會傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="80472-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="80472-190">僅限應用程式外的通知需要來自 Apple 或 Google 的憑證 (APN 或 GCM 憑證)。</span><span class="sxs-lookup"><span data-stu-id="80472-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="80472-191">僅限應用程式內：通知只會在應用程式執行時顯示。</span><span class="sxs-lookup"><span data-stu-id="80472-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="80472-192">通知使用 Capptain 傳遞系統觸達使用者。</span><span class="sxs-lookup"><span data-stu-id="80472-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="80472-193">您可以完全自訂推播的版面配置/顯示方式。</span><span class="sxs-lookup"><span data-stu-id="80472-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="80472-194">任何時間：無論應用程式是否執行，此選項可確保您傳送通知。</span><span class="sxs-lookup"><span data-stu-id="80472-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="80472-196">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-196">Option Applies to:</span></span>
* <span data-ttu-id="80472-197">通知：通知、投票</span><span class="sxs-lookup"><span data-stu-id="80472-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="80472-198">內容</span><span class="sxs-lookup"><span data-stu-id="80472-198">Content</span></span>
<span data-ttu-id="80472-199">您可以使用 [內容] 區段修改通知、投票、資料推送和磚 (僅限 Windows Phone) 的內容。</span><span class="sxs-lookup"><span data-stu-id="80472-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="80472-200">推播活動的 [內容] 設定與活動類型有關。</span><span class="sxs-lookup"><span data-stu-id="80472-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="80472-201">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80472-201">See also</span></span>
* <span data-ttu-id="80472-202">[UI 文件 - 觸達 - 推送內容][Link 29]</span><span class="sxs-lookup"><span data-stu-id="80472-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="80472-204">觀眾</span><span class="sxs-lookup"><span data-stu-id="80472-204">Audience</span></span>
<span data-ttu-id="80472-205">您可以使用 [對象] 區段定義標準的項目清單，或者根據自訂的準則，對活動設定限制。</span><span class="sxs-lookup"><span data-stu-id="80472-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="80472-206">限制對象的標準選項設定，可讓您只發送給新的或舊的使用者，或者只給原生的推播使用者。</span><span class="sxs-lookup"><span data-stu-id="80472-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="80472-207">您也可以設定配額，限制接收推播的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="80472-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="80472-208">您可以手動編輯運算式，如何篩選您的活動以包含一或多個選取使用者的準則。</span><span class="sxs-lookup"><span data-stu-id="80472-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="80472-209">您可以手動輸入對象運算式。</span><span class="sxs-lookup"><span data-stu-id="80472-209">You can manually type an audience expression.</span></span> <span data-ttu-id="80472-210">這類運算式必須明確定義準則之間的關係。</span><span class="sxs-lookup"><span data-stu-id="80472-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="80472-211">描述準則的識別項必須以大寫字母開頭，而且不能包含空格。</span><span class="sxs-lookup"><span data-stu-id="80472-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="80472-212">準則之間的關係可以使用 and、or、not 等運算子，以及「(」、「)」 來描述。</span><span class="sxs-lookup"><span data-stu-id="80472-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="80472-213">範例："Criterion1 or (Criterion1 and not Criterion2)"。</span><span class="sxs-lookup"><span data-stu-id="80472-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="80472-214">如果活動的對象很多，尤其是當您嘗試同時啟動多個活動時，伺服器端的目標掃描可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="80472-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="80472-215">可能的話，一次只啟動一個活動。</span><span class="sxs-lookup"><span data-stu-id="80472-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="80472-216">一次最多只啟動四個活動。</span><span class="sxs-lookup"><span data-stu-id="80472-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="80472-217">只推送給作用中使用者 (核取 [只吸引可使用原生推送觸達的使用者] 和 [只吸引作用中使用者] 方塊)，就只會掃描仍然安裝應用程式且使用它的使用者。</span><span class="sxs-lookup"><span data-stu-id="80472-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="80472-218">一旦定義您的對象之後，就可以使用模擬按鈕找出會收到此推播的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="80472-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="80472-219">這會計算此對象可能選出的已知使用者數目 (根據使用者的隨機取樣估計)。</span><span class="sxs-lookup"><span data-stu-id="80472-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="80472-220">請注意，已解除安裝應用程式的使用者也屬於這類對象，但無法觸達。</span><span class="sxs-lookup"><span data-stu-id="80472-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="80472-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80472-221">See also</span></span>
* <span data-ttu-id="80472-222">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="80472-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="80472-224">編輯運算式</span><span class="sxs-lookup"><span data-stu-id="80472-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="80472-226">限制對象選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="80472-227">只吸引部份使用者：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-228">只讓舊使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-229">只讓新使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-230">只讓閒置使用者參與：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="80472-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="80472-231">只讓作用中的使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="80472-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="80472-232">只吸引可使用原生推送觸達的使用者：宣告、投票</span><span class="sxs-lookup"><span data-stu-id="80472-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="80472-233">時間範圍</span><span class="sxs-lookup"><span data-stu-id="80472-233">Time Frame</span></span>
<span data-ttu-id="80472-234">您可以使用 [時間範圍] 區段設定推播傳送的時間，或者可以將時間範圍留空以便立即啟動活動。</span><span class="sxs-lookup"><span data-stu-id="80472-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="80472-235">請留意，使用使用者的時區來啟動活動，對於亞洲的使用者可能會比您預期的時間還早一天，因此請在世界上所有的時區都符合活動的時間範圍時，才一次傳送小型批次的推播。</span><span class="sxs-lookup"><span data-stu-id="80472-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="80472-236">使用使用者的時區也可能會造成活動延遲，因為必須先從使用者的電話取得時間才能啟動推送。</span><span class="sxs-lookup"><span data-stu-id="80472-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="80472-237">沒有結束日期的活動可能會在本機快取推送，甚至在您手動完成活動之後，仍然繼續顯示推送。</span><span class="sxs-lookup"><span data-stu-id="80472-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="80472-238">若要避免發生這個狀況，請為活動設定確切的結束時間。</span><span class="sxs-lookup"><span data-stu-id="80472-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="80472-239">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80472-239">See also</span></span>
* <span data-ttu-id="80472-240">[觸達 - 作法 – 排程][Link 3]</span><span class="sxs-lookup"><span data-stu-id="80472-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="80472-242">設定適用範圍：</span><span class="sxs-lookup"><span data-stu-id="80472-242">Settings Apply to:</span></span>
* <span data-ttu-id="80472-243">時間範圍：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="80472-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="80472-244">測試</span><span class="sxs-lookup"><span data-stu-id="80472-244">Test</span></span>
<span data-ttu-id="80472-245">儲存活動之前，您可以使用 [測試] 區段將此推播傳送到您自己的測試裝置。</span><span class="sxs-lookup"><span data-stu-id="80472-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="80472-246">如果您為此活動設定任何自訂語言，可以使用每個語言測試推播。</span><span class="sxs-lookup"><span data-stu-id="80472-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="80472-247">您可以從 [我的帳戶] 設定測試裝置。</span><span class="sxs-lookup"><span data-stu-id="80472-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="80472-248">當您使用按鈕來「測試」推送時，不會記錄任何伺服器端的資料，只會記錄實際推送活動的資料。</span><span class="sxs-lookup"><span data-stu-id="80472-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="80472-249">另請參閱</span><span class="sxs-lookup"><span data-stu-id="80472-249">See also</span></span>
* <span data-ttu-id="80472-250">[UI 文件 - 我的帳戶][Link 14]</span><span class="sxs-lookup"><span data-stu-id="80472-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

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

