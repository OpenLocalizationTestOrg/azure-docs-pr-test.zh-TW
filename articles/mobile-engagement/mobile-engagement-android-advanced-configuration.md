---
title: "Azure Mobile Engagement Android SDK 的進階組態"
description: "描述包含隨附 Azure Mobile Engagement Android SDK 之 Android 資訊清單的進階組態選項"
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
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="16dec-103">Azure Mobile Engagement Android SDK 的進階組態</span><span class="sxs-lookup"><span data-stu-id="16dec-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16dec-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="16dec-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="16dec-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="16dec-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="16dec-106">iOS</span><span class="sxs-lookup"><span data-stu-id="16dec-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="16dec-107">Android</span><span class="sxs-lookup"><span data-stu-id="16dec-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="16dec-108">此程序描述如何設定 Azure Mobile Engagement Android 應用程式的各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="16dec-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16dec-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="16dec-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="16dec-110">權限需求</span><span class="sxs-lookup"><span data-stu-id="16dec-110">Permission Requirements</span></span>
<span data-ttu-id="16dec-111">有一些選項需要特定權限，全部列在這裡方便參考，也內嵌在特定功能中。</span><span class="sxs-lookup"><span data-stu-id="16dec-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="16dec-112">將這些權限加入專案的 AndroidManifest.xml 中，而且要緊接在 `<application>` 標記之前或之後。</span><span class="sxs-lookup"><span data-stu-id="16dec-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="16dec-113">請根據下表填入適當的權限，權限程式碼必須看起來如下所示。</span><span class="sxs-lookup"><span data-stu-id="16dec-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="16dec-114">權限</span><span class="sxs-lookup"><span data-stu-id="16dec-114">Permission</span></span> | <span data-ttu-id="16dec-115">使用時機</span><span class="sxs-lookup"><span data-stu-id="16dec-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="16dec-116">網際網路</span><span class="sxs-lookup"><span data-stu-id="16dec-116">INTERNET</span></span> |<span data-ttu-id="16dec-117">必要。</span><span class="sxs-lookup"><span data-stu-id="16dec-117">Required.</span></span> <span data-ttu-id="16dec-118">針對基本報告</span><span class="sxs-lookup"><span data-stu-id="16dec-118">For basic reporting</span></span> |
| <span data-ttu-id="16dec-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="16dec-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="16dec-120">必要。</span><span class="sxs-lookup"><span data-stu-id="16dec-120">Required.</span></span> <span data-ttu-id="16dec-121">針對基本報告</span><span class="sxs-lookup"><span data-stu-id="16dec-121">For basic reporting</span></span> |
| <span data-ttu-id="16dec-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="16dec-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="16dec-123">必要。</span><span class="sxs-lookup"><span data-stu-id="16dec-123">Required.</span></span> <span data-ttu-id="16dec-124">若要在裝置重新啟動後顯示通知中心</span><span class="sxs-lookup"><span data-stu-id="16dec-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="16dec-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="16dec-125">WAKE_LOCK</span></span> |<span data-ttu-id="16dec-126">建議使用。</span><span class="sxs-lookup"><span data-stu-id="16dec-126">Recommended.</span></span> <span data-ttu-id="16dec-127">啟用「在使用 WiFi 或螢幕關閉時收集統計資料」</span><span class="sxs-lookup"><span data-stu-id="16dec-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="16dec-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="16dec-128">VIBRATE</span></span> |<span data-ttu-id="16dec-129">選用。</span><span class="sxs-lookup"><span data-stu-id="16dec-129">Optional.</span></span> <span data-ttu-id="16dec-130">在收到通知後啟用震動</span><span class="sxs-lookup"><span data-stu-id="16dec-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="16dec-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="16dec-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="16dec-132">選用。</span><span class="sxs-lookup"><span data-stu-id="16dec-132">Optional.</span></span> <span data-ttu-id="16dec-133">啟用「Android 重點通知」</span><span class="sxs-lookup"><span data-stu-id="16dec-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="16dec-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="16dec-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="16dec-135">選用。</span><span class="sxs-lookup"><span data-stu-id="16dec-135">Optional.</span></span> <span data-ttu-id="16dec-136">啟用「Android 重點通知」</span><span class="sxs-lookup"><span data-stu-id="16dec-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="16dec-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="16dec-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="16dec-138">選用。</span><span class="sxs-lookup"><span data-stu-id="16dec-138">Optional.</span></span> <span data-ttu-id="16dec-139">啟用「即時位置報告」</span><span class="sxs-lookup"><span data-stu-id="16dec-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="16dec-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="16dec-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="16dec-141">選用。</span><span class="sxs-lookup"><span data-stu-id="16dec-141">Optional.</span></span> <span data-ttu-id="16dec-142">啟用「GPS 式即時位置報告」</span><span class="sxs-lookup"><span data-stu-id="16dec-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="16dec-143">從 Android M 開始，[某些權限是在執行階段管理](mobile-engagement-android-location-reporting.md#android-m-permissions)。</span><span class="sxs-lookup"><span data-stu-id="16dec-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="16dec-144">如果您已使用 ``ACCESS_FINE_LOCATION``，則不需要同時使用 ``ACCESS_COARSE_LOCATION``。</span><span class="sxs-lookup"><span data-stu-id="16dec-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="16dec-145">Android 資訊清單組態選項</span><span class="sxs-lookup"><span data-stu-id="16dec-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="16dec-146">當機報告</span><span class="sxs-lookup"><span data-stu-id="16dec-146">Crash report</span></span>
<span data-ttu-id="16dec-147">若要停用當機報告，請在 `<application>` 和 `</application>` 標記之間加入此程式碼：</span><span class="sxs-lookup"><span data-stu-id="16dec-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="16dec-148">高載閾值</span><span class="sxs-lookup"><span data-stu-id="16dec-148">Burst threshold</span></span>
<span data-ttu-id="16dec-149">根據預設，Engagement 會即時報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="16dec-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="16dec-150">如果應用程式報告記錄檔經常有變化，建議您緩衝記錄檔，以固定時段一次報告全部的記錄檔 (稱為「高載模式」)。</span><span class="sxs-lookup"><span data-stu-id="16dec-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="16dec-151">若要這樣做，請在 `<application>` 和 `</application>` 標籤之間加入此程式碼：</span><span class="sxs-lookup"><span data-stu-id="16dec-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="16dec-152">高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響：所有工作階段和工作持續時間會調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。</span><span class="sxs-lookup"><span data-stu-id="16dec-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="16dec-153">高載閾值不能超過 30000 (30 秒)。</span><span class="sxs-lookup"><span data-stu-id="16dec-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="16dec-154">工作階段逾時</span><span class="sxs-lookup"><span data-stu-id="16dec-154">Session timeout</span></span>
 <span data-ttu-id="16dec-155">您可以按下 **Home** 或 **Back** 鍵結束活動，或跳到另一個應用程式設定行動電話閒置。</span><span class="sxs-lookup"><span data-stu-id="16dec-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="16dec-156">根據預設，工作階段會在最後一個活動結束之後 10 秒鐘結束。</span><span class="sxs-lookup"><span data-stu-id="16dec-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="16dec-157">這是為了避免當使用者退出但很快又返回應用程式 (例如使用者挑選影像、檢查通知等等) 時，工作階段產生分割的狀況。您可以修改這個參數。</span><span class="sxs-lookup"><span data-stu-id="16dec-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="16dec-158">若要這樣做，請在 `<application>` 和 `</application>` 標籤之間加入此程式碼：</span><span class="sxs-lookup"><span data-stu-id="16dec-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="16dec-159">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="16dec-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="16dec-160">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="16dec-160">Using a method call</span></span>
