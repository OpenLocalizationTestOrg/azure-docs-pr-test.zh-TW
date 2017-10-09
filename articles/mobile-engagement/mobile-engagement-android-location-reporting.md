---
title: "aaaLocation Azure Mobile Engagement Android SDK 的報告"
description: "描述如何 tooconfigure 報告 Azure Mobile Engagement Android SDK 的位置"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="85627-103">Azure Mobile Engagement Android SDK 位置報告</span><span class="sxs-lookup"><span data-stu-id="85627-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85627-104">Android</span><span class="sxs-lookup"><span data-stu-id="85627-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="85627-105">本主題描述如何為 Android 應用程式報告 toodo 位置。</span><span class="sxs-lookup"><span data-stu-id="85627-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85627-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="85627-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="85627-107">位置報告</span><span class="sxs-lookup"><span data-stu-id="85627-107">Location reporting</span></span>
<span data-ttu-id="85627-108">如果您想位置 toobe 報告，您需要 tooadd 幾行程式的組態 (之間 hello`<application>`和`</application>`標記)。</span><span class="sxs-lookup"><span data-stu-id="85627-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="85627-109">簡易區域位置報告</span><span class="sxs-lookup"><span data-stu-id="85627-109">Lazy area location reporting</span></span>
<span data-ttu-id="85627-110">延遲區域位置回報，可讓報告 hello 國家/地區、 區域和位置與裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="85627-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="85627-111">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="85627-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="85627-112">裝置 hello 區域會報告每個工作階段最多一次。</span><span class="sxs-lookup"><span data-stu-id="85627-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="85627-113">hello GPS 從未使用過，而且因此這種類型的報表位置對低影響 hello 電池。</span><span class="sxs-lookup"><span data-stu-id="85627-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="85627-114">報告的區域是使用的 toocompute 有關使用者、 工作階段、 事件和錯誤的地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="85627-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="85627-115">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="85627-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="85627-116">您啟用延遲區域位置使用先前在此程序所述的 hello 組態報表：</span><span class="sxs-lookup"><span data-stu-id="85627-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="85627-117">您也需要 toospecify 位置的權限。</span><span class="sxs-lookup"><span data-stu-id="85627-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="85627-118">此程式碼使用 ``COARSE`` 權限︰</span><span class="sxs-lookup"><span data-stu-id="85627-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="85627-119">如果您的應用程式需要，可以改用 ``ACCESS_FINE_LOCATION`` 。</span><span class="sxs-lookup"><span data-stu-id="85627-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="85627-120">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="85627-120">Real-time location reporting</span></span>
<span data-ttu-id="85627-121">啟用即時位置回報，報告的 hello 緯度和經度與裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="85627-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="85627-122">這類位置報告預設只會根據基地台識別碼或 WIFI 使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="85627-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="85627-123">hello 報告使用中時才 hello 應用程式在前景中執行 （例如，在工作階段）。</span><span class="sxs-lookup"><span data-stu-id="85627-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="85627-124">即時位置*不*用 toocompute 統計資料。</span><span class="sxs-lookup"><span data-stu-id="85627-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="85627-125">其唯一用途就是即時地理圍欄 tooallow hello 使用\<觸達觀眾-地理圍欄\>觸達活動中的準則。</span><span class="sxs-lookup"><span data-stu-id="85627-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="85627-126">tooenable 即時位置回報，加入一行程式碼 toowhere 您可設定 hello Engagement 連接字串 hello 啟動器活動中。</span><span class="sxs-lookup"><span data-stu-id="85627-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="85627-127">hello 結果看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="85627-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="85627-128">GPS 的報告</span><span class="sxs-lookup"><span data-stu-id="85627-128">GPS based reporting</span></span>
<span data-ttu-id="85627-129">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="85627-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="85627-130">tooenable hello GPS 基礎位置，請以更精確、 使用 hello 組態物件：</span><span class="sxs-lookup"><span data-stu-id="85627-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="85627-131">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="85627-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="85627-132">背景報告</span><span class="sxs-lookup"><span data-stu-id="85627-132">Background reporting</span></span>
<span data-ttu-id="85627-133">根據預設，即時位置回報作用中時才 hello 應用程式在前景中執行 （例如，在工作階段）。</span><span class="sxs-lookup"><span data-stu-id="85627-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="85627-134">tooenable hello reporting 也在背景中，使用這個組態物件：</span><span class="sxs-lookup"><span data-stu-id="85627-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="85627-135">當背景中執行 hello 應用程式時，會報告只有網路為基礎的位置，即使您啟用 hello GPS。</span><span class="sxs-lookup"><span data-stu-id="85627-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="85627-136">Hello 使用者重新啟動他們的裝置，並停止 hello 背景位置的報表。</span><span class="sxs-lookup"><span data-stu-id="85627-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="85627-137">toomake 自動重新啟動在開機時，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="85627-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="85627-138">您還需要下列權限，如果遺漏 tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="85627-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="85627-139">Android M 權限</span><span class="sxs-lookup"><span data-stu-id="85627-139">Android M permissions</span></span>
<span data-ttu-id="85627-140">從 Android M 開始，某些權限會在執行階段管理，而且需要使用者核准。</span><span class="sxs-lookup"><span data-stu-id="85627-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="85627-141">如果您的目標 Android API 層級 23，hello 執行階段權限會根據預設，新安裝的應用程式已關閉。</span><span class="sxs-lookup"><span data-stu-id="85627-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="85627-142">否則預設會開啟。</span><span class="sxs-lookup"><span data-stu-id="85627-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="85627-143">您可以啟用/停用 hello 裝置設定 功能表中的這些權限。</span><span class="sxs-lookup"><span data-stu-id="85627-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="85627-144">關閉 權限從 hello 系統功能表時，會清除 hello hello 應用程式，這是一種系統行為，且不會影響在背景中能力 tooreceive 推送的背景處理程序。</span><span class="sxs-lookup"><span data-stu-id="85627-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="85627-145">在 Mobile Engagement 位置 reporting hello 內容，還需要在執行階段的核准的 hello 權限：</span><span class="sxs-lookup"><span data-stu-id="85627-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="85627-146">從使用標準的系統對話方塊 hello 使用者要求權限。</span><span class="sxs-lookup"><span data-stu-id="85627-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="85627-147">如果 hello 使用者核准，告訴``EngagementAgent``tootake 變更成即時帳戶。</span><span class="sxs-lookup"><span data-stu-id="85627-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="85627-148">否則 hello 變更是處理的 hello 下一個時間 hello 使用者啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="85627-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="85627-149">以下是在您的應用程式 toorequest 權限和轉寄的 hello 結果的活動中的程式碼範例 toouse，如果正太``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="85627-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
