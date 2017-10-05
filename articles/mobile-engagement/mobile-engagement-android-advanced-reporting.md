---
title: "Azure Mobile Engagement Android SDK 的進階報告選項"
description: "描述如何為 Azure Mobile Engagement Android SDK 進行進階報告以擷取分析"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="5924e-103">Android 上使用 Engagement 的進階報告</span><span class="sxs-lookup"><span data-stu-id="5924e-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5924e-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="5924e-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="5924e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5924e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="5924e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5924e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="5924e-107">Android</span><span class="sxs-lookup"><span data-stu-id="5924e-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="5924e-108">本主題說明 Android 應用程式中的其他報告案例。</span><span class="sxs-lookup"><span data-stu-id="5924e-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="5924e-109">您可以將這些選項套用至 [快速入門](mobile-engagement-android-get-started.md) 教學課程中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5924e-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5924e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5924e-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="5924e-111">您完成的教學課程相當直接明瞭，但您還有一些進階選項可選擇。</span><span class="sxs-lookup"><span data-stu-id="5924e-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="5924e-112">修改 `Activity` 類別</span><span class="sxs-lookup"><span data-stu-id="5924e-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="5924e-113">在[快速入門教學課程](mobile-engagement-android-get-started.md)中，您只需要讓 `*Activity` 子類別繼承對應的 `Engagement*Activity` 類別即可。</span><span class="sxs-lookup"><span data-stu-id="5924e-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="5924e-114">例如，如果您的舊版活動延伸 `ListActivity`，可以將它延伸 `EngagementListActivity`。</span><span class="sxs-lookup"><span data-stu-id="5924e-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5924e-115">使用 `EngagementListActivity` 或 `EngagementExpandableListActivity` 時，務必先呼叫 `requestWindowFeature(...);` 再呼叫 `super.onCreate(...);`，否則會發生當機。</span><span class="sxs-lookup"><span data-stu-id="5924e-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="5924e-116">您可以在 `src` 資料夾中找到這些類別，並將其複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="5924e-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="5924e-117">這些類別也會顯示在 **JavaDoc** 中。</span><span class="sxs-lookup"><span data-stu-id="5924e-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="5924e-118">替代方法：手動呼叫 `startActivity()` 和 `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="5924e-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="5924e-119">如果您無法或不想多載 `Activity` 類別，可以改為直接呼叫 `EngagementAgent` 的方式來開始和結束您的活動。</span><span class="sxs-lookup"><span data-stu-id="5924e-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5924e-120">Android SDK 絕不會呼叫 `endActivity()` 方法，即使在關閉應用程式後也不會呼叫 (在 Android 上，應用程式永遠不會關閉)。</span><span class="sxs-lookup"><span data-stu-id="5924e-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="5924e-121">因此，「強烈」建議在您「所有」活動的 `onResume` 回呼中呼叫 `startActivity()` 方法，以及在您「所有」活動的 `onPause()` 回呼中呼叫 `endActivity()` 方法。</span><span class="sxs-lookup"><span data-stu-id="5924e-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="5924e-122">這是確保不會遺漏工作階段的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="5924e-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="5924e-123">如果遺漏了工作階段，Engagement 服務永遠不會從 Engagement 後端中斷連線 (因為只要工作階段處於暫止狀態，服務就會保持連線)。</span><span class="sxs-lookup"><span data-stu-id="5924e-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="5924e-124">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5924e-124">Here is an example:</span></span>

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

<span data-ttu-id="5924e-125">這個範例類似於 `EngagementActivity` 類別及其變體，原始程式碼位於 `src` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5924e-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="5924e-126">使用 Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="5924e-126">Using Application.onCreate()</span></span>
<span data-ttu-id="5924e-127">您放置在 `Application.onCreate()` 和其他應用程式回呼中的程式碼，會針對您所有應用程式的處理程序而執行，包括 Engagement 服務。</span><span class="sxs-lookup"><span data-stu-id="5924e-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="5924e-128">可能會產生不必要的副作用，例如 Engagement 處理程序中有不必要的記憶體配置和執行緒，或重複的廣播接收器或服務。</span><span class="sxs-lookup"><span data-stu-id="5924e-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="5924e-129">如果覆寫 `Application.onCreate()`，建議在 `Application.onCreate()` 函式的開頭加入下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="5924e-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="5924e-130">您可以對 `Application.onTerminate()`、`Application.onLowMemory()` 和 `Application.onConfigurationChanged(...)` 執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="5924e-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="5924e-131">您也可以不延伸 `Application`，改為延伸 `EngagementApplication`：回呼 `Application.onCreate()` 會進行處理程序檢查，並在目前的處理程序不是裝載 Engagement 服務的處理程序時才會呼叫 `Application.onApplicationProcessCreate()`，相同規則也適用於其他回呼。</span><span class="sxs-lookup"><span data-stu-id="5924e-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="5924e-132">AndroidManifest.xml 檔案中的標籤</span><span class="sxs-lookup"><span data-stu-id="5924e-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="5924e-133">在 AndroidManifest.xml 檔案中的 service 標籤中， `android:label` 屬性可讓您選擇 Engagement 服務的名稱，此名稱會出現在使用者電話的「執行中服務」畫面中。</span><span class="sxs-lookup"><span data-stu-id="5924e-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="5924e-134">建議將此屬性設定為 `"<Your application name>Service"` (例如 `"AcmeFunGameService"`)。</span><span class="sxs-lookup"><span data-stu-id="5924e-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="5924e-135">指定 `android:process` 屬性可確保 Engagement 服務在本身的處理程序中執行 (在與應用程式相同的處理程序中執行 Engagement，可能會造成主要/UI 執行緒回應速度較慢)。</span><span class="sxs-lookup"><span data-stu-id="5924e-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="5924e-136">使用 ProGuard 建置</span><span class="sxs-lookup"><span data-stu-id="5924e-136">Building with ProGuard</span></span>
<span data-ttu-id="5924e-137">如果您使用 ProGuard 建立應用程式封裝，您需要保留一些類別。</span><span class="sxs-lookup"><span data-stu-id="5924e-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="5924e-138">您可以使用下列組態程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="5924e-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
