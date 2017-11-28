---
title: "aaaAdvanced 報告 Azure Mobile Engagement Android SDK 選項"
description: "描述如何 toodo 進階報告 toocapture 分析 Azure Mobile Engagement Android SDK"
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
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="c6577-103">Android 上使用 Engagement 的進階報告</span><span class="sxs-lookup"><span data-stu-id="c6577-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6577-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="c6577-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="c6577-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c6577-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="c6577-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c6577-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="c6577-107">Android</span><span class="sxs-lookup"><span data-stu-id="c6577-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="c6577-108">本主題說明 Android 應用程式中的其他報告案例。</span><span class="sxs-lookup"><span data-stu-id="c6577-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="c6577-109">您可以套用這些選項的 toohello 應用程式建立 hello[入門](mobile-engagement-android-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="c6577-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6577-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c6577-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="c6577-111">您已完成的 hello 教學課程刻意直接和簡單，但屬於進階的選項，您可以選擇。</span><span class="sxs-lookup"><span data-stu-id="c6577-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="c6577-112">修改 `Activity` 類別</span><span class="sxs-lookup"><span data-stu-id="c6577-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="c6577-113">在 hello[快速入門教學課程](mobile-engagement-android-get-started.md)，只 toodo 已 toomake 您`*Activity`子類別繼承自 hello 對應`Engagement*Activity`類別。</span><span class="sxs-lookup"><span data-stu-id="c6577-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="c6577-114">例如，如果您的舊版活動延伸 `ListActivity`，可以將它延伸 `EngagementListActivity`。</span><span class="sxs-lookup"><span data-stu-id="c6577-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6577-115">當使用`EngagementListActivity`或`EngagementExpandableListActivity`，請確定任何呼叫太`requestWindowFeature(...);`太進行 hello 呼叫之前`super.onCreate(...);`，否則會發生損毀。</span><span class="sxs-lookup"><span data-stu-id="c6577-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="c6577-116">您可以在 hello 找到這些類別`src`資料夾，並可以將其複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="c6577-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="c6577-117">hello 類別中也會有 hello **JavaDoc**。</span><span class="sxs-lookup"><span data-stu-id="c6577-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="c6577-118">替代方法：手動呼叫 `startActivity()` 和 `endActivity()`</span><span class="sxs-lookup"><span data-stu-id="c6577-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="c6577-119">如果您無法或不想 toooverload 您`Activity`類別，您可以改為開始和結束您的活動藉由呼叫 hello`EngagementAgent`的直接的方法。</span><span class="sxs-lookup"><span data-stu-id="c6577-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6577-120">hello Android SDK 從未呼叫 hello`endActivity()`方法，即使關閉 hello 應用程式 （在 Android 上，應用程式會永遠不會關閉）。</span><span class="sxs-lookup"><span data-stu-id="c6577-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="c6577-121">因此，它是*高*建議 toocall hello `startActivity()` hello 中的方法`onResume`回呼的*所有*程式活動與 hello `endActivity()` hello 中的方法`onPause()`回呼的*所有*程式活動。</span><span class="sxs-lookup"><span data-stu-id="c6577-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="c6577-122">這是 hello 唯一方式 toobe 確定不會遺漏工作階段。</span><span class="sxs-lookup"><span data-stu-id="c6577-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="c6577-123">如果工作階段外洩，hello Engagement 服務永遠不會中斷 hello Engagement 後端 （因為 hello 服務仍會保持連接，只要工作階段已暫止）。</span><span class="sxs-lookup"><span data-stu-id="c6577-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="c6577-124">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="c6577-124">Here is an example:</span></span>

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

<span data-ttu-id="c6577-125">這個範例是類似 toohello`EngagementActivity`類別與變種，提供其原始程式碼中 hello`src`資料夾。</span><span class="sxs-lookup"><span data-stu-id="c6577-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="c6577-126">使用 Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="c6577-126">Using Application.onCreate()</span></span>
<span data-ttu-id="c6577-127">您將放置在任何程式碼`Application.onCreate()`和其他應用程式中執行所有應用程式的程序，包括 hello Engagement 服務回呼。</span><span class="sxs-lookup"><span data-stu-id="c6577-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="c6577-128">它可能會不必要的副作用，例如不必要的記憶體配置和 hello Engagement 的處理序中的執行緒或重複廣播接收器或服務。</span><span class="sxs-lookup"><span data-stu-id="c6577-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="c6577-129">如果您覆寫`Application.onCreate()`，我們建議您加入下列程式碼片段在 hello 開頭的 hello 您`Application.onCreate()`函式：</span><span class="sxs-lookup"><span data-stu-id="c6577-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="c6577-130">您可以 hello 相同的動作，如`Application.onTerminate()`， `Application.onLowMemory()`，和`Application.onConfigurationChanged(...)`。</span><span class="sxs-lookup"><span data-stu-id="c6577-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="c6577-131">您也可以擴充`EngagementApplication`而不是擴充`Application`: hello 回呼`Application.onCreate()`程序的核取並呼叫沒有 hello`Application.onApplicationProcessCreate()`僅 hello 目前處理序是否不 hello 一個裝載 hello Engagement 服務，hello 適用相同的規則hello 其他回呼。</span><span class="sxs-lookup"><span data-stu-id="c6577-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="c6577-132">Hello AndroidManifest.xml 檔中的標記</span><span class="sxs-lookup"><span data-stu-id="c6577-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="c6577-133">在 hello AndroidManifest.xml 檔中的 hello 服務標記，hello`android:label`屬性可讓您的行動服務的 hello toochoose hello 名稱出現 tooend 使用者在他們的電話號碼 hello 」 執行的服務 」 畫面中。</span><span class="sxs-lookup"><span data-stu-id="c6577-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="c6577-134">我們建議將此屬性設定太`"<Your application name>Service"`(例如， `"AcmeFunGameService"`)。</span><span class="sxs-lookup"><span data-stu-id="c6577-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="c6577-135">指定 hello`android:process`屬性可確保該 hello Engagement 服務執行其自己的處理程序 （在相同的處理序當做您的應用程式會讓您的主要/UI 執行緒可能較不回應 hello 執行 Engagement）。</span><span class="sxs-lookup"><span data-stu-id="c6577-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="c6577-136">使用 ProGuard 建置</span><span class="sxs-lookup"><span data-stu-id="c6577-136">Building with ProGuard</span></span>
<span data-ttu-id="c6577-137">如果您建立使用 ProGuard 應用程式套件，您需要 tookeep 某些類別。</span><span class="sxs-lookup"><span data-stu-id="c6577-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="c6577-138">您可以使用下列組態程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6577-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
