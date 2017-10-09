---
title: "aaaAzure Mobile Engagement 使用者介面為連線到準則"
description: "了解如何 toouse 目標準則 toosend 推送活動 tooa 選取您的使用者使用 Azure Mobile Engagement 的子集"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="6fa1a-103">Toouse 目標準則 toosend 推送活動 tooa 如何選取您的使用者子集</span><span class="sxs-lookup"><span data-stu-id="6fa1a-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="6fa1a-104">目標觀眾使用 hello 「 新準則 」 按鈕的特定準則是其中一個 hello 最強大的概念 Azure Mobile Engagement 可協助您傳送相關推播 hello 客戶會回應的濫發 everyone tooinstead 的通知。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="6fa1a-105">您可以限制觀眾根據標準的準則，並模擬推播通知 toodetermine 很多人會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="6fa1a-106">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-106">**See also:**</span></span>

* <span data-ttu-id="6fa1a-107">[UI 文件 - 觸達 - 新的推播活動][Link 27]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="6fa1a-108">對象準則可以包括：</span><span class="sxs-lookup"><span data-stu-id="6fa1a-108">Audience criteria can include:</span></span>
* <span data-ttu-id="6fa1a-109">* * Technicals: * * 您可鎖定目標根據的 hello hello 分析和監視章節中可以看到相同的技術資訊。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="6fa1a-110">**另請參閱：** [UI 文件 - 分析][Link 15]、[UI 文件 - 監視器][Link 16]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="6fa1a-111">**位置：**應用程式，使用 「 即時位置回報 「 地理圍欄可作為準則 tootarget 從 hello GPS 位置的對象的地理位置。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="6fa1a-112">「 延遲區域位置報告 」 呼叫也會使用的 tootarget 從 hello 手機位置的對象 （「 即時位置回報 」 和 「 延遲區域位置回報 」 必須從啟動 hello SDK）。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="6fa1a-113">**另請參閱：** [SDK 文件 - iOS - 整合][Link 5]、[SDK 文件 - Android - 整合][Link 5]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="6fa1a-114">**觸達意見反應：** 您可以根據他們上一個透過觸達意見反應的通知、投票和資料推送的觸達意見反應來選擇目標對象。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="6fa1a-115">這可讓您 toobetter 目標觀眾兩個或三個到達您的行銷活動之後無法 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="6fa1a-116">它也可以用出使用者已經收到一則通知類似內容，藉由設定活動 tooNOT toofilter 傳送 toousers 已經已收到特定的上一個活動。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="6fa1a-117">您甚至可以排除包含特定有效活動的使用者收到新的推播。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="6fa1a-118">**另請參閱：** [UI 文件 - 觸達 - 推播內容][Link 29]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="6fa1a-119">**安裝追蹤：** 您可以追蹤根據使用者安裝您應用程式之位置所建立的資訊。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="6fa1a-120">**另請參閱：** [UI 文件 - 設定][Link 20]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="6fa1a-121">**使用者設定檔：**您可以根據標準使用者資訊的目標，您可以根據您所建立的 hello 自訂的應用程式資訊的目標。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="6fa1a-122">這包括使用者目前登入而回答您要求其相關的 tooset hello 應用程式本身而不是只如何它們所作的反應 tooprevious 活動中的特定問題的使用者。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="6fa1a-123">所有為您應用程式定義的應用程式資訊都顯示在這個清單。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="6fa1a-124">區隔：您也可以根據依特定使用者行為 (包含多個準則) 建立的區隔來選擇目標。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="6fa1a-125">所有為您應用程式定義的區隔都顯示在這個清單。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="6fa1a-126">**另請參閱：** [UI 文件 -區隔][Link 18]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="6fa1a-127">**應用程式資訊：**可以從 [設定] tootrack 使用者行為建立自訂應用程式資訊標記。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="6fa1a-128">**另請參閱：** [UI 文件 - 設定][Link 20]</span><span class="sxs-lookup"><span data-stu-id="6fa1a-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="6fa1a-129">範例：</span><span class="sxs-lookup"><span data-stu-id="6fa1a-129">Example:</span></span>
<span data-ttu-id="6fa1a-130">如果您想 toopush 公告只有 toohello 子集使用者執行應用程式內購買動作。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="6fa1a-131">移 tooyour 應用程式設定頁面上，選取 hello"應用程式資訊 功能表，然後選取 新應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="6fa1a-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="6fa1a-132">註冊一個稱為 "inAppPurchase" 的新布林值應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="6fa1a-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="6fa1a-133">讓您設定此應用程式資訊的應用程式太"，則為 true 」 時 hello 使用者成功執行應用程式內購買 (使用 hello sendAppInfo (「 inAppPurchase"，...) 函式)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="6fa1a-134">如果您不想 toodo 這從您的應用程式，您可以從您的後端執行使用 hello 裝置 API）</span><span class="sxs-lookup"><span data-stu-id="6fa1a-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="6fa1a-135">然後，您只需要您的通知，限制您的觀眾 toousers 具有"inAppPurchase"的準則設定太 」 為 true 」 toocreate）</span><span class="sxs-lookup"><span data-stu-id="6fa1a-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="6fa1a-136">目標應用程式資訊標記以外的準則為根據需要 Azure Mobile Engagement toogather 資訊從您的使用者裝置，才會傳送 hello 推入，並可能會導致延遲。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="6fa1a-137">複雜的推送設定選項 (例如更新徽章) 可能也會延遲推送。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="6fa1a-138">使用 hello 推送 API 中的 「 一次完成 「 活動是 hello 絕對最快推入的方法在 Azure Mobile Engagement 中。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="6fa1a-139">使用應用程式資訊標記為推入準則觸達活動 （是使用從 hello 觸達 API 或 hello UI） 是 hello 下一個最快的方法，因為應用程式資訊標記會儲存在 hello 伺服器端上。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="6fa1a-140">使用其他目標條件的推播宣傳活動為 hello 最有彈性，但最慢的推入方法，因為 Azure Mobile Engagement tooquery hello 裝置順序 toosend hello 促銷活動中。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="6fa1a-142">準則選項適用範圍：</span><span class="sxs-lookup"><span data-stu-id="6fa1a-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="6fa1a-143">**技術**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-143">**Technicals**</span></span>     
* <span data-ttu-id="6fa1a-144">韌體名稱：韌體名稱</span><span class="sxs-lookup"><span data-stu-id="6fa1a-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="6fa1a-145">韌體版本：韌體版本</span><span class="sxs-lookup"><span data-stu-id="6fa1a-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="6fa1a-146">裝置型號：裝置型號</span><span class="sxs-lookup"><span data-stu-id="6fa1a-146">Device model:    Device model</span></span>
* <span data-ttu-id="6fa1a-147">裝置製造商：裝置製造商</span><span class="sxs-lookup"><span data-stu-id="6fa1a-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="6fa1a-148">應用程式版本：應用程式版本</span><span class="sxs-lookup"><span data-stu-id="6fa1a-148">Application version:    Application version</span></span>
* <span data-ttu-id="6fa1a-149">電信業者名稱：電信業者名稱、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="6fa1a-150">電信業者國家/地區：電信業者國家/地區、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="6fa1a-151">網路類型：網路類型</span><span class="sxs-lookup"><span data-stu-id="6fa1a-151">Network type:    Network type</span></span>
* <span data-ttu-id="6fa1a-152">地區設定：地區設定</span><span class="sxs-lookup"><span data-stu-id="6fa1a-152">Locale:    Locale</span></span>
* <span data-ttu-id="6fa1a-153">螢幕大小：螢幕大小</span><span class="sxs-lookup"><span data-stu-id="6fa1a-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="6fa1a-154">**位置**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-154">**Location**</span></span>      
* <span data-ttu-id="6fa1a-155">上一個已知區域：國家/地區、區域、位置</span><span class="sxs-lookup"><span data-stu-id="6fa1a-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="6fa1a-156">即時地理柵欄：POI 清單 (名稱、動作)、圓形 POI (名稱、緯度、經度、以公尺為單位的半徑)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="6fa1a-157">**觸達意見反應**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-157">**Reach feedback**</span></span>     
* <span data-ttu-id="6fa1a-158">通知意見反應：通知、意見反應</span><span class="sxs-lookup"><span data-stu-id="6fa1a-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="6fa1a-159">投票意見反應：投票、意見反應</span><span class="sxs-lookup"><span data-stu-id="6fa1a-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="6fa1a-160">投票答案意見反應：投票答案意見反應、問題、選項</span><span class="sxs-lookup"><span data-stu-id="6fa1a-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="6fa1a-161">資料推送意見反應：資料推送、意見反應</span><span class="sxs-lookup"><span data-stu-id="6fa1a-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="6fa1a-162">**安裝追蹤**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-162">**Install Tracking**</span></span>     
* <span data-ttu-id="6fa1a-163">市集：市集、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="6fa1a-164">來源：來源</span><span class="sxs-lookup"><span data-stu-id="6fa1a-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="6fa1a-165">**使用者個人檔案**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-165">**User profile**</span></span>     
* <span data-ttu-id="6fa1a-166">性別：男性或女性、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="6fa1a-167">生日：運算子、日期、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="6fa1a-168">選擇加入：true 或 false、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="6fa1a-169">**應用程式資訊**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-169">**App Info**</span></span>      
* <span data-ttu-id="6fa1a-170">字串：字串、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-170">String:    String, undefined</span></span>
* <span data-ttu-id="6fa1a-171">日期：運算子、日期、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="6fa1a-172">整數：運算子、數字、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="6fa1a-173">布林值：true 或 false、未定義</span><span class="sxs-lookup"><span data-stu-id="6fa1a-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="6fa1a-174">**區隔**</span><span class="sxs-lookup"><span data-stu-id="6fa1a-174">**Segment**</span></span>    
* <span data-ttu-id="6fa1a-175">區隔的名稱 (從下拉式清單)、排除 (不屬於此區隔的目標使用者)。</span><span class="sxs-lookup"><span data-stu-id="6fa1a-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

