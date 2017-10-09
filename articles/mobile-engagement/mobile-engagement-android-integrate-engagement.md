---
title: "aaaAzure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="3aff3-103">如何在 Android 上 Engagement tooIntegrate</span><span class="sxs-lookup"><span data-stu-id="3aff3-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aff3-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="3aff3-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="3aff3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3aff3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="3aff3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3aff3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="3aff3-107">Android</span><span class="sxs-lookup"><span data-stu-id="3aff3-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="3aff3-108">此程序描述 hello 最簡單方式 tooactivate Engagement 分析及監視您的 Android 應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="3aff3-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aff3-109">最低 Android SDK API 層級必須是 10 或更高版本 (Android 2.3.3 或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="3aff3-110">hello 步驟所記錄的足夠 tooactivates hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="3aff3-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="3aff3-111">hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 如何進階標記您的 Android 應用程式開發介面的 Mobile Engagement](mobile-engagement-android-use-engagement-api.md)自這些統計資料是應用程式相依。</span><span class="sxs-lookup"><span data-stu-id="3aff3-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="3aff3-112">嵌入您的 Android 專案中的 hello Engagement SDK 和服務</span><span class="sxs-lookup"><span data-stu-id="3aff3-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="3aff3-113">下載 hello 從 Android SDK[這裡](https://aka.ms/vq9mfn)取得`mobile-engagement-VERSION.jar`並將它們放入 hello `libs` Android 專案的資料夾 （如果它尚未存在，請建立 hello 程式庫資料夾）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aff3-114">如果您建立使用 ProGuard 應用程式套件，您需要 tookeep 某些類別。</span><span class="sxs-lookup"><span data-stu-id="3aff3-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="3aff3-115">您可以使用下列組態程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="3aff3-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="3aff3-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="3aff3-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="3aff3-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="3aff3-118">指定依照 hello 啟動器活動的方法呼叫 hello Engagement 連接字串：</span><span class="sxs-lookup"><span data-stu-id="3aff3-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3aff3-119">您的應用程式的 hello 連接字串會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3aff3-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="3aff3-120">如果遺失，新增下列 Android 的權限的 hello (之前 hello`<application>`標記):</span><span class="sxs-lookup"><span data-stu-id="3aff3-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="3aff3-121">新增下列區段的 hello (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="3aff3-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="3aff3-122">變更`<Your application name>`hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3aff3-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="3aff3-123">hello`android:label`屬性可讓您 toochoose hello hello Engagement 服務名稱將顯示 toohello 使用者在他們的電話號碼的 hello 」 執行的服務 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="3aff3-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="3aff3-124">它會建議 tooset 這個屬性太`"<Your application name>Service"`(例如`"AcmeFunGameService"`)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="3aff3-125">指定 hello`android:process`屬性可確保該 hello Engagement 服務會在自己的處理序 （在相同的處理序因為您的應用程式會使得您的主要/UI 執行緒可能較不回應 hello 執行 Engagement） 中執行。</span><span class="sxs-lookup"><span data-stu-id="3aff3-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="3aff3-126">您將放置在任何程式碼`Application.onCreate()`並將所有應用程式的處理程序，包括 hello Engagement 服務執行其他應用程式回呼。</span><span class="sxs-lookup"><span data-stu-id="3aff3-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="3aff3-127">它有不必要的副作用 （如不需要的記憶體配置和 hello Engagement 的程序、 重複廣播的接收者或服務中的執行緒）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="3aff3-128">如果您覆寫`Application.onCreate()`，它為下列程式碼片段在 hello 開頭的建議的 tooadd hello 您`Application.onCreate()`函式：</span><span class="sxs-lookup"><span data-stu-id="3aff3-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="3aff3-129">您可以 hello 相同的動作，如`Application.onTerminate()`，`Application.onLowMemory()`和`Application.onConfigurationChanged(...)`。</span><span class="sxs-lookup"><span data-stu-id="3aff3-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="3aff3-130">您也可以擴充`EngagementApplication`而不是擴充`Application`: hello 回呼`Application.onCreate()`程序的核取並呼叫沒有 hello`Application.onApplicationProcessCreate()`僅 hello 目前處理序是否不 hello 一個裝載 hello Engagement 服務，hello 適用相同的規則hello 其他回呼。</span><span class="sxs-lookup"><span data-stu-id="3aff3-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="3aff3-131">基本報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="3aff3-132">建議使用的方法：多載您的 `Activity` 類別</span><span class="sxs-lookup"><span data-stu-id="3aff3-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="3aff3-133">在訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您只需要 toomake 所有您`*Activity`子類別是繼承自 hello 對應`Engagement*Activity`類別 (例如： 如果您的舊版活動延伸`ListActivity`，讓它會擴充`EngagementListActivity`)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="3aff3-134">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="3aff3-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="3aff3-135">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="3aff3-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="3aff3-136">當使用`EngagementListActivity`或`EngagementExpandableListActivity`，請確定任何呼叫太`requestWindowFeature(...);`太進行 hello 呼叫之前`super.onCreate(...);`，否則會發生損毀。</span><span class="sxs-lookup"><span data-stu-id="3aff3-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="3aff3-137">您可以在 hello 找到這些類別`src`資料夾，並可以將其複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="3aff3-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="3aff3-138">hello 類別中也會有 hello **JavaDoc**。</span><span class="sxs-lookup"><span data-stu-id="3aff3-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="3aff3-139">替代方法：手動呼叫 `startActivity()` 和 `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="3aff3-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="3aff3-140">如果您無法或不想 toooverload 您`Activity`類別，您可以改為啟動及結束您的活動藉由呼叫`EngagementAgent`的直接的方法。</span><span class="sxs-lookup"><span data-stu-id="3aff3-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aff3-141">hello Android SDK 從未呼叫 hello`endActivity()`方法，即使關閉 hello 應用程式 （在 Android 上，已關閉應用程式實際上永遠不會）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="3aff3-142">因此，它是*高*建議 toocall hello `startActivity()` hello 中的方法`onResume`回呼的*所有*程式活動與 hello `endActivity()` hello 中的方法`onPause()`回呼的*所有*程式活動。</span><span class="sxs-lookup"><span data-stu-id="3aff3-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="3aff3-143">這是 hello 唯一方式 toobe 確定不會遺漏工作階段。</span><span class="sxs-lookup"><span data-stu-id="3aff3-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="3aff3-144">如果工作階段外洩，hello Engagement 服務將永遠不會中斷 hello Engagement 後端 （因為 hello 服務仍會保持連接，只要工作階段已暫止）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="3aff3-145">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="3aff3-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="3aff3-146">此範例非常類似 toohello`EngagementActivity`類別與變種，提供其原始程式碼中 hello`src`資料夾。</span><span class="sxs-lookup"><span data-stu-id="3aff3-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="3aff3-147">測試</span><span class="sxs-lookup"><span data-stu-id="3aff3-147">Test</span></span>
<span data-ttu-id="3aff3-148">現在請確認您的整合，方法是執行中模擬器或裝置的行動應用程式，然後確認它註冊 hello 監視 索引標籤上的工作階段。</span><span class="sxs-lookup"><span data-stu-id="3aff3-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="3aff3-149">hello 下一個區段是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="3aff3-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="3aff3-150">位置報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-150">Location reporting</span></span>
<span data-ttu-id="3aff3-151">如果您想位置 toobe 報告，您需要 tooadd 幾行程式的組態 (之間 hello`<application>`和`</application>`標記)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="3aff3-152">簡易區域位置報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-152">Lazy area location reporting</span></span>
<span data-ttu-id="3aff3-153">延遲區域位置回報允許 tooreport hello 國家/地區、 區域和位置相關聯 toodevices。</span><span class="sxs-lookup"><span data-stu-id="3aff3-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="3aff3-154">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="3aff3-155">裝置 hello 區域會報告每個工作階段最多一次。</span><span class="sxs-lookup"><span data-stu-id="3aff3-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="3aff3-156">hello GPS 從未使用過，，因此這種類型的報表位置會有很少 (不 toosay 沒有) hello 電池的影響。</span><span class="sxs-lookup"><span data-stu-id="3aff3-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="3aff3-157">報告的區域是使用的 toocompute 有關使用者、 工作階段、 事件和錯誤地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="3aff3-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="3aff3-158">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="3aff3-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="3aff3-159">tooenable 延遲區域位置回報，您可以使用此程序中先前所述的 hello 組態來進行：</span><span class="sxs-lookup"><span data-stu-id="3aff3-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3aff3-160">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="3aff3-161">或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="3aff3-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="3aff3-162">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-162">Real time location reporting</span></span>
<span data-ttu-id="3aff3-163">即時位置回報允許 tooreport hello 緯度和經度相關聯 toodevices。</span><span class="sxs-lookup"><span data-stu-id="3aff3-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="3aff3-164">根據預設，這類位置報告只會使用網路位置 （根據資料格識別碼或 WIFI），而且 hello reporting 僅 active hello 應用程式在前景中執行 （也就是在工作階段） 時。</span><span class="sxs-lookup"><span data-stu-id="3aff3-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="3aff3-165">即時位置*不*用 toocompute 統計資料。</span><span class="sxs-lookup"><span data-stu-id="3aff3-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="3aff3-166">其唯一用途就是即時地理圍欄 tooallow hello 使用\<觸達觀眾-地理圍欄\>觸達活動中的準則。</span><span class="sxs-lookup"><span data-stu-id="3aff3-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="3aff3-167">tooenable 即時位置回報，您可以使用此程序中先前所述的 hello 組態來進行：</span><span class="sxs-lookup"><span data-stu-id="3aff3-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3aff3-168">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="3aff3-169">或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="3aff3-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="3aff3-170">GPS 式報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-170">GPS based reporting</span></span>
<span data-ttu-id="3aff3-171">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="3aff3-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="3aff3-172">GPS tooenable hello 使用基礎 （也就是更精確） 的位置，請使用 hello 組態物件：</span><span class="sxs-lookup"><span data-stu-id="3aff3-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3aff3-173">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="3aff3-174">背景報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-174">Background reporting</span></span>
<span data-ttu-id="3aff3-175">根據預設，即時位置回報作用中時才 hello 應用程式在前景中執行 （也就是在工作階段）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="3aff3-176">tooenable hello reporting 也在背景中，使用 hello 組態物件：</span><span class="sxs-lookup"><span data-stu-id="3aff3-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="3aff3-177">當背景中執行 hello 應用程式時，會報告只有基礎的網路位置，即使您啟用 hello GPS。</span><span class="sxs-lookup"><span data-stu-id="3aff3-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="3aff3-178">若 hello 使用者重新開機裝置，將會停止 hello 背景位置的報表，您可以加入這個 toomake 自動重新啟動在開機時：</span><span class="sxs-lookup"><span data-stu-id="3aff3-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="3aff3-179">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="3aff3-180">Android M 權限</span><span class="sxs-lookup"><span data-stu-id="3aff3-180">Android M permissions</span></span>
<span data-ttu-id="3aff3-181">從 Android M 開始，某些權限會在執行階段管理，而且需要使用者核准。</span><span class="sxs-lookup"><span data-stu-id="3aff3-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="3aff3-182">如果您的目標 Android API 層級 23 hello 執行階段權限將會根據預設，新安裝的應用程式關閉。</span><span class="sxs-lookup"><span data-stu-id="3aff3-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="3aff3-183">否則預設將會開啟。</span><span class="sxs-lookup"><span data-stu-id="3aff3-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="3aff3-184">hello 使用者可以啟用/停用 hello 裝置設定 功能表中的這些權限。</span><span class="sxs-lookup"><span data-stu-id="3aff3-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="3aff3-185">關閉 權限，從系統功能表刪除 hello 應用程式的背景處理程序，這是系統行為，而且在能力 tooreceive 推送背景中沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="3aff3-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="3aff3-186">在 Mobile Engagement 的 hello 內容中，還需要在執行階段的核准的 hello 權限：</span><span class="sxs-lookup"><span data-stu-id="3aff3-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="3aff3-187">`WRITE_EXTERNAL_STORAGE` (只有在針對 Android API 層級 23 的這個權限時)</span><span class="sxs-lookup"><span data-stu-id="3aff3-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="3aff3-188">hello 外部儲存體只能用於觸達整體功能。</span><span class="sxs-lookup"><span data-stu-id="3aff3-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="3aff3-189">如果您發現要求此權限 toobe 干擾性的使用者，您可以將它移除您用 Mobile Engagement 只但停用大圖片功能 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="3aff3-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="3aff3-190">Hello 位置功能，您應要求權限 toouser 使用標準的系統對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3aff3-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="3aff3-191">如果 hello 使用者核准，您需要 tootell ``EngagementAgent`` tootake 以 （否則 hello 變更將會處理的 hello 下一個時間 hello 使用者啟動 hello 應用程式） 的即時變更納入考量。</span><span class="sxs-lookup"><span data-stu-id="3aff3-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="3aff3-192">以下是在您的應用程式 toorequest 權限和轉寄的 hello 結果的活動中的程式碼範例 toouse，如果正太``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="3aff3-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="3aff3-193">進階報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-193">Advanced reporting</span></span>
<span data-ttu-id="3aff3-194">（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您需要透過 hello 方法的 hello toouse hello Engagement API`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="3aff3-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="3aff3-195">這個類別的物件可以透過呼叫 hello 互動式`EngagementAgent.getInstance()`靜態方法。</span><span class="sxs-lookup"><span data-stu-id="3aff3-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="3aff3-196">hello Engagement API 允許 toouse 所有參與的進階功能，並會詳細說明 hello 如何 tooUse 在 Android 上的行動應用程式開發介面 (以及在 hello hello 的技術文件中`EngagementAgent`類別)。</span><span class="sxs-lookup"><span data-stu-id="3aff3-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="3aff3-197">進階組態 (在 AndroidManifest.xml 中)</span><span class="sxs-lookup"><span data-stu-id="3aff3-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="3aff3-198">線上醒機的鎖定</span><span class="sxs-lookup"><span data-stu-id="3aff3-198">Wake locks</span></span>
<span data-ttu-id="3aff3-199">如果您想 toobe 確定統計資料會傳送即時使用 Wifi 時，或關閉囉 」 畫面時，，加入下列選擇性權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="3aff3-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="3aff3-200">當機報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-200">Crash report</span></span>
<span data-ttu-id="3aff3-201">如果您想要 toodisable 損毀報表，加入 (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="3aff3-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="3aff3-202">高載閾值</span><span class="sxs-lookup"><span data-stu-id="3aff3-202">Burst threshold</span></span>
<span data-ttu-id="3aff3-203">根據預設，hello Engagement 服務報表會即時記錄。</span><span class="sxs-lookup"><span data-stu-id="3aff3-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="3aff3-204">如果您的應用程式會報告記錄檔頻率很高，是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 hello 「 高載模式 」）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="3aff3-205">toodo，加入 (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="3aff3-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="3aff3-206">hello 高載模式稍微增加 hello 電池壽命但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間將會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="3aff3-207">它會建議 toouse 高載臨界值不會再於 30000 （30 秒）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="3aff3-208">工作階段逾時</span><span class="sxs-lookup"><span data-stu-id="3aff3-208">Session timeout</span></span>
<span data-ttu-id="3aff3-209">根據預設，工作階段是以結束的 10s hello 其最後一個活動 （這通常是按 hello 首頁所致，或透過閒置的 設定 hello 電話或跳到其他應用程式，備份金鑰，） 的結尾之後。</span><span class="sxs-lookup"><span data-stu-id="3aff3-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="3aff3-210">這是 tooavoid 工作階段分隔每個階段 hello 使用者結束，並非常快速地返回 toohello 應用程式 （這可以發生時他挑選一個映像，請檢查通知等。）。</span><span class="sxs-lookup"><span data-stu-id="3aff3-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="3aff3-211">您可能想 toomodify 這個參數。</span><span class="sxs-lookup"><span data-stu-id="3aff3-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="3aff3-212">toodo，加入 (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="3aff3-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="3aff3-213">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="3aff3-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="3aff3-214">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="3aff3-214">Using a method call</span></span>
<span data-ttu-id="3aff3-215">如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="3aff3-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="3aff3-216">這個呼叫是持續性的：它使用共用的喜好設定檔案。</span><span class="sxs-lookup"><span data-stu-id="3aff3-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="3aff3-217">如果參與作用中時呼叫此函式，可能需要 hello 服務 toostop 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3aff3-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="3aff3-218">不過，它將不會啟動所有 hello hello 服務下次您啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3aff3-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="3aff3-219">您可以啟用記錄 reporting 再次呼叫相同函式與 hello `true`。</span><span class="sxs-lookup"><span data-stu-id="3aff3-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="3aff3-220">在您自己的 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="3aff3-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="3aff3-221">如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。</span><span class="sxs-lookup"><span data-stu-id="3aff3-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="3aff3-222">您可以設定您的喜好設定檔案 （由 hello 所需的模式） 的 Engagement toouse hello`AndroidManifest.xml`檔案搭配`application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="3aff3-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="3aff3-223">hello`engagement:agent:settings:name`金鑰是使用的 toodefine hello hello 共用的喜好設定檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3aff3-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="3aff3-224">hello`engagement:agent:settings:mode`金鑰是使用的 toodefine hello 模式 hello 共用的喜好設定檔案，您應該使用 hello 相同的模式，在您`PreferenceActivity`。</span><span class="sxs-lookup"><span data-stu-id="3aff3-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="3aff3-225">必須傳遞 hello 模式，表示為數字： 如果您在程式碼中使用常數旗標的組合，請檢查 hello 總計值。</span><span class="sxs-lookup"><span data-stu-id="3aff3-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="3aff3-226">Engagement 一律使用 hello`engagement:key`內 hello 喜好設定檔案，以便管理這項設定，則為 true 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3aff3-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="3aff3-227">下列範例中的 hello`AndroidManifest.xml`顯示 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="3aff3-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="3aff3-228">接著您可以將新增`CheckBoxPreference`中您的喜好設定配置，例如 hello 下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="3aff3-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
