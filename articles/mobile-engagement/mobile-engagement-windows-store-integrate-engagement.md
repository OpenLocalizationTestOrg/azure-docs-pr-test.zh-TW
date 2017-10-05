---
title: "Windows 通用 app Engagement SDK 整合"
description: "如何將 Azure Mobile Engagement 與 Windows 通用 app 整合"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="81660-103">Windows 通用 app Engagement SDK 整合</span><span class="sxs-lookup"><span data-stu-id="81660-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81660-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="81660-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="81660-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="81660-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="81660-106">iOS</span><span class="sxs-lookup"><span data-stu-id="81660-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="81660-107">Android</span><span class="sxs-lookup"><span data-stu-id="81660-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="81660-108">本程序說明如何以最簡單的方式啟用 Windows 通用 app 內 Engagement 的分析與監視功能。</span><span class="sxs-lookup"><span data-stu-id="81660-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="81660-109">下列步驟便足以啟用計算使用者、工作階段、活動、當機和技術等所有統計資料時需要的記錄檔報告。</span><span class="sxs-lookup"><span data-stu-id="81660-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="81660-110">用來計算其他統計資料 (例如事件、錯誤及工作) 所需的記錄檔報告必須使用 Engagement API 來手動完成 (請參閱 [如何在 Windows 通用 app 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-store-use-engagement-api.md) )，因為這些是應用程式相依的統計資料。</span><span class="sxs-lookup"><span data-stu-id="81660-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="81660-111">支援的版本</span><span class="sxs-lookup"><span data-stu-id="81660-111">Supported versions</span></span>
<span data-ttu-id="81660-112">適用於 Windows 通用 app 的 Mobile Engagement SDK 只能整合至目標為以下作業系統的 Windows 執行階段和通用 Windows 平台應用程式：</span><span class="sxs-lookup"><span data-stu-id="81660-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="81660-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="81660-113">Windows 8</span></span>
* <span data-ttu-id="81660-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="81660-114">Windows 8.1</span></span>
* <span data-ttu-id="81660-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="81660-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="81660-116">Windows 10 (桌上型電腦和行動裝置系列)</span><span class="sxs-lookup"><span data-stu-id="81660-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="81660-117">如果您是以 Windows Phone Silverlight 為目標，則請參考 [Windows Phone Silverlight 整合程序](mobile-engagement-windows-phone-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="81660-117">If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="81660-118">安裝 Mobile Engagement 跨平台 app SDK</span><span class="sxs-lookup"><span data-stu-id="81660-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="81660-119">所有平台</span><span class="sxs-lookup"><span data-stu-id="81660-119">All platforms</span></span>
<span data-ttu-id="81660-120">提供適用於 Windows 通用 app 的 Mobile Engagement SDK 時會使用稱為 *MicrosoftAzure.MobileEngagement*的 Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="81660-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="81660-121">您可以從 Visual Studio Nuget 封裝管理員安裝該封裝。</span><span class="sxs-lookup"><span data-stu-id="81660-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="81660-122">Windows 8.x 和 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="81660-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="81660-123">NuGet 會自動在您的應用程式專案根目錄 `Resources` 資料夾中部署 SDK 資源。</span><span class="sxs-lookup"><span data-stu-id="81660-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="81660-124">Windows 10 通用 Windows 平台應用程式</span><span class="sxs-lookup"><span data-stu-id="81660-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="81660-125">NuGet 目前還不會自動在您的 UWP 應用程式部署 SDK 資源。</span><span class="sxs-lookup"><span data-stu-id="81660-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="81660-126">您必須手動執行，直到 NuGet 重新引進資源部署：</span><span class="sxs-lookup"><span data-stu-id="81660-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="81660-127">開啟 [檔案總管]。</span><span class="sxs-lookup"><span data-stu-id="81660-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="81660-128">瀏覽至以下位置 (**x.x.x** 是您安裝的 Engagement 版本)：*%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="81660-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="81660-129">從檔案總管將 [Resources]  資料夾拖放到您的專案在 Visual Studio 中的根目錄。</span><span class="sxs-lookup"><span data-stu-id="81660-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="81660-130">在 Visual Studio 中，選取您的專案並啟動 [方案總管] 上方的 [顯示所有檔案] 圖示。</span><span class="sxs-lookup"><span data-stu-id="81660-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="81660-131">部分檔案未包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="81660-131">Some files are not included in the project.</span></span> <span data-ttu-id="81660-132">若要將它們一次匯入，請在 [Resources] 資料夾上按一下滑鼠右鍵，[從專案移除] 然後再次在 [Resources] 資料夾上按一次滑鼠右鍵，[加入至專案] 以重新包含整個資料夾。</span><span class="sxs-lookup"><span data-stu-id="81660-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="81660-133">所有來自 [Resources]  資料夾的檔案現在已經包含在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="81660-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="81660-134">新增功能</span><span class="sxs-lookup"><span data-stu-id="81660-134">Add the capabilities</span></span>
<span data-ttu-id="81660-135">Engagement SDK 需要一些 Windows SDK 的功能以正常運作。</span><span class="sxs-lookup"><span data-stu-id="81660-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="81660-136">開啟 `Package.appxmanifest` 檔案，並確定已宣告下列功能：</span><span class="sxs-lookup"><span data-stu-id="81660-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="81660-137">初始化 Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="81660-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="81660-138">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="81660-138">Engagement configuration</span></span>
<span data-ttu-id="81660-139">Engagement 組態會集中在您專案的 `Resources\EngagementConfiguration.xml` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="81660-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="81660-140">編輯此檔案來指定：</span><span class="sxs-lookup"><span data-stu-id="81660-140">Edit this file to specify:</span></span>

