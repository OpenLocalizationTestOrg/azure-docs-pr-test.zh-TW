---
title: "aaaAzure Mobile Engagement 使用者介面為連線到活動"
description: "Laern 如何 toocreate 和管理使用 Azure Mobile Engagement 的推送通知活動"
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="b7004-103">如何 toocreate 和管理推送通知活動</span><span class="sxs-lookup"><span data-stu-id="b7004-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="b7004-104">您可以使用包含複雜公式的 hello hello UI toocreate 新的推播宣傳活動觸達一節提供您需要 toosend 推播通知的所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="b7004-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="b7004-105">hello 選項的推播宣傳活動會稍微不同視 hello 四個活動類型而定： 宣告、 投票、 資料推入和磚 (僅限 Windows Phone)。</span><span class="sxs-lookup"><span data-stu-id="b7004-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="b7004-106">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-106">Option Applies to:</span></span>
* <span data-ttu-id="b7004-107">語言：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-108">活動：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-109">通知：通知、投票</span><span class="sxs-lookup"><span data-stu-id="b7004-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="b7004-110">內容：每種活動類型都不同</span><span class="sxs-lookup"><span data-stu-id="b7004-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="b7004-111">對象：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-112">時間範圍：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="b7004-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b7004-113">測試：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="b7004-115">語言</span><span class="sxs-lookup"><span data-stu-id="b7004-115">Languages</span></span>
<span data-ttu-id="b7004-116">您可以使用 hello 語言下拉式清單功能表 toosend 設定 toouse 不同語言程式推入 toodevices 的不同版本。</span><span class="sxs-lookup"><span data-stu-id="b7004-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="b7004-117">根據預設，所有的裝置將會收到的 hello 相同不論何種語言設定 toouse 推入。</span><span class="sxs-lookup"><span data-stu-id="b7004-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="b7004-118">使用其裝置設定 tooa 不同語言的使用者會收到 hello hello 推入預設語言版本。</span><span class="sxs-lookup"><span data-stu-id="b7004-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="b7004-119">Hello 推送活動選項中有許多可讓您 toospecify 替代內容為每個您所選取的 hello 其他語言。</span><span class="sxs-lookup"><span data-stu-id="b7004-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="b7004-121">語言差異適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-121">Language differences apply to:</span></span>
* <span data-ttu-id="b7004-122">語言： 可能在加法 toohello 預設語言中選取唯一的語言</span><span class="sxs-lookup"><span data-stu-id="b7004-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="b7004-123">活動：所有語言都相同</span><span class="sxs-lookup"><span data-stu-id="b7004-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="b7004-124">通知： 唯一的每一種語言此外 toohello 預設語言</span><span class="sxs-lookup"><span data-stu-id="b7004-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="b7004-125">內容： 唯一的每一種語言此外 toohello 預設語言</span><span class="sxs-lookup"><span data-stu-id="b7004-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="b7004-126">對象：可根據個別的語言準則來篩選</span><span class="sxs-lookup"><span data-stu-id="b7004-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="b7004-127">時間範圍：所有語言都相同</span><span class="sxs-lookup"><span data-stu-id="b7004-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="b7004-128">測試： 可能會傳送 tooeach 語言一次</span><span class="sxs-lookup"><span data-stu-id="b7004-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="b7004-129">支援的語言：</span><span class="sxs-lookup"><span data-stu-id="b7004-129">Supported Languages:</span></span>
* <span data-ttu-id="b7004-130">阿拉伯文 (ar)</span><span class="sxs-lookup"><span data-stu-id="b7004-130">Arabic (ar)</span></span> 
* <span data-ttu-id="b7004-131">保加利亞文 (bg)</span><span class="sxs-lookup"><span data-stu-id="b7004-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="b7004-132">卡達隆尼亞文 (ca)</span><span class="sxs-lookup"><span data-stu-id="b7004-132">Catalan (ca)</span></span> 
* <span data-ttu-id="b7004-133">中文 (zh)</span><span class="sxs-lookup"><span data-stu-id="b7004-133">Chinese (zh)</span></span> 
* <span data-ttu-id="b7004-134">克羅埃西亞文 (hr)</span><span class="sxs-lookup"><span data-stu-id="b7004-134">Croatian (hr)</span></span> 
* <span data-ttu-id="b7004-135">捷克文 (cs)</span><span class="sxs-lookup"><span data-stu-id="b7004-135">Czech (cs)</span></span> 
* <span data-ttu-id="b7004-136">丹麥文 (da)</span><span class="sxs-lookup"><span data-stu-id="b7004-136">Danish (da)</span></span> 
* <span data-ttu-id="b7004-137">荷蘭文 (nl)</span><span class="sxs-lookup"><span data-stu-id="b7004-137">Dutch (nl)</span></span> 
* <span data-ttu-id="b7004-138">英文 (en)</span><span class="sxs-lookup"><span data-stu-id="b7004-138">English (en)</span></span> 
* <span data-ttu-id="b7004-139">芬蘭文 (fi)</span><span class="sxs-lookup"><span data-stu-id="b7004-139">Finnish (fi)</span></span> 
* <span data-ttu-id="b7004-140">法文 (fr)</span><span class="sxs-lookup"><span data-stu-id="b7004-140">French (fr)</span></span> 
* <span data-ttu-id="b7004-141">德文 (de)</span><span class="sxs-lookup"><span data-stu-id="b7004-141">German (de)</span></span> 
* <span data-ttu-id="b7004-142">希臘文 (el)</span><span class="sxs-lookup"><span data-stu-id="b7004-142">Greek (el)</span></span> 
* <span data-ttu-id="b7004-143">希伯來文 (he)</span><span class="sxs-lookup"><span data-stu-id="b7004-143">Hebrew (he)</span></span> 
* <span data-ttu-id="b7004-144">印度文 (hi)</span><span class="sxs-lookup"><span data-stu-id="b7004-144">Hindi (hi)</span></span> 
* <span data-ttu-id="b7004-145">匈牙利文 (hu)</span><span class="sxs-lookup"><span data-stu-id="b7004-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="b7004-146">印尼文 (id)</span><span class="sxs-lookup"><span data-stu-id="b7004-146">Indonesian (id)</span></span> 
* <span data-ttu-id="b7004-147">義大利文 (it)</span><span class="sxs-lookup"><span data-stu-id="b7004-147">Italian (it)</span></span> 
* <span data-ttu-id="b7004-148">日文 (ja)</span><span class="sxs-lookup"><span data-stu-id="b7004-148">Japanese (ja)</span></span> 
* <span data-ttu-id="b7004-149">韓文 (ko)</span><span class="sxs-lookup"><span data-stu-id="b7004-149">Korean (ko)</span></span> 
* <span data-ttu-id="b7004-150">拉脫維亞文 (lv)</span><span class="sxs-lookup"><span data-stu-id="b7004-150">Latvian (lv)</span></span> 
* <span data-ttu-id="b7004-151">立陶宛文 (lt)</span><span class="sxs-lookup"><span data-stu-id="b7004-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="b7004-152">馬來文 (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="b7004-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="b7004-153">挪威文 (巴克摩) (nb)</span><span class="sxs-lookup"><span data-stu-id="b7004-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="b7004-154">波蘭文 (pl)</span><span class="sxs-lookup"><span data-stu-id="b7004-154">Polish (pl)</span></span> 
* <span data-ttu-id="b7004-155">葡萄牙文 (pt)</span><span class="sxs-lookup"><span data-stu-id="b7004-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="b7004-156">羅馬尼亞文 (ro)</span><span class="sxs-lookup"><span data-stu-id="b7004-156">Romanian (ro)</span></span> 
* <span data-ttu-id="b7004-157">俄文 (ru)</span><span class="sxs-lookup"><span data-stu-id="b7004-157">Russian (ru)</span></span> 
* <span data-ttu-id="b7004-158">塞爾維亞文 (sr)</span><span class="sxs-lookup"><span data-stu-id="b7004-158">Serbian (sr)</span></span> 
* <span data-ttu-id="b7004-159">斯洛伐克文 (sk)</span><span class="sxs-lookup"><span data-stu-id="b7004-159">Slovak (sk)</span></span> 
* <span data-ttu-id="b7004-160">斯洛維尼亞文 (sl)</span><span class="sxs-lookup"><span data-stu-id="b7004-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="b7004-161">西班牙文 (es)</span><span class="sxs-lookup"><span data-stu-id="b7004-161">Spanish (es)</span></span> 
* <span data-ttu-id="b7004-162">瑞典文 (sv)</span><span class="sxs-lookup"><span data-stu-id="b7004-162">Swedish (sv)</span></span> 
* <span data-ttu-id="b7004-163">塔加拉族文 (tl)</span><span class="sxs-lookup"><span data-stu-id="b7004-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="b7004-164">泰文 (th)</span><span class="sxs-lookup"><span data-stu-id="b7004-164">Thai (th)</span></span> 
* <span data-ttu-id="b7004-165">土耳其文 (tr)</span><span class="sxs-lookup"><span data-stu-id="b7004-165">Turkish (tr)</span></span> 
* <span data-ttu-id="b7004-166">烏克蘭文 (uk)</span><span class="sxs-lookup"><span data-stu-id="b7004-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="b7004-167">越南文 (vi)</span><span class="sxs-lookup"><span data-stu-id="b7004-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="b7004-168">活動</span><span class="sxs-lookup"><span data-stu-id="b7004-168">Campaign</span></span>
<span data-ttu-id="b7004-169">您可以使用 hello 活動區段 tooset hello 名稱，以及您的活動的類別以及您計劃的推播宣傳活動 tooignore hello 觀眾區段，並改為傳送 hello 觸達 API 透過此活動 （和 hello 低層級推送 API 的某些項目）。</span><span class="sxs-lookup"><span data-stu-id="b7004-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="b7004-170">類別可用於根據預先定義的設定自訂的通知範本 toocontrol 應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="b7004-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="b7004-171">您可以取得一份您現有 「 類別 」 透過 hello 觸達 API。</span><span class="sxs-lookup"><span data-stu-id="b7004-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="b7004-172">如果您使用 hello"忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers 」 選項 hello 「 活動 」 一節中的觸達活動，不會自動傳送 hello 行銷活動，您需要 toosend 它以手動方式透過 hello 觸達 API。</span><span class="sxs-lookup"><span data-stu-id="b7004-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="b7004-174">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-174">Option Applies to:</span></span>
* <span data-ttu-id="b7004-175">名稱：全部</span><span class="sxs-lookup"><span data-stu-id="b7004-175">Name:    All</span></span>
* <span data-ttu-id="b7004-176">類別：通知、投票</span><span class="sxs-lookup"><span data-stu-id="b7004-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="b7004-177">忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers： 所有</span><span class="sxs-lookup"><span data-stu-id="b7004-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="b7004-178">通知</span><span class="sxs-lookup"><span data-stu-id="b7004-178">Notification</span></span>
<span data-ttu-id="b7004-179">您可以使用 hello 通知區段 tooset 基本設定，您的推播包括： hello 標題的 hello 推入，hello 訊息，在應用程式映像，或者如果它是可解除。</span><span class="sxs-lookup"><span data-stu-id="b7004-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="b7004-180">通知的許多設定都是裝置的特定 toohello 平台，您。</span><span class="sxs-lookup"><span data-stu-id="b7004-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="b7004-181">您可以選取要在「應用程式內」或「應用程式外」或兩者傳送您的推播。</span><span class="sxs-lookup"><span data-stu-id="b7004-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="b7004-182">(請記住，使用者就可以 「 選擇加入 」 或 「 退出 」 的 「 從應用程式 」 在 hello 作業系統層級將推入至他們的裝置，而且 Azure Mobile Engagement 不會是能 toooverride 這項設定。</span><span class="sxs-lookup"><span data-stu-id="b7004-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="b7004-183">也請記住，hello 觸達 API 「 以應用程式 「 處理 」 應用程式超出"推播通知。</span><span class="sxs-lookup"><span data-stu-id="b7004-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="b7004-184">hello 推送 API 可以是使用的 toohandle 太推入 」 的應用程式超出"）。使用圖片或 HTML 內容，包括深層連結來連結您的應用程式或 tooanother 位置，在您的應用程式 （Android SDK 2.1.0 或更新版本所需的意圖類別） 之外，您可以自訂推播通知。</span><span class="sxs-lookup"><span data-stu-id="b7004-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="b7004-185">您可以變更 hello 圖示或 iOS 徽章和文字或 web 內容 （html 內容，URL 連結 tooanother 位置 hello 應用程式內外的快顯） 傳送。</span><span class="sxs-lookup"><span data-stu-id="b7004-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="b7004-186">您也可以使 Android 裝置響鈴或震動以 hello 推入。</span><span class="sxs-lookup"><span data-stu-id="b7004-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="b7004-187">（請記住，您將需要 hello 正確 Android SDK 權限資訊清單檔案 tooring 或震動裝置）。Android 的「大型圖片」尺寸目前沒有任何業界標準，因為每個裝置使用不同的螢幕尺寸，不過 400x100 的圖片幾乎可在所有的螢幕尺寸上運作。</span><span class="sxs-lookup"><span data-stu-id="b7004-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="b7004-188">傳遞類型：</span><span class="sxs-lookup"><span data-stu-id="b7004-188">Delivery Types:</span></span>
* <span data-ttu-id="b7004-189">不在應用程式只： hello 使用者不使用 hello 應用程式時，就會傳送 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="b7004-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="b7004-190">從應用程式僅通知的 hello 需要從 Apple 或 Google （APNS 或 GCM 憑證） 的憑證。</span><span class="sxs-lookup"><span data-stu-id="b7004-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="b7004-191">在應用程式只： 只有在執行 hello 應用程式時才出現 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="b7004-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="b7004-192">hello 通知使用 hello Capptain 傳送系統 tooreach hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b7004-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="b7004-193">您可以完全自訂 hello 配置/的視覺顯示發送。</span><span class="sxs-lookup"><span data-stu-id="b7004-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="b7004-194">任何時間： 此選項可確保您傳送的通知，或未執行其中一個 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7004-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="b7004-196">選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-196">Option Applies to:</span></span>
* <span data-ttu-id="b7004-197">通知：通知、投票</span><span class="sxs-lookup"><span data-stu-id="b7004-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="b7004-198">內容</span><span class="sxs-lookup"><span data-stu-id="b7004-198">Content</span></span>
<span data-ttu-id="b7004-199">您可以使用 hello 內容區段 toomodify hello 內容的宣告、 投票、 資料推播通知，以及磚 (僅限 Windows Phone)。</span><span class="sxs-lookup"><span data-stu-id="b7004-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="b7004-200">hello 內容設定的推送活動的是特定 toohello 活動類型。</span><span class="sxs-lookup"><span data-stu-id="b7004-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="b7004-201">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7004-201">See also</span></span>
* <span data-ttu-id="b7004-202">[UI 文件 - 觸達 - 推送內容][Link 29]</span><span class="sxs-lookup"><span data-stu-id="b7004-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="b7004-204">對象</span><span class="sxs-lookup"><span data-stu-id="b7004-204">Audience</span></span>
<span data-ttu-id="b7004-205">您的行銷活動根據自訂準則的限制，您可以使用 hello 觀眾區段 toodefine 標準的項目 toolimit 清單。</span><span class="sxs-lookup"><span data-stu-id="b7004-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="b7004-206">hello 組標準的選項 tooLimit 觀眾可讓您 toopush tooeither 新或舊的使用者或僅限原生推送使用者。</span><span class="sxs-lookup"><span data-stu-id="b7004-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="b7004-207">您也可以設定使用者接收 hello 推播配額 toolimit hello 數字。</span><span class="sxs-lookup"><span data-stu-id="b7004-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="b7004-208">您可以手動編輯 hello 運算式活動的方式篩選的 tooinclude 一或多個準則 tootarget 使用者。</span><span class="sxs-lookup"><span data-stu-id="b7004-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="b7004-209">您可以手動輸入對象運算式。</span><span class="sxs-lookup"><span data-stu-id="b7004-209">You can manually type an audience expression.</span></span> <span data-ttu-id="b7004-210">這類運算式必須明確地定義 hello 準則之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="b7004-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="b7004-211">描述準則的識別項必須以大寫字母開頭，而且不能包含空格。</span><span class="sxs-lookup"><span data-stu-id="b7004-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="b7004-212">可以使用描述 hello hello 準則之間的關聯性 'and'、 'or'、 'not' 運算子以及 '（'，'）'。</span><span class="sxs-lookup"><span data-stu-id="b7004-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="b7004-213">範例："Criterion1 or (Criterion1 and not Criterion2)"。</span><span class="sxs-lookup"><span data-stu-id="b7004-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="b7004-214">大型的對象，包含在活動中，與 hello 伺服器端為目標的掃描可能會降低，特別是當您嘗試 toostart 多個活動在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b7004-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="b7004-215">可能的話，一次只啟動一個活動。</span><span class="sxs-lookup"><span data-stu-id="b7004-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="b7004-216">在 hello 最多只能啟動四個活動一次。</span><span class="sxs-lookup"><span data-stu-id="b7004-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="b7004-217">推播 tooyour 作用中使用者 (核取方塊 」 僅連絡使用者可以使用原生推送連 」 和 「 僅連絡作用中的使用者 」)，因此只有您的使用者仍 hello 安裝的應用程式，並用它將需要 toobe 掃描。</span><span class="sxs-lookup"><span data-stu-id="b7004-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="b7004-218">一旦您的對象定義之後，您可以使用 hello 模擬按鈕 toofind 出多少使用者會收到此 Push。</span><span class="sxs-lookup"><span data-stu-id="b7004-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="b7004-219">這會計算 hello 可能目標 （這是根據使用者隨機取樣估計） 此對象的已知使用者數。</span><span class="sxs-lookup"><span data-stu-id="b7004-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="b7004-220">請注意，已解除安裝 hello 應用程式的使用者也是算是此受眾的一部分，但無法觸達。</span><span class="sxs-lookup"><span data-stu-id="b7004-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="b7004-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7004-221">See also</span></span>
* <span data-ttu-id="b7004-222">[UI 文件 - 觸達 - 新增推播準則][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b7004-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="b7004-224">編輯運算式</span><span class="sxs-lookup"><span data-stu-id="b7004-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="b7004-226">限制對象選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="b7004-227">只吸引部份使用者：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-228">只讓舊使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-229">只讓新使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-230">只讓閒置使用者參與：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="b7004-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b7004-231">只讓作用中的使用者參與：全部 (通知、投票、資料推送、圖格)</span><span class="sxs-lookup"><span data-stu-id="b7004-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b7004-232">只吸引可使用原生推送觸達的使用者：宣告、投票</span><span class="sxs-lookup"><span data-stu-id="b7004-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="b7004-233">時間範圍</span><span class="sxs-lookup"><span data-stu-id="b7004-233">Time Frame</span></span>
<span data-ttu-id="b7004-234">將傳送嗨推入，或您可以立即讓 hello 時段空白 toostart hello 活動時，您可以使用 hello 時段區段 tooset。</span><span class="sxs-lookup"><span data-stu-id="b7004-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="b7004-235">請記住，使用 hello 一向 time zone 可能 hello 活動一天開始早於您預期使用者在亞洲和傳送的推播通知一次 hello world 相符 hello 時間範圍內的時區設定您的活動時，才小批次。</span><span class="sxs-lookup"><span data-stu-id="b7004-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="b7004-236">使用 hello 畷樾簅 time zone 也可能導致延遲活動中因為它有 toorequest hello 時間，從 hello 電話才開始 hello 推入。</span><span class="sxs-lookup"><span data-stu-id="b7004-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="b7004-237">沒有結束日期的活動可能會在本機快取推送，甚至在您手動完成活動之後，仍然繼續顯示推送。</span><span class="sxs-lookup"><span data-stu-id="b7004-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="b7004-238">tooavoid 此行為的特定活動結束時間。</span><span class="sxs-lookup"><span data-stu-id="b7004-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b7004-239">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7004-239">See also</span></span>
* <span data-ttu-id="b7004-240">[觸達 - 作法 – 排程][Link 3]</span><span class="sxs-lookup"><span data-stu-id="b7004-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="b7004-242">設定適用範圍：</span><span class="sxs-lookup"><span data-stu-id="b7004-242">Settings Apply to:</span></span>
* <span data-ttu-id="b7004-243">時間範圍：通知、投票、圖格</span><span class="sxs-lookup"><span data-stu-id="b7004-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="b7004-244">測試</span><span class="sxs-lookup"><span data-stu-id="b7004-244">Test</span></span>
<span data-ttu-id="b7004-245">您可以使用 hello 測試區段 toosend 此 push tooyour 自己的測試裝置，才能儲存 hello 行銷活動。</span><span class="sxs-lookup"><span data-stu-id="b7004-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="b7004-246">如果您已設定任何自訂的支援語言的這個活動，您可以在每個語言中測試 hello 推入。</span><span class="sxs-lookup"><span data-stu-id="b7004-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="b7004-247">您可以從 [我的帳戶] 設定測試裝置。</span><span class="sxs-lookup"><span data-stu-id="b7004-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="b7004-248">當您使用 hello 按鈕時，會記錄資料的任何伺服器端太"test"推播通知，針對實際的推送活動只會記錄資料。</span><span class="sxs-lookup"><span data-stu-id="b7004-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b7004-249">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7004-249">See also</span></span>
* <span data-ttu-id="b7004-250">[UI 文件 - 我的帳戶][Link 14]</span><span class="sxs-lookup"><span data-stu-id="b7004-250">[UI Documentation - My Account][Link 14]</span></span>

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

