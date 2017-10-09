---
title: "aaaAzure Mobile Engagement 疑難排解指南-SDK"
description: "Azure Mobile Engagement 中 SDK 整合的疑難排解"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="5a7a3-103">SDK 整合問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="5a7a3-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="5a7a3-104">hello 以下是可能的問題，您可能會遇到與 Azure Mobile Engagement 如何整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="5a7a3-105">因為您應用程式的另一個區域中發生失敗而發現的 SDK 問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="5a7a3-106">問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-106">Issue</span></span>
* <span data-ttu-id="5a7a3-107">UI 資料收集失敗 (在分析、監視、分割或儀表板中)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="5a7a3-108">推送失敗 (推送在應用程式內或應用程式外無法運作，或在兩個情況下都無法運作)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="5a7a3-109">進階功能失敗 (追蹤、地理位置或平台特定的推送無法運作)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="5a7a3-110">API 失敗 (API 經常以無訊息模式失敗，沒有錯誤訊息)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="5a7a3-111">服務失敗 (所有 Azure Mobile Engagement 都無法在您的應用程式上運作)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="5a7a3-112">原因</span><span class="sxs-lookup"><span data-stu-id="5a7a3-112">Causes</span></span>
* <span data-ttu-id="5a7a3-113">大部分需要 toobe 解決 hello Azure Mobile Engagement SDK 的問題將會探索您的應用程式 （例如 UI 資料收集失敗、 推入失敗、 進階的功能失敗、 應用程式開發介面失敗、 應用程式損毀或明顯服務失敗中斷的狀況）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="5a7a3-114">如果特定功能的 Azure Mobile Engagement 具有永遠不會在您的應用程式之前，您需要 toocomplete hello 整合。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="5a7a3-115">如果 Azure Mobile Engagement 的特定功能運作，而停止，您可能需要以 hello Azure Mobile Engagement SDK tooupgrade toohello 最後一個版本。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="5a7a3-116">請記住每個平台支援的 Azure Mobile Engagement （Android、 iOS、 Windows 和 Windows Phone） hello Azure Mobile Engagement SDK 不同版本。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="5a7a3-117">SDK 整合</span><span class="sxs-lookup"><span data-stu-id="5a7a3-117">SDK Integration</span></span>
* <span data-ttu-id="5a7a3-118">Azure Mobile Engagement 未正確整合在 SDK 中 (分析)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="5a7a3-119">Reach 未正確整合在 SDK 中 (應用程式內推送和應用程式外推送)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="5a7a3-120">憑證已過期或 PROD 與 DEV 不正確 (僅限 iOS)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="5a7a3-121">GCM 或 ADM 未正確整合在 SDK 中 (僅限 Android - 服務特定推送)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="5a7a3-122">追蹤未正確整合在 SDK 中 (安裝存放區追蹤)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="5a7a3-123">延遲位置或 GPS 位置未正確整合在 SDK 中 (依地理位置設定目標)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="5a7a3-124">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="5a7a3-124">**See also:**</span></span>

