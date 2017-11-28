---
title: "aaaAzure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="1a141-103">升級程序</span><span class="sxs-lookup"><span data-stu-id="1a141-103">Upgrade procedures</span></span>
<span data-ttu-id="1a141-104">如果您已經有整合至您的應用程式較舊版本的我們 SDK，您必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="1a141-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="1a141-105">如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。</span><span class="sxs-lookup"><span data-stu-id="1a141-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="1a141-106">例如，如果您從 1.4.0 移轉 too1.6.0 您有遵循 hello toofirst"1.4.0 從 too1.5.0 」 程序然後 hello 」 從 1.5.0 too1.6.0 」 程序。</span><span class="sxs-lookup"><span data-stu-id="1a141-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="1a141-107">您升級，不論 hello 版本有 tooreplace hello`mobile-engagement-VERSION.jar`以 hello 新。</span><span class="sxs-lookup"><span data-stu-id="1a141-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="1a141-108">從 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="1a141-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="1a141-109">實際上在任何版本的 hello SDK 上完成這個步驟，就安全性改進整合觸達活動時。</span><span class="sxs-lookup"><span data-stu-id="1a141-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="1a141-110">您現在應該加入`exported="false"`tooall 觸達活動。</span><span class="sxs-lookup"><span data-stu-id="1a141-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="1a141-111">在您的 `AndroidManifest.xml`中，現在觸達活動應該看起來如下：</span><span class="sxs-lookup"><span data-stu-id="1a141-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="1a141-112">從 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="1a141-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="1a141-113">hello SDK 現在控制代碼新權限的模型從 Android M。</span><span class="sxs-lookup"><span data-stu-id="1a141-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="1a141-114">如果您使用定位功能或大型圖片通知，請閱讀 [本章節](mobile-engagement-android-integrate-engagement.md#android-m-permissions)。</span><span class="sxs-lookup"><span data-stu-id="1a141-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="1a141-115">此外 toohello 新權限模型中，我們現在支援在執行階段設定位置功能。</span><span class="sxs-lookup"><span data-stu-id="1a141-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="1a141-116">我們目前仍與 hello 位置的資訊清單參數相容，但現在已被取代。</span><span class="sxs-lookup"><span data-stu-id="1a141-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="1a141-117">toouse 執行階段組態，移除 hello 以下幾節從您``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="1a141-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="1a141-118">讀取和[這個更新的程序](mobile-engagement-android-integrate-engagement.md#location-reporting)toouse 執行階段組態改為。</span><span class="sxs-lookup"><span data-stu-id="1a141-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="1a141-119">從 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="1a141-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="1a141-120">原生推播</span><span class="sxs-lookup"><span data-stu-id="1a141-120">Native push</span></span>
<span data-ttu-id="1a141-121">原生推送 (GCM/ADM) 現在也用於應用程式內通知，您必須設定為任何類型的推播宣傳活動 hello 原生推送認證。</span><span class="sxs-lookup"><span data-stu-id="1a141-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="1a141-122">如果尚未完成，請遵循 [此程序](mobile-engagement-android-integrate-engagement-reach.md#native-push)。</span><span class="sxs-lookup"><span data-stu-id="1a141-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="1a141-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1a141-123">AndroidManifest.xml</span></span>
<span data-ttu-id="1a141-124">``AndroidManifest.xml``中的 Reach 整合已修改。</span><span class="sxs-lookup"><span data-stu-id="1a141-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="1a141-125">取代下列項目：</span><span class="sxs-lookup"><span data-stu-id="1a141-125">Replace this:</span></span>

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

<span data-ttu-id="1a141-126">依據</span><span class="sxs-lookup"><span data-stu-id="1a141-126">By</span></span>

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

