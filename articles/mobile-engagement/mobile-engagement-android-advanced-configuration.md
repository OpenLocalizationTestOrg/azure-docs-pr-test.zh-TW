---
title: "Azure Mobile Engagement Android SDK 的 aaaAdvanced 組態"
description: "說明進階組態選項包括 hello，Android 的 Azure Mobile Engagement Android SDK 資訊清單的 hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="1308c-103">Azure Mobile Engagement Android SDK 的進階組態</span><span class="sxs-lookup"><span data-stu-id="1308c-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1308c-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="1308c-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="1308c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1308c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="1308c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1308c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="1308c-107">Android</span><span class="sxs-lookup"><span data-stu-id="1308c-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="1308c-108">此程序描述如何 tooconfigure Azure Mobile Engagement Android 應用程式的各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="1308c-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1308c-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1308c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="1308c-110">權限需求</span><span class="sxs-lookup"><span data-stu-id="1308c-110">Permission Requirements</span></span>
<span data-ttu-id="1308c-111">有些選項需要所有的參考和內嵌在 hello 特定功能中的以下所列的特定權限。</span><span class="sxs-lookup"><span data-stu-id="1308c-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="1308c-112">加入這些權限 toohello AndroidManifest.xml 專案的之前或之後 hello`<application>`標記。</span><span class="sxs-lookup"><span data-stu-id="1308c-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="1308c-113">hello 權限的程式碼需要 toolook 如下 hello，填寫 hello hello 表的適當權限。</span><span class="sxs-lookup"><span data-stu-id="1308c-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="1308c-114">權限</span><span class="sxs-lookup"><span data-stu-id="1308c-114">Permission</span></span> | <span data-ttu-id="1308c-115">使用時機</span><span class="sxs-lookup"><span data-stu-id="1308c-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="1308c-116">網際網路</span><span class="sxs-lookup"><span data-stu-id="1308c-116">INTERNET</span></span> |<span data-ttu-id="1308c-117">必要。</span><span class="sxs-lookup"><span data-stu-id="1308c-117">Required.</span></span> <span data-ttu-id="1308c-118">針對基本報告</span><span class="sxs-lookup"><span data-stu-id="1308c-118">For basic reporting</span></span> |
| <span data-ttu-id="1308c-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="1308c-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="1308c-120">必要。</span><span class="sxs-lookup"><span data-stu-id="1308c-120">Required.</span></span> <span data-ttu-id="1308c-121">針對基本報告</span><span class="sxs-lookup"><span data-stu-id="1308c-121">For basic reporting</span></span> |
| <span data-ttu-id="1308c-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="1308c-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="1308c-123">必要。</span><span class="sxs-lookup"><span data-stu-id="1308c-123">Required.</span></span> <span data-ttu-id="1308c-124">裝置重新開機後 hello 通知中心 tooshow</span><span class="sxs-lookup"><span data-stu-id="1308c-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="1308c-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="1308c-125">WAKE_LOCK</span></span> |<span data-ttu-id="1308c-126">建議使用。</span><span class="sxs-lookup"><span data-stu-id="1308c-126">Recommended.</span></span> <span data-ttu-id="1308c-127">啟用「在使用 WiFi 或螢幕關閉時收集統計資料」</span><span class="sxs-lookup"><span data-stu-id="1308c-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="1308c-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="1308c-128">VIBRATE</span></span> |<span data-ttu-id="1308c-129">選用。</span><span class="sxs-lookup"><span data-stu-id="1308c-129">Optional.</span></span> <span data-ttu-id="1308c-130">在收到通知後啟用震動</span><span class="sxs-lookup"><span data-stu-id="1308c-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="1308c-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="1308c-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="1308c-132">選用。</span><span class="sxs-lookup"><span data-stu-id="1308c-132">Optional.</span></span> <span data-ttu-id="1308c-133">啟用「Android 重點通知」</span><span class="sxs-lookup"><span data-stu-id="1308c-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="1308c-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="1308c-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="1308c-135">選用。</span><span class="sxs-lookup"><span data-stu-id="1308c-135">Optional.</span></span> <span data-ttu-id="1308c-136">啟用「Android 重點通知」</span><span class="sxs-lookup"><span data-stu-id="1308c-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="1308c-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="1308c-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="1308c-138">選用。</span><span class="sxs-lookup"><span data-stu-id="1308c-138">Optional.</span></span> <span data-ttu-id="1308c-139">啟用「即時位置報告」</span><span class="sxs-lookup"><span data-stu-id="1308c-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="1308c-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="1308c-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="1308c-141">選用。</span><span class="sxs-lookup"><span data-stu-id="1308c-141">Optional.</span></span> <span data-ttu-id="1308c-142">啟用「GPS 式即時位置報告」</span><span class="sxs-lookup"><span data-stu-id="1308c-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="1308c-143">從 Android M 開始，[某些權限是在執行階段管理](mobile-engagement-android-location-reporting.md#android-m-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1308c-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="1308c-144">如果您已經在使用``ACCESS_FINE_LOCATION``，則不需要 tooalso 使用``ACCESS_COARSE_LOCATION``。</span><span class="sxs-lookup"><span data-stu-id="1308c-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="1308c-145">Android 資訊清單組態選項</span><span class="sxs-lookup"><span data-stu-id="1308c-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="1308c-146">當機報告</span><span class="sxs-lookup"><span data-stu-id="1308c-146">Crash report</span></span>
<span data-ttu-id="1308c-147">toodisable 當機報告，加入此程式碼之間 hello`<application>`和`</application>`標記：</span><span class="sxs-lookup"><span data-stu-id="1308c-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="1308c-148">高載閾值</span><span class="sxs-lookup"><span data-stu-id="1308c-148">Burst threshold</span></span>
<span data-ttu-id="1308c-149">根據預設，hello Engagement 服務報表會即時記錄。</span><span class="sxs-lookup"><span data-stu-id="1308c-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="1308c-150">如果經常改變應用程式報表記錄，它是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 「 高載模式 」）。</span><span class="sxs-lookup"><span data-stu-id="1308c-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="1308c-151">toodo，因此請加入這個程式碼之間 hello`<application>`和`</application>`標記：</span><span class="sxs-lookup"><span data-stu-id="1308c-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="1308c-152">高載模式稍微增加 hello 電池壽命，但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。</span><span class="sxs-lookup"><span data-stu-id="1308c-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="1308c-153">高載閾值不能超過 30000 (30 秒)。</span><span class="sxs-lookup"><span data-stu-id="1308c-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="1308c-154">工作階段逾時</span><span class="sxs-lookup"><span data-stu-id="1308c-154">Session timeout</span></span>
 <span data-ttu-id="1308c-155">您可以按 hello 結束活動**首頁**或**回**索引鍵，透過閒置的 設定 hello 電話或跳到其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="1308c-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="1308c-156">根據預設，工作階段結束十秒 hello 其最後一個活動結尾之後。</span><span class="sxs-lookup"><span data-stu-id="1308c-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="1308c-157">這可避免工作階段分隔每個階段 hello 使用者結束，並傳回 toohello 應用程式快速，可以發生時 hello 使用者收取映像，檢查通知等等。您可能想 toomodify 這個參數。</span><span class="sxs-lookup"><span data-stu-id="1308c-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="1308c-158">toodo，因此請加入這個程式碼之間 hello`<application>`和`</application>`標記：</span><span class="sxs-lookup"><span data-stu-id="1308c-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="1308c-159">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="1308c-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="1308c-160">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="1308c-160">Using a method call</span></span>