* <span data-ttu-id="81660-141">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="81660-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="81660-142">若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="81660-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="81660-143">應用程式的連接字串會顯示在 Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="81660-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="81660-144">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="81660-144">Engagement initialization</span></span>
<span data-ttu-id="81660-145">當您建立新專案時會產生一份 `App.xaml.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="81660-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="81660-146">這個類別繼承自 `Application` ，且包含的許多重要的方法。</span><span class="sxs-lookup"><span data-stu-id="81660-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="81660-147">它將會用來初始化 Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="81660-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="81660-148">修改 `App.xaml.cs`：</span><span class="sxs-lookup"><span data-stu-id="81660-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="81660-149">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="81660-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="81660-150">定義一個方法以針對所有呼叫一次共用 Engagement 初始化：</span><span class="sxs-lookup"><span data-stu-id="81660-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="81660-151">呼叫 `OnLaunched` 方法中的 `InitEngagement`：</span><span class="sxs-lookup"><span data-stu-id="81660-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="81660-152">當您的應用程式使用自訂配置、其他應用程式或命令列啟動時，會呼叫 `OnActivated` 方法。</span><span class="sxs-lookup"><span data-stu-id="81660-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="81660-153">您也需要在您的應用程式啟動時初始化 Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="81660-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="81660-154">若要這樣做，請覆寫 `OnActivated` 方法：</span><span class="sxs-lookup"><span data-stu-id="81660-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="81660-155">我們強烈地建議您不要在應用程式的其他地方新增 Engagement 初始化。</span><span class="sxs-lookup"><span data-stu-id="81660-155">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="81660-156">基本報告</span><span class="sxs-lookup"><span data-stu-id="81660-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="81660-157">建議使用的方法：多載您的 `Page` 類別</span><span class="sxs-lookup"><span data-stu-id="81660-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="81660-158">為了啟用 Engagement 計算使用者、工作階段、活動、當機和技術的統計資料所需的所有記錄檔報告，您可讓所有的 `Page` 子類別繼承自 `EngagementPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="81660-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="81660-159">以下是如何在您應用程式其中一個頁面使用此方法的範例。</span><span class="sxs-lookup"><span data-stu-id="81660-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="81660-160">您可以將相同的方法用於您應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="81660-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="81660-161">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="81660-161">C# Source file</span></span>
<span data-ttu-id="81660-162">修改您頁面的 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="81660-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="81660-163">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="81660-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="81660-164">以 `EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="81660-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="81660-165">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="81660-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="81660-166">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="81660-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="81660-167">如果您的頁面會覆寫 `OnNavigatedTo` 方法，請務必呼叫 `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="81660-167">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="81660-168">否則不會報告活動 (`EngagementPage` 會在其 `OnNavigatedTo` 方法內呼叫 `StartActivity`)。</span><span class="sxs-lookup"><span data-stu-id="81660-168">Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="81660-169">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="81660-169">XAML file</span></span>
<span data-ttu-id="81660-170">修改您頁面的 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="81660-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="81660-171">新增命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="81660-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="81660-172">以 `engagement:EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="81660-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="81660-173">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="81660-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="81660-174">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="81660-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="81660-175">覆寫預設行為</span><span class="sxs-lookup"><span data-stu-id="81660-175">Override the default behaviour</span></span>
<span data-ttu-id="81660-176">根據預設，頁面的類別名稱會在報告時做為活動名稱 (沒有額外的名稱)。</span><span class="sxs-lookup"><span data-stu-id="81660-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="81660-177">如果類別使用 "Page" 尾碼，Engagement 也會移除它。</span><span class="sxs-lookup"><span data-stu-id="81660-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="81660-178">如果想要覆寫名稱的預設行為，您只需將下列新增至您的程式碼：</span><span class="sxs-lookup"><span data-stu-id="81660-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="81660-179">如果想要報告活動的一些額外資訊，您可以將下列新增至您的程式碼：</span><span class="sxs-lookup"><span data-stu-id="81660-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="81660-180">系統會從您頁面的 `OnNavigatedTo` 方法中呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="81660-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="81660-181">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="81660-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="81660-182">如果您無法或不想要多載您的 `Page` 類別，您可以改為透過直接呼叫 `EngagementAgent` 方法來啟動活動。</span><span class="sxs-lookup"><span data-stu-id="81660-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="81660-183">我們建議您於 Page 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="81660-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="81660-184">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="81660-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="81660-185">應用程式關閉時，Windows 通用 SDK 會自動呼叫 `EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="81660-185">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="81660-186">因此，「強烈」建議每當使用者的活動變更時便叫呼叫 `StartActivity` 方法，並且「絕對不要」呼叫 `EndActivity` 方法，此方法會傳送至 Engagement 伺服器，目前的使用者已離開應用程式，這會影響所有應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="81660-186">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="81660-187">進階報告</span><span class="sxs-lookup"><span data-stu-id="81660-187">Advanced reporting</span></span>
<span data-ttu-id="81660-188">(選擇性) 您可以報告應用程式的特定事件、錯誤和工作；若要這樣做，請使用 `EngagementAgent` 類別中找到的其他方法。</span><span class="sxs-lookup"><span data-stu-id="81660-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="81660-189">Engagement API 允許使用所有 Engagement 的進階功能。</span><span class="sxs-lookup"><span data-stu-id="81660-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="81660-190">如需詳細資訊，請參閱 [如何在 Windows 通用 app 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-store-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="81660-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="81660-191">進階組態</span><span class="sxs-lookup"><span data-stu-id="81660-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="81660-192">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="81660-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="81660-193">您可以停用 Engagement 的自動當機報告功能。</span><span class="sxs-lookup"><span data-stu-id="81660-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="81660-194">然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="81660-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="81660-195">如果您打算停用此功能，請注意當您的應用程式中將發生未處理的當機時，Engagement 將不會傳送該當機，「且」亦不會關閉工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="81660-195">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="81660-196">若要停用自動當機報告，只要依照您宣告的方式自訂您的組態即可：</span><span class="sxs-lookup"><span data-stu-id="81660-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="81660-197">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="81660-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="81660-198">在 `<reportCrash>` 和 `</reportCrash>` 標記之間，將報告當機設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="81660-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="81660-199">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="81660-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="81660-200">使用 EngagementConfiguration 物件將報告當機設為 false。</span><span class="sxs-lookup"><span data-stu-id="81660-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="81660-201">高載模式</span><span class="sxs-lookup"><span data-stu-id="81660-201">Burst mode</span></span>
<span data-ttu-id="81660-202">根據預設，Engagement 服務會即時報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="81660-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="81660-203">如果應用程式報告記錄檔的頻率很高，最好先緩衝處理記錄檔，再定期一次報告它們 (此稱為「高載模式」)。</span><span class="sxs-lookup"><span data-stu-id="81660-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="81660-204">若要這樣做，請呼叫方法：</span><span class="sxs-lookup"><span data-stu-id="81660-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="81660-205">該引數是以 「毫秒」為單位的值。</span><span class="sxs-lookup"><span data-stu-id="81660-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="81660-206">如果您想要重新啟動及時記錄，您隨時可以呼叫該方法，而不需要使用任何參數 (或使用 0 為值)。</span><span class="sxs-lookup"><span data-stu-id="81660-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="81660-207">高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響： 所有工作階段和工作持續時間將調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。</span><span class="sxs-lookup"><span data-stu-id="81660-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="81660-208">建議使用低於 30000 (30 秒) 的閾值。</span><span class="sxs-lookup"><span data-stu-id="81660-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="81660-209">您必須留意儲存記錄檔僅限於 300 個項目。</span><span class="sxs-lookup"><span data-stu-id="81660-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="81660-210">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="81660-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="81660-211">高載閾值無法設定為小於 1 秒的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="81660-211">The burst threshold cannot be configured to a period lesser than 1s.</span></span> <span data-ttu-id="81660-212">如果您嘗試這樣做，SDK 會顯示含錯誤訊息的追蹤，並且會自動重設為預設值 (0 秒)。</span><span class="sxs-lookup"><span data-stu-id="81660-212">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s.</span></span> <span data-ttu-id="81660-213">這樣會觸發 SDK 以即時的方式報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="81660-213">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

