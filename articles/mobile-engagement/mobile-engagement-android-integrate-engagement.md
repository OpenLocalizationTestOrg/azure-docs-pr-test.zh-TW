---
title: "Azure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="574cd-103">如何在 Android 上整合 Engagement</span><span class="sxs-lookup"><span data-stu-id="574cd-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="574cd-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="574cd-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="574cd-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="574cd-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="574cd-106">iOS</span><span class="sxs-lookup"><span data-stu-id="574cd-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="574cd-107">Android</span><span class="sxs-lookup"><span data-stu-id="574cd-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="574cd-108">此程序描述在您的 Android 應用程式中啟動 Engagement 分析和監視功能的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="574cd-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="574cd-109">最低 Android SDK API 層級必須是 10 或更高版本 (Android 2.3.3 或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="574cd-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="574cd-110">下列步驟足以啟動計算使用者、工作階段、活動、當機和技術相關之所有統計資料所需的記錄檔報表。</span><span class="sxs-lookup"><span data-stu-id="574cd-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="574cd-111">用來計算事件、錯誤及工作等其他統計資料所需的記錄檔報告必須使用 Engagement API 手動完成 (請參閱 [如何在 Android 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-android-use-engagement-api.md) )，因為這些是與應用程式相依的統計資料。</span><span class="sxs-lookup"><span data-stu-id="574cd-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="574cd-112">將 Engagement SDK 和服務嵌入至您的 Android 專案</span><span class="sxs-lookup"><span data-stu-id="574cd-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="574cd-113">從[這裡](https://aka.ms/vq9mfn)下載 Android SDK，取得 `mobile-engagement-VERSION.jar` 並將它們放入 Android 專案的 `libs` 資料夾 (如果 libs 資料夾尚不存在，請建立此資料夾)。</span><span class="sxs-lookup"><span data-stu-id="574cd-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="574cd-114">如果您使用 ProGuard 建立應用程式封裝，您需要保留一些類別。</span><span class="sxs-lookup"><span data-stu-id="574cd-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="574cd-115">您可以使用下列組態程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="574cd-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="574cd-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="574cd-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="574cd-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="574cd-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="574cd-118">在啟動器活動中呼叫下列方法，指定 Engagement 連接字串：</span><span class="sxs-lookup"><span data-stu-id="574cd-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="574cd-119">您應用程式的連接字串會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="574cd-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="574cd-120">若有遺漏，請加入下列 Android 權限 (在 `<application>` 標記之前)：</span><span class="sxs-lookup"><span data-stu-id="574cd-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="574cd-121">加入下列區段 (在 `<application>` 和 `</application>` 標記之間)：</span><span class="sxs-lookup"><span data-stu-id="574cd-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="574cd-122">將 `<Your application name>` 改為您應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="574cd-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="574cd-123">`android:label` 屬性可讓您選擇 Engagement 服務的名稱，此名稱會出現在使用者電話的「執行中服務」畫面中。</span><span class="sxs-lookup"><span data-stu-id="574cd-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="574cd-124">建議將此屬性設定為 `"<Your application name>Service"` (例如 `"AcmeFunGameService"`)。</span><span class="sxs-lookup"><span data-stu-id="574cd-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="574cd-125">指定 `android:process` 屬性可確保 Engagement 服務在本身的處理程序中執行 (在與應用程式相同的處理程序中執行 Engagement，可能會造成主要/UI 執行緒回應速度較慢)。</span><span class="sxs-lookup"><span data-stu-id="574cd-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="574cd-126">您放置在 `Application.onCreate()` 和其他應用程式回呼中的程式碼會針對您所有應用程式的處理程序而執行，其中包括 Engagement 服務。</span><span class="sxs-lookup"><span data-stu-id="574cd-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="574cd-127">可能會產生不必要的副作用 (例如 Engagement 處理程序中不必要的記憶體配置和執行緒、重複的廣播接收器或服務)。</span><span class="sxs-lookup"><span data-stu-id="574cd-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="574cd-128">如果覆寫 `Application.onCreate()`，建議在 `Application.onCreate()` 函數的開頭加入下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="574cd-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="574cd-129">您可以對 `Application.onTerminate()`、`Application.onLowMemory()` 和 `Application.onConfigurationChanged(...)` 執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="574cd-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="574cd-130">您也可以不延伸 `Application`，改為延伸 `EngagementApplication`：回呼 `Application.onCreate()` 會進行處理程序檢查，並在目前的處理程序不是裝載 Engagement 服務的處理程序時才會呼叫 `Application.onApplicationProcessCreate()`，相同規則也適用於其他回呼。</span><span class="sxs-lookup"><span data-stu-id="574cd-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="574cd-131">基本報告</span><span class="sxs-lookup"><span data-stu-id="574cd-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="574cd-132">建議使用的方法：多載您的 `Activity` 類別</span><span class="sxs-lookup"><span data-stu-id="574cd-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="574cd-133">若要啟動 Engagement 需要的所有記錄檔報告以計算使用者、工作階段、活動、當機和技術統計資料，您只需要讓所有 `*Activity` 子類別繼承自對應的 `Engagement*Activity` 類別 (例如，如果您的舊版活動延伸 `ListActivity`，則使其延伸 `EngagementListActivity`)。</span><span class="sxs-lookup"><span data-stu-id="574cd-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="574cd-134">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="574cd-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="574cd-135">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="574cd-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="574cd-136">使用 `EngagementListActivity` 或 `EngagementExpandableListActivity` 時，務必先呼叫 `requestWindowFeature(...);` 再呼叫 `super.onCreate(...);`，否則會發生當機。</span><span class="sxs-lookup"><span data-stu-id="574cd-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="574cd-137">您可以在 `src` 資料夾中找到這些類別，並將其複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="574cd-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="574cd-138">這些類別也會顯示在 **JavaDoc** 中。</span><span class="sxs-lookup"><span data-stu-id="574cd-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="574cd-139">替代方法：手動呼叫 `startActivity()` 和 `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="574cd-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="574cd-140">如果您無法或不想多載 `Activity` 類別，可以改用直接呼叫 `EngagementAgent` 的方式來開始及結束您的活動。</span><span class="sxs-lookup"><span data-stu-id="574cd-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="574cd-141">Android SDK 絕不會呼叫 `endActivity()` 方法，即使在關閉應用程式後也不會呼叫 (在 Android 上，應用程式其實永遠不會關閉)。</span><span class="sxs-lookup"><span data-stu-id="574cd-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="574cd-142">因此，「強烈」建議在您「所有」活動的 `onResume` 回呼中呼叫 `startActivity()` 方法，以及在您「所有」活動的 `onPause()` 回呼中呼叫 `endActivity()` 方法。</span><span class="sxs-lookup"><span data-stu-id="574cd-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="574cd-143">這是確保不會遺漏工作階段的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="574cd-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="574cd-144">如果遺漏了工作階段，Engagement 服務將永遠不會從 Engagement 後端中斷連線 (因為只要工作階段處於暫止狀態，服務就會保持連線)。</span><span class="sxs-lookup"><span data-stu-id="574cd-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="574cd-145">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="574cd-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="574cd-146">這個範例非常類似於 `EngagementActivity` 類別與其變體，在 `src` 資料夾中提供會其原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="574cd-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="574cd-147">測試</span><span class="sxs-lookup"><span data-stu-id="574cd-147">Test</span></span>
<span data-ttu-id="574cd-148">現在請確認您的整合，方法是在模擬器或裝置中執行您的行動應用程式，並確認它會在 [監視] 索引標籤上註冊工作階段。</span><span class="sxs-lookup"><span data-stu-id="574cd-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="574cd-149">下一節是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="574cd-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="574cd-150">位置報告</span><span class="sxs-lookup"><span data-stu-id="574cd-150">Location reporting</span></span>
<span data-ttu-id="574cd-151">如果想要報告位置，您需要加入幾行組態 (在 `<application>` 和 `</application>` 標記之間)。</span><span class="sxs-lookup"><span data-stu-id="574cd-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="574cd-152">延遲區域位置報告</span><span class="sxs-lookup"><span data-stu-id="574cd-152">Lazy area location reporting</span></span>
<span data-ttu-id="574cd-153">延遲區域位置報告允許報告國家、地區以及與裝置相關聯的位置。</span><span class="sxs-lookup"><span data-stu-id="574cd-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="574cd-154">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="574cd-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="574cd-155">每個工作階段最多報告一次裝置區域。</span><span class="sxs-lookup"><span data-stu-id="574cd-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="574cd-156">絕不會使用 GPS，因此這類位置報告對於電池的影響很小 (但不是沒有)。</span><span class="sxs-lookup"><span data-stu-id="574cd-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="574cd-157">報告的區域用來計算關於使用者、工作階段、事件與錯誤的地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="574cd-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="574cd-158">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="574cd-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="574cd-159">若要啟用簡易區域位置報告，您可以使用此程序中先前所述的組態執行：</span><span class="sxs-lookup"><span data-stu-id="574cd-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="574cd-160">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="574cd-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="574cd-161">或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="574cd-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="574cd-162">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="574cd-162">Real time location reporting</span></span>
<span data-ttu-id="574cd-163">即時位置報告允許報告與裝置相關聯的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="574cd-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="574cd-164">根據預設，這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)，且只會在應用程式於前景中執行 (也就是在工作階段) 時，報告才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="574cd-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="574cd-165">即時位置「不會」  用來計算統計資料。</span><span class="sxs-lookup"><span data-stu-id="574cd-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="574cd-166">其唯一用途，是允許在觸達活動中使用即時地理圍欄 \<Reach-Audience-geofencing\> 準則。</span><span class="sxs-lookup"><span data-stu-id="574cd-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="574cd-167">若要啟用即時位置報告，您可以使用此程序中先前所述的組態執行：</span><span class="sxs-lookup"><span data-stu-id="574cd-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="574cd-168">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="574cd-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="574cd-169">或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="574cd-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="574cd-170">GPS 式報告</span><span class="sxs-lookup"><span data-stu-id="574cd-170">GPS based reporting</span></span>
<span data-ttu-id="574cd-171">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="574cd-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="574cd-172">若要啟用 GPS 位置 (精準度大為提高)，請使用組態物件：</span><span class="sxs-lookup"><span data-stu-id="574cd-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="574cd-173">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="574cd-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="574cd-174">背景報告</span><span class="sxs-lookup"><span data-stu-id="574cd-174">Background reporting</span></span>
<span data-ttu-id="574cd-175">根據預設，即時位置報告只在應用程式在前景中執行 (也就是在工作階段) 時才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="574cd-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="574cd-176">若也要在背景中啟用報告，請使用組態物件：</span><span class="sxs-lookup"><span data-stu-id="574cd-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="574cd-177">當應用程式在背景中執行，即使啟用 GPS，也只會報告網路位置。</span><span class="sxs-lookup"><span data-stu-id="574cd-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="574cd-178">如果使用者重新啟動裝置，就會停止背景位置報表，您可以加入以下內容，讓它在開機時自動重新啟動：</span><span class="sxs-lookup"><span data-stu-id="574cd-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="574cd-179">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="574cd-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="574cd-180">Android M 權限</span><span class="sxs-lookup"><span data-stu-id="574cd-180">Android M permissions</span></span>
<span data-ttu-id="574cd-181">從 Android M 開始，某些權限會在執行階段管理，而且需要使用者核准。</span><span class="sxs-lookup"><span data-stu-id="574cd-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="574cd-182">如果您針對 Android API 層級 23，新的應用程式安裝預設將會關閉執行階段權限。</span><span class="sxs-lookup"><span data-stu-id="574cd-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="574cd-183">否則預設將會開啟。</span><span class="sxs-lookup"><span data-stu-id="574cd-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="574cd-184">使用者可以從裝置設定功能表啟用/停用這些權限。</span><span class="sxs-lookup"><span data-stu-id="574cd-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="574cd-185">從系統功能表關閉權限會刪除應用程式的背景處理程序，這是一種系統行為，對於在背景中接收推播的功能不會有任何影響。</span><span class="sxs-lookup"><span data-stu-id="574cd-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="574cd-186">在 Mobile Engagement 環境中，需要在執行階段核准的權限為：</span><span class="sxs-lookup"><span data-stu-id="574cd-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="574cd-187">`WRITE_EXTERNAL_STORAGE` (只有在針對 Android API 層級 23 的這個權限時)</span><span class="sxs-lookup"><span data-stu-id="574cd-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="574cd-188">只有觸達概觀功能才會使用外部儲存體。</span><span class="sxs-lookup"><span data-stu-id="574cd-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="574cd-189">如果您發現向使用者要求這個權限會引起混亂，而您只是為了 Mobile Engagement 才使用它但必須停用概觀功能，您可以將它移除。</span><span class="sxs-lookup"><span data-stu-id="574cd-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="574cd-190">對於位置功能，您應該使用標準的系統對話方塊向使用者要求權限。</span><span class="sxs-lookup"><span data-stu-id="574cd-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="574cd-191">如果使用者核准，您必須告訴 ``EngagementAgent`` 即時將變更納入考量 (否則下次使用者啟動應用程式時會處理變更)。</span><span class="sxs-lookup"><span data-stu-id="574cd-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="574cd-192">以下是在應用程式要求權限並轉送結果 (如果 ``EngagementAgent``收到肯定) 時的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="574cd-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="574cd-193">進階報告</span><span class="sxs-lookup"><span data-stu-id="574cd-193">Advanced reporting</span></span>
<span data-ttu-id="574cd-194">此外，如果您想要報告應用程式的特定事件、錯誤及工作，必須透過 `EngagementAgent` 類別的方法使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="574cd-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="574cd-195">此類別的物件可以透過呼叫 `EngagementAgent.getInstance()` 靜態方法來擷取。</span><span class="sxs-lookup"><span data-stu-id="574cd-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="574cd-196">Engagement API 可允許使用所有 Engagement 的進階功能，詳情請見＜如何在 Android 上使用 Engagement API＞(以及 `EngagementAgent` 類別的技術文件)。</span><span class="sxs-lookup"><span data-stu-id="574cd-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="574cd-197">進階組態 (在 AndroidManifest.xml 中)</span><span class="sxs-lookup"><span data-stu-id="574cd-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="574cd-198">線上醒機的鎖定</span><span class="sxs-lookup"><span data-stu-id="574cd-198">Wake locks</span></span>
<span data-ttu-id="574cd-199">如果您希望在使用 Wifi 或關閉螢幕時仍確保即時傳送統計資料，請新增下列選用權限：</span><span class="sxs-lookup"><span data-stu-id="574cd-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="574cd-200">當機報告</span><span class="sxs-lookup"><span data-stu-id="574cd-200">Crash report</span></span>
<span data-ttu-id="574cd-201">如果您想要停用當機報告，請加入下列內容 (在 `<application>` 和 `</application>` 標記之間)：</span><span class="sxs-lookup"><span data-stu-id="574cd-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="574cd-202">高載閾值</span><span class="sxs-lookup"><span data-stu-id="574cd-202">Burst threshold</span></span>
<span data-ttu-id="574cd-203">根據預設，Engagement 會即時報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="574cd-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="574cd-204">如果應用程式報告記錄檔的頻率很高，建議您緩衝記錄檔，以固定時段一次報告全部的記錄檔 (此稱為「高載模式」)。</span><span class="sxs-lookup"><span data-stu-id="574cd-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="574cd-205">若要完成此作業，請加入下列內容 (在 `<application>` 和 `</application>` 標記之間)：</span><span class="sxs-lookup"><span data-stu-id="574cd-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="574cd-206">高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響： 所有工作階段和工作持續時間將調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。</span><span class="sxs-lookup"><span data-stu-id="574cd-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="574cd-207">建議使用低於 30000 (30 秒) 的閾值。</span><span class="sxs-lookup"><span data-stu-id="574cd-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="574cd-208">工作階段逾時</span><span class="sxs-lookup"><span data-stu-id="574cd-208">Session timeout</span></span>
<span data-ttu-id="574cd-209">根據預設，工作階段會在最後一個活動結束後 10 秒終止 (最後一個活動通常發生在按 [首頁] 或 [上一步] 鍵、將行動電話設定為閒置或跳到另一個應用程式)。</span><span class="sxs-lookup"><span data-stu-id="574cd-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="574cd-210">這是為了避免當使用者退出但很快又返回應用程式 (例如使用者挑選影像、檢查通知等等) 時，工作階段產生分割的狀況。</span><span class="sxs-lookup"><span data-stu-id="574cd-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="574cd-211">您可以修改這個參數。</span><span class="sxs-lookup"><span data-stu-id="574cd-211">You may want to modify this parameter.</span></span> <span data-ttu-id="574cd-212">若要完成此作業，請加入下列內容 (在 `<application>` 和 `</application>` 標記之間)：</span><span class="sxs-lookup"><span data-stu-id="574cd-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="574cd-213">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="574cd-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="574cd-214">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="574cd-214">Using a method call</span></span>
<span data-ttu-id="574cd-215">如果您想要 Engagement 停止傳送記錄檔，可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="574cd-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="574cd-216">這個呼叫是持續性的：它使用共用的喜好設定檔案。</span><span class="sxs-lookup"><span data-stu-id="574cd-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="574cd-217">如果當您呼叫此函式時 Engagement 已啟用，停止服務可能需要 1 分鐘時間。</span><span class="sxs-lookup"><span data-stu-id="574cd-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="574cd-218">不過，當您下次啟動應用程式時，完全不會啟動服務。</span><span class="sxs-lookup"><span data-stu-id="574cd-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="574cd-219">您可以使用 `true`呼叫相同函式，即可再次啟用記錄報告。</span><span class="sxs-lookup"><span data-stu-id="574cd-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="574cd-220">在您自己的 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="574cd-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="574cd-221">如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。</span><span class="sxs-lookup"><span data-stu-id="574cd-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="574cd-222">您可以在 `AndroidManifest.xml` 檔案中使用 `application meta-data`，設定 Engagement 使用您的喜好設定檔案 (搭配所需的模式)：</span><span class="sxs-lookup"><span data-stu-id="574cd-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="574cd-223">`engagement:agent:settings:name` 機碼可用來定義共用喜好設定檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="574cd-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="574cd-224">`engagement:agent:settings:mode` 機碼可用來定義共用喜好設定檔案的模式，您應該使用與 `PreferenceActivity` 中相同的模式。</span><span class="sxs-lookup"><span data-stu-id="574cd-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="574cd-225">模式必須以數字傳遞：如果您在程式碼中使用常數旗標的組合，請檢查總值。</span><span class="sxs-lookup"><span data-stu-id="574cd-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="574cd-226">Engagement 在喜好設定檔案內會一律使用 `engagement:key` 布林值機碼來管理這項設定。</span><span class="sxs-lookup"><span data-stu-id="574cd-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="574cd-227">下列 `AndroidManifest.xml` 範例顯示的是預設值：</span><span class="sxs-lookup"><span data-stu-id="574cd-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="574cd-228">接著您可以將 `CheckBoxPreference` 加入您的喜好設定配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="574cd-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