<span data-ttu-id="1a141-127">現在當您按一下公告 (具有文字/網頁內容) 或輪詢，可能是載入畫面。</span><span class="sxs-lookup"><span data-stu-id="1a141-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="1a141-128">您的 tooadd 這 4.0.0 中這些活動 toowork:</span><span class="sxs-lookup"><span data-stu-id="1a141-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="1a141-129">資源</span><span class="sxs-lookup"><span data-stu-id="1a141-129">Resources</span></span>
<span data-ttu-id="1a141-130">內嵌 hello 新`res/layout/engagement_loading.xml`將檔案貼入您的專案。</span><span class="sxs-lookup"><span data-stu-id="1a141-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="1a141-131">從 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="1a141-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="1a141-132">hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a141-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="1a141-133">如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too2.4.0，然後套用 hello 遵循程序。</span><span class="sxs-lookup"><span data-stu-id="1a141-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a141-134">Capptain Mobile Engagement 不 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="1a141-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="1a141-135">移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a141-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="1a141-136">JAR 檔案</span><span class="sxs-lookup"><span data-stu-id="1a141-136">JAR file</span></span>
<span data-ttu-id="1a141-137">將 `libs` 資料夾中的 `capptain.jar` 以 `mobile-engagement-VERSION.jar`取代。</span><span class="sxs-lookup"><span data-stu-id="1a141-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="1a141-138">資源檔</span><span class="sxs-lookup"><span data-stu-id="1a141-138">Resource files</span></span>
<span data-ttu-id="1a141-139">我們提供每個資源檔 (前面加上`capptain_`) 已由新的 hello 取代 toobe (前面加上`engagement_`)。</span><span class="sxs-lookup"><span data-stu-id="1a141-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="1a141-140">如果您自訂這些檔案，您會有 toore-hello 新檔案，檔案上套用您的自訂**hello 資源檔中的所有 hello 識別碼也已重新都命名**。</span><span class="sxs-lookup"><span data-stu-id="1a141-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="1a141-141">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="1a141-141">Application ID</span></span>
<span data-ttu-id="1a141-142">現在 Engagement 使用連接字串 tooconfigure hello SDK 識別碼，例如 hello 應用程式識別項。</span><span class="sxs-lookup"><span data-stu-id="1a141-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="1a141-143">您有 toouse`EngagementAgent.init`方法在啟動器活動就像這樣：</span><span class="sxs-lookup"><span data-stu-id="1a141-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="1a141-144">您的應用程式的 hello 連接字串會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1a141-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="1a141-145">請移除任何呼叫太`CapptainAgent.configure`為`EngagementAgent.init`取代該方法。</span><span class="sxs-lookup"><span data-stu-id="1a141-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="1a141-146">hello`appId`可以再設定使用`AndroidManifest.xml`。</span><span class="sxs-lookup"><span data-stu-id="1a141-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="1a141-147">如果您的 `AndroidManifest.xml` 有下列區段，請將其移除：</span><span class="sxs-lookup"><span data-stu-id="1a141-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="1a141-148">Java API</span><span class="sxs-lookup"><span data-stu-id="1a141-148">Java API</span></span>
<span data-ttu-id="1a141-149">每個呼叫 tooany 我們 SDK 的 Java 類別已重新命名; toobe例如，`CapptainAgent.getInstance(this)`必須重新命名`EngagementAgent.getInstance(this)`，`extends CapptainActivity`必須重新命名`extends EngagementActivity`等等...</span><span class="sxs-lookup"><span data-stu-id="1a141-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="1a141-150">如果您已整合與預設代理程式喜好設定檔，hello 預設檔案名稱現在是`engagement.agent`hello 索引鍵是`engagement:agent`。</span><span class="sxs-lookup"><span data-stu-id="1a141-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="1a141-151">Hello Javascript 繫結器在建立 web 宣布，現在是`engagementReachContent`。</span><span class="sxs-lookup"><span data-stu-id="1a141-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="1a141-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1a141-152">AndroidManifest.xml</span></span>
<span data-ttu-id="1a141-153">許多變更發生那里、 hello 服務不會共用失效，且許多接收者不是可匯出了。</span><span class="sxs-lookup"><span data-stu-id="1a141-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="1a141-154">hello 服務宣告現在是更簡單。移除 hello 意圖篩選和內文的所有中繼資料，並加入`exportable=false`。</span><span class="sxs-lookup"><span data-stu-id="1a141-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="1a141-155">加上的所有項目是已重新命名的 toouse engagement。</span><span class="sxs-lookup"><span data-stu-id="1a141-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="1a141-156">現在的樣貌如下：</span><span class="sxs-lookup"><span data-stu-id="1a141-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="1a141-157">當您想 tooenable 測試記錄檔時，中繼資料，hello 現已移 toohello 應用程式標記和已重新命名：</span><span class="sxs-lookup"><span data-stu-id="1a141-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="1a141-158">只要已重新命名所有其他中繼資料，以下是 hello 完整清單 (當然重新命名只有 hello 的您所使用):</span><span class="sxs-lookup"><span data-stu-id="1a141-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="1a141-159">已移除 Google Play 和 SmartAd 追蹤從 SDK 您只需要 tooremove 這而不取代：</span><span class="sxs-lookup"><span data-stu-id="1a141-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="1a141-160">hello 觸達活動現在會宣告如下：</span><span class="sxs-lookup"><span data-stu-id="1a141-160">hello Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="1a141-161">如果您有自訂的觸達活動，您必須唯一 toochange hello 意圖動作 toomatch`com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT`或`com.microsoft.azure.engagement.reach.intent.action.POLL`。</span><span class="sxs-lookup"><span data-stu-id="1a141-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="1a141-162">hello 廣播的接收者已重新命名，再加上現在加入`exported=false`。</span><span class="sxs-lookup"><span data-stu-id="1a141-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="1a141-163">以下是 hello 的 hello 接收者 hello 新規格 (當然重新命名只有 hello 的您所使用) 的完整清單：</span><span class="sxs-lookup"><span data-stu-id="1a141-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="1a141-164">追蹤收件者已被移除，因此您需要 tooremove 這一節：</span><span class="sxs-lookup"><span data-stu-id="1a141-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="1a141-165">請注意您實作的 hello hello 宣告廣播接收者**EngagementMessageReceiver** hello 中已經變更`AndroidManifest.xml`。</span><span class="sxs-lookup"><span data-stu-id="1a141-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="1a141-166">這是因為 hello API toosend 和移除任意 XMPP 訊息從任意 XMPP 實體和 hello API toosend 而接收裝置之間的訊息已被移除。</span><span class="sxs-lookup"><span data-stu-id="1a141-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="1a141-167">因此，您必須也 toodelete hello 下列回呼您**EngagementMessageReceiver**實作：</span><span class="sxs-lookup"><span data-stu-id="1a141-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="1a141-168">和</span><span class="sxs-lookup"><span data-stu-id="1a141-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="1a141-169">然後刪除 **EngagementAgent** 對下列項目的任何呼叫：</span><span class="sxs-lookup"><span data-stu-id="1a141-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="1a141-170">和</span><span class="sxs-lookup"><span data-stu-id="1a141-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="1a141-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="1a141-171">Proguard</span></span>
<span data-ttu-id="1a141-172">Proguard 組態受到 rebranding，hello 規則現在正在尋找類似：</span><span class="sxs-lookup"><span data-stu-id="1a141-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