<span data-ttu-id="16dec-161">如果您想要 Engagement 停止傳送記錄檔，可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="16dec-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="16dec-162">這個呼叫是持續性的：它使用共用的喜好設定檔案。</span><span class="sxs-lookup"><span data-stu-id="16dec-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="16dec-163">如果當您呼叫此函式時 Engagement 已啟用，停止服務可能需要 1 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="16dec-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="16dec-164">不過，當您下次啟動應用程式時，完全不會啟動服務。</span><span class="sxs-lookup"><span data-stu-id="16dec-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="16dec-165">您可以使用 `true`呼叫相同函式，即可再次啟用記錄報告。</span><span class="sxs-lookup"><span data-stu-id="16dec-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="16dec-166">在您自己的 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="16dec-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="16dec-167">如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。</span><span class="sxs-lookup"><span data-stu-id="16dec-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="16dec-168">您可以在 `AndroidManifest.xml` 檔案中使用 `application meta-data`，設定 Engagement 使用您的喜好設定檔案 (搭配所需的模式)：</span><span class="sxs-lookup"><span data-stu-id="16dec-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="16dec-169">`engagement:agent:settings:name` 機碼可用來定義共用喜好設定檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="16dec-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="16dec-170">`engagement:agent:settings:mode` 機碼可用來定義共用喜好設定檔案的模式。</span><span class="sxs-lookup"><span data-stu-id="16dec-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="16dec-171">使用與您的 `PreferenceActivity`相同的模式。</span><span class="sxs-lookup"><span data-stu-id="16dec-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="16dec-172">模式必須以數字傳遞：如果您在程式碼中使用常數旗標的組合，請檢查總值。</span><span class="sxs-lookup"><span data-stu-id="16dec-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="16dec-173">Engagement 在喜好設定檔案內會一律使用 `engagement:key` 布林值機碼來管理這項設定。</span><span class="sxs-lookup"><span data-stu-id="16dec-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="16dec-174">下列 `AndroidManifest.xml` 範例顯示的是預設值：</span><span class="sxs-lookup"><span data-stu-id="16dec-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="16dec-175">接著您可以將 `CheckBoxPreference` 加入您的喜好設定配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="16dec-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
