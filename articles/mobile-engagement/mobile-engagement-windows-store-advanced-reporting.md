---
title: "Windows 通用進階報告與 MobileApps Engagement"
description: "如何將 Azure Mobile Engagement 與 Windows 通用 app 整合"
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
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="83892-103">使用 Windows 通用 App Engagement SDK 的進階報告</span><span class="sxs-lookup"><span data-stu-id="83892-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83892-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="83892-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="83892-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="83892-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="83892-106">iOS</span><span class="sxs-lookup"><span data-stu-id="83892-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="83892-107">Android</span><span class="sxs-lookup"><span data-stu-id="83892-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="83892-108">本主題說明 Windows 通用應用程式中的其他報告案例。</span><span class="sxs-lookup"><span data-stu-id="83892-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="83892-109">這些案例包含的選項可供您選擇套用至 [快速入門](mobile-engagement-windows-store-dotnet-get-started.md) 教學課程中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="83892-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83892-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="83892-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="83892-111">開始本教學課程之前，您必須先完成 [快速入門](mobile-engagement-windows-store-dotnet-get-started.md) 教學課程，此教學課程相當直接明瞭。</span><span class="sxs-lookup"><span data-stu-id="83892-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="83892-112">本教學課程涵蓋您可以選擇的其他選項。</span><span class="sxs-lookup"><span data-stu-id="83892-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="83892-113">指定執行階段的 Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="83892-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="83892-114">Engagement 組態集中在您專案的 `Resources\EngagementConfiguration.xml` 檔案，這是在 [快速入門](mobile-engagement-windows-store-dotnet-get-started.md) 主題中指定的位置。</span><span class="sxs-lookup"><span data-stu-id="83892-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="83892-115">但是您也可以在執行階段指定它：您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="83892-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="83892-116">建議使用的方法：多載您的 `Page` 類別</span><span class="sxs-lookup"><span data-stu-id="83892-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="83892-117">若要啟用 Engagement 計算使用者、工作階段、活動、當機和技術的統計資料所需的所有記錄檔報告，請讓所有的 `Page` 子類別繼承自 `EngagementPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="83892-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="83892-118">以下是您應用程式其中一個頁面的範例。</span><span class="sxs-lookup"><span data-stu-id="83892-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="83892-119">您可以將相同的方法用於您應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="83892-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="83892-120">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="83892-120">C# Source file</span></span>
<span data-ttu-id="83892-121">修改您頁面的 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="83892-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="83892-122">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="83892-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="83892-123">以 `EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="83892-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="83892-124">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="83892-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="83892-125">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="83892-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="83892-126">如果您的頁面會覆寫 `OnNavigatedTo` 方法，請務必呼叫 `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="83892-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="83892-127">否則不會報告活動 (`EngagementPage` 會在其 `OnNavigatedTo` 方法內呼叫 `StartActivity`)。</span><span class="sxs-lookup"><span data-stu-id="83892-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="83892-128">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="83892-128">XAML file</span></span>
<span data-ttu-id="83892-129">修改您頁面的 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="83892-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="83892-130">新增命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="83892-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="83892-131">以 `engagement:EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="83892-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="83892-132">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="83892-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="83892-133">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="83892-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="83892-134">覆寫預設行為</span><span class="sxs-lookup"><span data-stu-id="83892-134">Override the default behaviour</span></span>
<span data-ttu-id="83892-135">根據預設，頁面的類別名稱會在報告時做為活動名稱 (沒有額外的名稱)。</span><span class="sxs-lookup"><span data-stu-id="83892-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="83892-136">如果類別使用 "Page" 尾碼，Engagement 會移除它。</span><span class="sxs-lookup"><span data-stu-id="83892-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="83892-137">若要覆寫名稱的預設行為，請加入下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="83892-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="83892-138">若要報告活動的額外資訊，請加入下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="83892-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="83892-139">系統會從您頁面的 `OnNavigatedTo` 方法中呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="83892-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="83892-140">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="83892-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="83892-141">如果您無法或不想要多載您的 `Page` 類別，您可以改為透過直接呼叫 `EngagementAgent` 方法來啟動活動。</span><span class="sxs-lookup"><span data-stu-id="83892-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="83892-142">我們建議您於 Page 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="83892-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="83892-143">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="83892-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="83892-144">應用程式關閉時，Windows 通用 SDK 會自動呼叫 `EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="83892-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="83892-145">因此，「強烈」建議每當使用者的活動變更時便叫呼叫 `StartActivity` 方法，並且「絕對不要」呼叫 `EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="83892-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="83892-146">這個方法會通知 Engagement 伺服器目前的使用者已離開應用程式，這會影響所有應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="83892-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="83892-147">進階報告</span><span class="sxs-lookup"><span data-stu-id="83892-147">Advanced reporting</span></span>
<span data-ttu-id="83892-148">(選擇性) 您可以報告應用程式的特定事件、錯誤和工作；若要這樣做，請使用 `EngagementAgent` 類別中找到的其他方法。</span><span class="sxs-lookup"><span data-stu-id="83892-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="83892-149">Engagement API 允許使用所有 Engagement 的進階功能。</span><span class="sxs-lookup"><span data-stu-id="83892-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="83892-150">如需詳細資訊，請參閱 [如何在 Windows 通用 app 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-store-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="83892-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

