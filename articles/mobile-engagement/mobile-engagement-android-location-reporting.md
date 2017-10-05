---
title: "Azure Mobile Engagement Android SDK 位置報告"
description: "描述如何設定 Azure Mobile Engagement Android SDK 位置報告"
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
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="3ed3b-103">Azure Mobile Engagement Android SDK 位置報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ed3b-104">Android</span><span class="sxs-lookup"><span data-stu-id="3ed3b-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="3ed3b-105">本主題說明如何為您的 Android 應用程式進行位置報告。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ed3b-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ed3b-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="3ed3b-107">位置報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-107">Location reporting</span></span>
<span data-ttu-id="3ed3b-108">如果想要報告位置，您需要加入幾行組態 (在 `<application>` 和 `</application>` 標記之間)。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="3ed3b-109">簡易區域位置報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-109">Lazy area location reporting</span></span>
<span data-ttu-id="3ed3b-110">簡易區域位置報告可報告國家、地區以及與裝置相關聯的位置。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="3ed3b-111">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="3ed3b-112">每個工作階段最多報告一次裝置區域。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="3ed3b-113">絕不會使用 GPS，因此這類位置報告對於電池的影響很小。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="3ed3b-114">報告的區域用來計算關於使用者、工作階段、事件與錯誤的地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="3ed3b-115">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="3ed3b-116">您可以使用此程序中先前所述的組態，啟用簡易區域位置報告：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3ed3b-117">您也必須指定位置權限。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-117">You also need to specify a location permission.</span></span> <span data-ttu-id="3ed3b-118">此程式碼使用 ``COARSE`` 權限︰</span><span class="sxs-lookup"><span data-stu-id="3ed3b-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="3ed3b-119">如果您的應用程式需要，可以改用 ``ACCESS_FINE_LOCATION`` 。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="3ed3b-120">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-120">Real-time location reporting</span></span>
<span data-ttu-id="3ed3b-121">即時位置報告可報告與裝置相關聯的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="3ed3b-122">這類位置報告預設只會根據基地台識別碼或 WIFI 使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="3ed3b-123">報告只在應用程式在前景 (例如在工作階段) 中執行時才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="3ed3b-124">即時位置「不會」  用來計算統計資料。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="3ed3b-125">其唯一用途，是允許在觸達活動中使用即時地理圍欄 \<Reach-Audience-geofencing\> 準則。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="3ed3b-126">若要啟用即時位置報告，請在您在啟動器活動中設定 Engagement 連接字串的地方加入一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="3ed3b-127">結果看起來如下：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="3ed3b-128">GPS 式報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-128">GPS based reporting</span></span>
<span data-ttu-id="3ed3b-129">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="3ed3b-130">若要啟用 GPS 位置 (精準度大為提高)，請使用組態物件：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3ed3b-131">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="3ed3b-132">背景報告</span><span class="sxs-lookup"><span data-stu-id="3ed3b-132">Background reporting</span></span>
<span data-ttu-id="3ed3b-133">根據預設，即時位置報告只在應用程式在前景 (例如在工作階段) 中執行時才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="3ed3b-134">若也要在背景中啟用報告，請使用此組態物件：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="3ed3b-135">當應用程式在背景中執行，即使啟用 GPS，也只會報告網路位置。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="3ed3b-136">如果使用者重新啟動他們的裝置，則會停止背景位置報告。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="3ed3b-137">若要在開機時自動重新啟動，請加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="3ed3b-138">您還需要新增下列權限 (如果未有此權限)：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="3ed3b-139">Android M 權限</span><span class="sxs-lookup"><span data-stu-id="3ed3b-139">Android M permissions</span></span>
<span data-ttu-id="3ed3b-140">從 Android M 開始，某些權限會在執行階段管理，而且需要使用者核准。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="3ed3b-141">如果您針對 Android API 層級 23，新的應用程式安裝預設會關閉執行階段權限。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="3ed3b-142">否則預設會開啟。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="3ed3b-143">您可以從裝置設定功能表啟用/停用這些權限。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="3ed3b-144">從系統功能表關閉權限會刪除應用程式的背景處理程序，這是一種系統行為，對於在背景中接收推播的功能不會有任何影響。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="3ed3b-145">在 Mobile Engagement 位置報告的環境中，需要在執行階段核准的權限為：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="3ed3b-146">使用標準系統對話方塊向使用者要求權限。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="3ed3b-147">如果使用者核准，告訴 ``EngagementAgent`` 即時列入這項變更。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="3ed3b-148">否則變更會在下次使用者啟動應用程式時處理。</span><span class="sxs-lookup"><span data-stu-id="3ed3b-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="3ed3b-149">以下是在應用程式要求權限並轉送結果 (如果 ``EngagementAgent``收到肯定) 時的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="3ed3b-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
