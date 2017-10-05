---
title: "Azure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="1914b-103">升級程序</span><span class="sxs-lookup"><span data-stu-id="1914b-103">Upgrade procedures</span></span>
<span data-ttu-id="1914b-104">如果您已經整合我們的舊版 SDK 到您的應用程式，在升級 SDK 時您必須考慮以下幾點。</span><span class="sxs-lookup"><span data-stu-id="1914b-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="1914b-105">如果您有錯過幾個版本的 SDK，您必須遵循幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="1914b-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="1914b-106">例如，如果您要從 1.4.0 移轉到 1.6.0，必須先遵循「從 1.4.0 到 1.5.0」的程序，然後再依照「從 1.5.0 到 1.6.0」的程序進行。</span><span class="sxs-lookup"><span data-stu-id="1914b-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="1914b-107">不論您升級開始的版本為何，都必須將 `mobile-engagement-VERSION.jar` 替換為新的。</span><span class="sxs-lookup"><span data-stu-id="1914b-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="1914b-108">從 4.2.0 到 4.2.1</span><span class="sxs-lookup"><span data-stu-id="1914b-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="1914b-109">此步驟其實可以任何版本的 SDK 上完成，這是您在整合觸達活動時的安全性改善。</span><span class="sxs-lookup"><span data-stu-id="1914b-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="1914b-110">現在您應該新增 `exported="false"` 至所有觸達活動中。</span><span class="sxs-lookup"><span data-stu-id="1914b-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="1914b-111">在您的 `AndroidManifest.xml`中，現在觸達活動應該看起來如下：</span><span class="sxs-lookup"><span data-stu-id="1914b-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-to-410"></a><span data-ttu-id="1914b-112">從 4.0.0 到 4.1.0</span><span class="sxs-lookup"><span data-stu-id="1914b-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="1914b-113">SDK 現在處理 Android M 新的權限模型。</span><span class="sxs-lookup"><span data-stu-id="1914b-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="1914b-114">如果您使用定位功能或大型圖片通知，請閱讀 [本章節](mobile-engagement-android-integrate-engagement.md#android-m-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1914b-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="1914b-115">除了新的權限模型，現在支援在執行階段設定定位功能。</span><span class="sxs-lookup"><span data-stu-id="1914b-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="1914b-116">定位的資訊清單參數仍然相容，但現在已經被取代。</span><span class="sxs-lookup"><span data-stu-id="1914b-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="1914b-117">若要使用執行階段設定，請從您的 ``AndroidManifest.xml``移除下列區段：</span><span class="sxs-lookup"><span data-stu-id="1914b-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="1914b-118">並請閱讀 [此更新的程序](mobile-engagement-android-integrate-engagement.md#location-reporting) ，以改用執行階段設定。</span><span class="sxs-lookup"><span data-stu-id="1914b-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="1914b-119">從 3.0.0 到 4.0.0</span><span class="sxs-lookup"><span data-stu-id="1914b-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="1914b-120">原生推播</span><span class="sxs-lookup"><span data-stu-id="1914b-120">Native push</span></span>
<span data-ttu-id="1914b-121">原生推播 (GCM/ADM) 現在也用於應用程式通知，因此您必須為任何類型的推播行銷活動設定原生推播認證。</span><span class="sxs-lookup"><span data-stu-id="1914b-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="1914b-122">如果尚未完成，請遵循 [此程序](mobile-engagement-android-integrate-engagement-reach.md#native-push)。</span><span class="sxs-lookup"><span data-stu-id="1914b-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="1914b-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1914b-123">AndroidManifest.xml</span></span>
<span data-ttu-id="1914b-124">``AndroidManifest.xml``中的 Reach 整合已修改。</span><span class="sxs-lookup"><span data-stu-id="1914b-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="1914b-125">取代下列項目：</span><span class="sxs-lookup"><span data-stu-id="1914b-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="1914b-126">依據</span><span class="sxs-lookup"><span data-stu-id="1914b-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="1914b-127">現在當您按一下公告 (具有文字/網頁內容) 或輪詢，可能是載入畫面。</span><span class="sxs-lookup"><span data-stu-id="1914b-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="1914b-128">您必須加入此項目，這些行銷活動才能在 4.0.0 中運作：</span><span class="sxs-lookup"><span data-stu-id="1914b-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="1914b-129">資源</span><span class="sxs-lookup"><span data-stu-id="1914b-129">Resources</span></span>
<span data-ttu-id="1914b-130">內嵌新的 `res/layout/engagement_loading.xml` 檔案到您的專案。</span><span class="sxs-lookup"><span data-stu-id="1914b-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="1914b-131">從 2.4.0 到 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1914b-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="1914b-132">以下說明如何將 SDK 整合從 Capptain SAS 提供的 Capptain 服務，移轉到由 Azure Mobile Engagement 提供的應用程式內。</span><span class="sxs-lookup"><span data-stu-id="1914b-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="1914b-133">如果您是從較早版本移轉，請參閱 Capptain 網站，先移轉到 2.4.0 後再套用以下程序。</span><span class="sxs-lookup"><span data-stu-id="1914b-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1914b-134">Capptain 和 Mobile Engagement 是不同的服務，而以下程序只適用於移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1914b-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="1914b-135">移轉應用程式中的 SDK「不會」將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1914b-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="1914b-136">JAR 檔案</span><span class="sxs-lookup"><span data-stu-id="1914b-136">JAR file</span></span>
<span data-ttu-id="1914b-137">將 `libs` 資料夾中的 `capptain.jar` 以 `mobile-engagement-VERSION.jar`取代。</span><span class="sxs-lookup"><span data-stu-id="1914b-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="1914b-138">資源檔</span><span class="sxs-lookup"><span data-stu-id="1914b-138">Resource files</span></span>
<span data-ttu-id="1914b-139">我們提供的每個資源檔 (前置詞為 `capptain_`) 都必須替換為新的資源檔 (前置詞為 `engagement_`)。</span><span class="sxs-lookup"><span data-stu-id="1914b-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="1914b-140">如果您已自訂這些檔案，則必須在新的檔案上重新套用自訂， 資源檔中的所有識別碼也已重新命名。</span><span class="sxs-lookup"><span data-stu-id="1914b-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="1914b-141">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="1914b-141">Application ID</span></span>
<span data-ttu-id="1914b-142">現在 Engagement 使用連接字串來設定 SDK 識別碼，例如應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="1914b-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="1914b-143">您必須在啟動程式活動中使用 `EngagementAgent.init` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1914b-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="1914b-144">您應用程式的連接字串會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1914b-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="1914b-145">請移除對 `CapptainAgent.configure` 的所有呼叫，因為 `EngagementAgent.init` 已取代該方法。</span><span class="sxs-lookup"><span data-stu-id="1914b-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="1914b-146">無法再使用 `AndroidManifest.xml` 設定 `appId`。</span><span class="sxs-lookup"><span data-stu-id="1914b-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="1914b-147">如果您的 `AndroidManifest.xml` 有下列區段，請將其移除：</span><span class="sxs-lookup"><span data-stu-id="1914b-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="1914b-148">Java API</span><span class="sxs-lookup"><span data-stu-id="1914b-148">Java API</span></span>
<span data-ttu-id="1914b-149">對 SDK 任何 Java 類別的各個呼叫都必須重新命名，例如 `CapptainAgent.getInstance(this)` 必須重新命名為 `EngagementAgent.getInstance(this)`、`extends CapptainActivity` 必須重新命名為 `extends EngagementActivity`，以此類推...</span><span class="sxs-lookup"><span data-stu-id="1914b-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="1914b-150">如果您已整合預設代理程式喜好設定檔，現在預設檔案名稱是 `engagement.agent`，而索引鍵為 `engagement:agent`。</span><span class="sxs-lookup"><span data-stu-id="1914b-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="1914b-151">建立 Web 公告時，Javascript 繫結器現在是 `engagementReachContent`。</span><span class="sxs-lookup"><span data-stu-id="1914b-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="1914b-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1914b-152">AndroidManifest.xml</span></span>
<span data-ttu-id="1914b-153">這裡有許多變更，服務不再共用，且許多接收器也不再能匯出。</span><span class="sxs-lookup"><span data-stu-id="1914b-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="1914b-154">服務宣告現在更為簡單，移除意圖篩選及其內所有中繼資料，然後加入 `exportable=false`。</span><span class="sxs-lookup"><span data-stu-id="1914b-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="1914b-155">再加上所有項目重新命名以使用 Engagement。</span><span class="sxs-lookup"><span data-stu-id="1914b-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="1914b-156">現在的樣貌如下：</span><span class="sxs-lookup"><span data-stu-id="1914b-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="1914b-157">當您想要啟用測試記錄檔時，中繼資料現在已經移至應用程式標記，並且已重新命名：</span><span class="sxs-lookup"><span data-stu-id="1914b-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="1914b-158">所有其他中繼資料都已重新命名，完整清單如下 (當然，請只重新命名您所使用的項目)：</span><span class="sxs-lookup"><span data-stu-id="1914b-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="1914b-159">已從 SDK 移除 Google Play 和 SmartAd 追蹤，您只需要移除它，不必取代：</span><span class="sxs-lookup"><span data-stu-id="1914b-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="1914b-160">Reach 活動現在宣告如下：</span><span class="sxs-lookup"><span data-stu-id="1914b-160">The Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="1914b-161">如果您有自訂的 Reach 活動，只需要變更意圖動作，以符合 `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` 或 `com.microsoft.azure.engagement.reach.intent.action.POLL`。</span><span class="sxs-lookup"><span data-stu-id="1914b-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="1914b-162">廣播接收器已重新命名，此外我們現在也已加入 `exported=false`。</span><span class="sxs-lookup"><span data-stu-id="1914b-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="1914b-163">以下是新規格之接收器的完整清單 (當然，請只重新命名您所使用的項目)：</span><span class="sxs-lookup"><span data-stu-id="1914b-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="1914b-164">已移除追蹤接收器，所以您必須移除此區段：</span><span class="sxs-lookup"><span data-stu-id="1914b-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="1914b-165">請注意，您的廣播接收器 **EngagementMessageReceiver** 實作的宣告已在 `AndroidManifest.xml` 中變更。</span><span class="sxs-lookup"><span data-stu-id="1914b-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="1914b-166">這是因為已經移除從任意 XMPP 實體傳送和接收任意 XMPP 訊息的 API，以及在裝置之間傳送和接收訊息的 API。</span><span class="sxs-lookup"><span data-stu-id="1914b-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="1914b-167">因此，您也必須從您的 **EngagementMessageReceiver** 實作刪除下列回呼：</span><span class="sxs-lookup"><span data-stu-id="1914b-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="1914b-168">和</span><span class="sxs-lookup"><span data-stu-id="1914b-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="1914b-169">然後刪除 **EngagementAgent** 對下列項目的任何呼叫：</span><span class="sxs-lookup"><span data-stu-id="1914b-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="1914b-170">和</span><span class="sxs-lookup"><span data-stu-id="1914b-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="1914b-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="1914b-171">Proguard</span></span>
<span data-ttu-id="1914b-172">Proguard 組態受到品牌重新命名的影響，規則現在類似：</span><span class="sxs-lookup"><span data-stu-id="1914b-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

