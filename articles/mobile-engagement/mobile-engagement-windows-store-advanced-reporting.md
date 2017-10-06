---
title: "通用進階報告功能與 MobileApps Engagement aaaWindows"
description: "如何 tooIntegrate 與 Windows 通用應用程式的 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="04f0e-103">以 hello Windows 通用應用程式 Engagement SDK 的進階的報告</span><span class="sxs-lookup"><span data-stu-id="04f0e-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04f0e-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="04f0e-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="04f0e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="04f0e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="04f0e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="04f0e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="04f0e-107">Android</span><span class="sxs-lookup"><span data-stu-id="04f0e-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="04f0e-108">本主題說明 Windows 通用應用程式中的其他報告案例。</span><span class="sxs-lookup"><span data-stu-id="04f0e-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="04f0e-109">這些案例包括您可以選擇建立 hello tooapply toohello 應用程式的選項[入門](mobile-engagement-windows-store-dotnet-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="04f0e-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04f0e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="04f0e-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="04f0e-111">再開始本教學課程，您必須先完成 hello[入門](mobile-engagement-windows-store-dotnet-get-started.md)教學課程中，已刻意直接且簡單。</span><span class="sxs-lookup"><span data-stu-id="04f0e-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="04f0e-112">本教學課程涵蓋您可以選擇的其他選項。</span><span class="sxs-lookup"><span data-stu-id="04f0e-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="04f0e-113">指定執行階段的 Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="04f0e-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="04f0e-114">hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`檔案的專案，也就是其中指定在 hello[入門](mobile-engagement-windows-store-dotnet-get-started.md)主題。</span><span class="sxs-lookup"><span data-stu-id="04f0e-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="04f0e-115">但是您也可以指定它在執行階段： 您可以呼叫下列方法 hello Engagement 代理程式初始化之前 hello:</span><span class="sxs-lookup"><span data-stu-id="04f0e-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="04f0e-116">建議使用的方法：多載您的 `Page` 類別</span><span class="sxs-lookup"><span data-stu-id="04f0e-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="04f0e-117">tooactivate Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的 hello reporting 進行所有您`Page`子類別是繼承自 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="04f0e-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="04f0e-118">以下是您應用程式其中一個頁面的範例。</span><span class="sxs-lookup"><span data-stu-id="04f0e-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="04f0e-119">您可以 hello 相同的動作，為您的應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="04f0e-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="04f0e-120">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="04f0e-120">C# Source file</span></span>
<span data-ttu-id="04f0e-121">修改您頁面的 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="04f0e-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="04f0e-122">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="04f0e-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="04f0e-123">以 `EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="04f0e-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="04f0e-124">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="04f0e-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="04f0e-125">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="04f0e-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="04f0e-126">如果您的頁面會覆寫 hello`OnNavigatedTo`方法，是確定 toocall `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="04f0e-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="04f0e-127">否則，不會報告 hello 活動 (hello`EngagementPage`呼叫`StartActivity`內其`OnNavigatedTo`方法)。</span><span class="sxs-lookup"><span data-stu-id="04f0e-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="04f0e-128">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="04f0e-128">XAML file</span></span>
<span data-ttu-id="04f0e-129">修改您頁面的 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="04f0e-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="04f0e-130">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="04f0e-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="04f0e-131">以 `engagement:EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="04f0e-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="04f0e-132">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="04f0e-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="04f0e-133">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="04f0e-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="04f0e-134">覆寫預設行為，hello</span><span class="sxs-lookup"><span data-stu-id="04f0e-134">Override hello default behaviour</span></span>
<span data-ttu-id="04f0e-135">根據預設，hello 活動名稱，以及不需額外會報告 hello 頁面 hello 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="04f0e-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="04f0e-136">如果 hello 類別使用 hello"Page"後置詞，Engagement 會移除它。</span><span class="sxs-lookup"><span data-stu-id="04f0e-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="04f0e-137">hello 名稱 toooverride hello 預設行為會加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04f0e-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="04f0e-138">tooreport 額外的資訊與程式活動中，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04f0e-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="04f0e-139">這些方法從呼叫 hello 內`OnNavigatedTo`頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="04f0e-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="04f0e-140">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="04f0e-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="04f0e-141">如果您無法或不想 toooverload 您`Page`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`直接的方法。</span><span class="sxs-lookup"><span data-stu-id="04f0e-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="04f0e-142">我們建議您於 Page 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="04f0e-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="04f0e-143">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="04f0e-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="04f0e-144">hello Windows 通用 SDK 會自動呼叫 hello `EndActivity` hello 應用程式關閉時的方法。</span><span class="sxs-lookup"><span data-stu-id="04f0e-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="04f0e-145">因此，它是**高**建議 toocall hello`StartActivity`每當 hello 使用者的 hello 活動變更時，方法和太**永不**呼叫 hello`EndActivity`方法。</span><span class="sxs-lookup"><span data-stu-id="04f0e-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="04f0e-146">這個方法會通知 hello Engagement 伺服器 hello 目前的使用者已離開 hello 應用程式，將會影響所有的應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04f0e-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="04f0e-147">進階報告</span><span class="sxs-lookup"><span data-stu-id="04f0e-147">Advanced reporting</span></span>
<span data-ttu-id="04f0e-148">（選擇性） 您可能會想 tooreport 應用程式特定事件、 錯誤和作業、 toodo 因此、 使用 hello 其他方法位於 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="04f0e-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="04f0e-149">hello Engagement 應用程式開發介面可讓您使用所有參與的進階功能。</span><span class="sxs-lookup"><span data-stu-id="04f0e-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="04f0e-150">如需詳細資訊，請參閱[toouse hello 如何進階標記 Windows 通用應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="04f0e-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