<span data-ttu-id="1308c-161">如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="1308c-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="1308c-162">這個呼叫是持續性的：它使用共用的喜好設定檔案。</span><span class="sxs-lookup"><span data-stu-id="1308c-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="1308c-163">如果參與作用中時呼叫此函式，可能需要一分鐘的 hello 服務 toostop。</span><span class="sxs-lookup"><span data-stu-id="1308c-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="1308c-164">不過，它將不會啟動所有 hello hello 服務下次您啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1308c-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="1308c-165">您可以啟用記錄 reporting 再次呼叫相同函式與 hello `true`。</span><span class="sxs-lookup"><span data-stu-id="1308c-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="1308c-166">在您自己的 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="1308c-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="1308c-167">如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。</span><span class="sxs-lookup"><span data-stu-id="1308c-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="1308c-168">您可以設定您的喜好設定檔案 （由 hello 所需的模式） 的 Engagement toouse hello`AndroidManifest.xml`檔案搭配`application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="1308c-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="1308c-169">hello`engagement:agent:settings:name`金鑰是使用的 toodefine hello hello 共用的喜好設定檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1308c-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="1308c-170">hello`engagement:agent:settings:mode`金鑰是使用的 toodefine hello 模式 hello 共用的喜好設定檔案。</span><span class="sxs-lookup"><span data-stu-id="1308c-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="1308c-171">使用 hello 相同模式做為您`PreferenceActivity`。</span><span class="sxs-lookup"><span data-stu-id="1308c-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="1308c-172">必須傳遞 hello 模式，表示為數字： 如果您在程式碼中使用常數旗標的組合，請檢查 hello 總計值。</span><span class="sxs-lookup"><span data-stu-id="1308c-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="1308c-173">Engagement 一律會使用 hello`engagement:key`內 hello 喜好設定檔案，以便管理這項設定，則為 true 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1308c-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="1308c-174">下列範例中的 hello`AndroidManifest.xml`顯示 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="1308c-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="1308c-175">接著您可以將新增`CheckBoxPreference`中您的喜好設定配置，例如 hello 下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="1308c-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