* <span data-ttu-id="5a7a3-125">[SDK 文件 - 整合指南][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="5a7a3-126">[疑難排解指南 - 推送][Link 23]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="5a7a3-127">SDK 升級</span><span class="sxs-lookup"><span data-stu-id="5a7a3-127">SDK Upgrade</span></span>
* <span data-ttu-id="5a7a3-128">需要 tooupgrade SDK tooresolve 問題與舊版本的 hello SDK （通常相關的 toonewer hello 裝置作業系統版本）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="5a7a3-129">從您的裝置解除安裝所有舊版的應用程式，並重新安裝應用程式的 hello 最新版本，hello 重新註冊您的裝置識別碼，從您的裝置正在使用您的應用程式的 hello 最新版本的 hello Azure Mobile Engagement UI tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="5a7a3-130">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="5a7a3-130">**See also:**</span></span>

* [<span data-ttu-id="5a7a3-131">SDK 文件 - 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5a7a3-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="5a7a3-132">SDK 文件 - 升級指南</span><span class="sxs-lookup"><span data-stu-id="5a7a3-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="5a7a3-133">SDK 其他問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-133">SDK Other</span></span>
* <span data-ttu-id="5a7a3-134">在應用程式資訊清單"AndroidManifest.xml 」 的錯誤可能會導致 Azure Mobile Engagement toowork (僅 Android)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="5a7a3-135">常見的問題與 SDK 整合及應用程式開發介面使用方式為 tooconfuse hello SDK 金鑰和 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="5a7a3-136">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="5a7a3-136">**See also:**</span></span>

* <span data-ttu-id="5a7a3-137">[概念 - 詞彙][Link 6]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="5a7a3-138">進階編碼問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="5a7a3-139">問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-139">Issue</span></span>
* <span data-ttu-id="5a7a3-140">平台特定程式碼不是直接相關的 tooAzure Mobile Engagement 進行 iOS、 Android 和 Windows Phone，可能會導致某些問題。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="5a7a3-141">原因</span><span class="sxs-lookup"><span data-stu-id="5a7a3-141">Causes</span></span>
* <span data-ttu-id="5a7a3-142">有許多進階與 Azure Mobile Engagement 的撰寫問題的原因藉由撰寫不正確的平台特定程式碼不是直接相關的 tooAzure Mobile Engagement。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="5a7a3-143">您將需要 tooconsult 文件特定 toohello 平台您正在開發此外 tooAzure Mobile Engagement 文件 （Android、 iOS、 Web、 Windows 和 Windows Phone）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="5a7a3-144">未正確設定 「 類別 」，可避免從內部或外部 hello 應用程式 (僅 Android) 的通知 tooanother 位置連結。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="5a7a3-145">未設定太 「 選用 」 在您的 iOS 程式碼，便會顯示 「 找不到錯誤的符號""UIKit.framework 」 及 （或較舊的 iOS 裝置 (僅限 iOS) 上發生當機)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="5a7a3-146">過期的憑證或未正確使用 hello 開發人員或生產環境版本 hello cert，原因發送問題 (僅限 iOS)。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="5a7a3-147">有一些限制固有 tooa 平台的 Azure Mobile Engagement 無法控制 （例如如何 hello system center 的運作方式的應用程式外推播通知在 Android 和 iOS）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="5a7a3-148">Azure Mobile Engagement 發行參考使用的 Azure Mobile Engagement 適用於 iOS 和 Android 的 hello 內部套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="5a7a3-149">請記住，某些功能的 Azure Mobile Engagement 是特定 toohello 平台 （Android、 iOS、 Web、 Windows 和 Windows Phone）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="5a7a3-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5a7a3-150">See also</span></span>
* <span data-ttu-id="5a7a3-151">[疑難排解指南 - 推送][Link 23]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="5a7a3-152">[SDK 文件 - 版本資訊][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="5a7a3-153">[SDK 文件 - 升級指南][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="5a7a3-154">應用程式當機</span><span class="sxs-lookup"><span data-stu-id="5a7a3-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="5a7a3-155">問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-155">Issue</span></span>
* <span data-ttu-id="5a7a3-156">應用程式損毀 hello 結束使用者的裝置上。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="5a7a3-157">原因</span><span class="sxs-lookup"><span data-stu-id="5a7a3-157">Causes</span></span>
* <span data-ttu-id="5a7a3-158">可以在 hello 檢視損毀資訊*分析 UI*或 hello*分析 API*</span><span class="sxs-lookup"><span data-stu-id="5a7a3-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="5a7a3-159">您可以找到 hello 測試裝置的裝置識別碼，並採取 hello 相同的動作，導致您的應用程式 toocrash 的終端使用者 toohelp 識別 hello 程式損毀原因。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="5a7a3-160">以 hello Azure Mobile Engagement SDK 的已知的問題會造成應用程式 toocrash 有時被解決方法是升級 toohello hello SDK 最新版本。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="5a7a3-161">調查損毀時，請確定您的平台有關 toocheck hello 版本資訊。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="5a7a3-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5a7a3-162">See also</span></span>
* <span data-ttu-id="5a7a3-163">[SDK 文件 - 版本資訊][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="5a7a3-164">[SDK 文件 - 升級指南][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5a7a3-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="5a7a3-165">應用程式商店上傳失敗</span><span class="sxs-lookup"><span data-stu-id="5a7a3-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="5a7a3-166">問題</span><span class="sxs-lookup"><span data-stu-id="5a7a3-166">Issue</span></span>
* <span data-ttu-id="5a7a3-167">錯誤相關的應用程式 tooApple、 Google、 或 hello Windows 應用程式存放區的 toouploading hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="5a7a3-168">原因</span><span class="sxs-lookup"><span data-stu-id="5a7a3-168">Causes</span></span>
* <span data-ttu-id="5a7a3-169">應用程式會將有時封鎖應用程式已啟用特定功能 （例如 hello Apple Store 防止 IDFV 的 hello 存放區中的應用程式中的 hello 利用並 hello GooglePlay 存放區可防止 hello 共用應用程式之間的應用程式資訊）。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="5a7a3-170">請確定您檢查 hello 版本資訊有關您的平台和目前 hello SDK 版本，如果您無法上傳應用程式 toohello 市集。</span><span class="sxs-lookup"><span data-stu-id="5a7a3-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

