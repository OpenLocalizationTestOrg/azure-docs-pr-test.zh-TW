---
title: "Windows Phone Silverlight Engagement SDK 整合"
description: "如何將 Azure Mobile Engagement 與 Windows Phone Silverlight 應用程式整合"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="7530e-103">Windows Phone Silverlight Engagement SDK 整合</span><span class="sxs-lookup"><span data-stu-id="7530e-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7530e-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="7530e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="7530e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7530e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="7530e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7530e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="7530e-107">Android</span><span class="sxs-lookup"><span data-stu-id="7530e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="7530e-108">本程序說明如何以最簡單的方式啟用 Windows Phone Silverlight 應用程式內 Azure Mobile Engagement 的分析與監視功能。</span><span class="sxs-lookup"><span data-stu-id="7530e-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="7530e-109">下列步驟便足以啟用計算使用者、工作階段、活動、當機和技術等所有統計資料時需要的記錄檔報告。</span><span class="sxs-lookup"><span data-stu-id="7530e-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="7530e-110">用來計算其他統計資料 (例如事件、錯誤和工作) 所需的記錄檔報告必須使用 Engagement API 來手動完成 (請參閱下方的 [如何在 Windows Phone Silverlight 應用程式中使用進階的 Mobile Engagement 標籤 API](mobile-engagement-windows-phone-use-engagement-api.md) )，因為這些是與應用程式相依的統計資料。</span><span class="sxs-lookup"><span data-stu-id="7530e-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="7530e-111">支援的版本</span><span class="sxs-lookup"><span data-stu-id="7530e-111">Supported versions</span></span>
<span data-ttu-id="7530e-112">適用於 Windows Silverlight 的 Mobile Engagement SDK 只能整合至目標為以下作業系統的應用程式：</span><span class="sxs-lookup"><span data-stu-id="7530e-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="7530e-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="7530e-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="7530e-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="7530e-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="7530e-115">如果您的目標是 Windows Phone 8.1 (非 Silverlight)，請參閱 [Windows 通用整合程序](mobile-engagement-windows-store-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="7530e-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="7530e-116">安裝 Mobile Engagement Silverlight SDK</span><span class="sxs-lookup"><span data-stu-id="7530e-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="7530e-117">提供適用於 Windows Silverlight 的 Mobile Engagement SDK 時會使用稱為 *MicrosoftAzure.MobileEngagement*的 Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="7530e-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="7530e-118">您可以從 Visual Studio Nuget 封裝管理員安裝該封裝。</span><span class="sxs-lookup"><span data-stu-id="7530e-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="7530e-119">新增功能</span><span class="sxs-lookup"><span data-stu-id="7530e-119">Add the capabilities</span></span>
<span data-ttu-id="7530e-120">Engagement SDK 需要一些 Windows Phone Silverlight SDK 的功能才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="7530e-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="7530e-121">開啟 `WMAppManifest.xml` 檔案，並確定 `Capabilities` 面板中已宣告下列功能：</span><span class="sxs-lookup"><span data-stu-id="7530e-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="7530e-122">初始化 Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="7530e-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="7530e-123">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="7530e-123">Engagement configuration</span></span>
<span data-ttu-id="7530e-124">Engagement 組態會集中在您專案的 `Resources\EngagementConfiguration.xml` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7530e-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="7530e-125">編輯此檔案來指定：</span><span class="sxs-lookup"><span data-stu-id="7530e-125">Edit this file to specify :</span></span>

* <span data-ttu-id="7530e-126">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7530e-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="7530e-127">若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="7530e-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="7530e-128">應用程式的連接字串會顯示在 Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="7530e-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="7530e-129">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="7530e-129">Engagement initialization</span></span>
<span data-ttu-id="7530e-130">當您建立新專案時會產生一份 `App.xaml.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7530e-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="7530e-131">這個類別繼承自 `Application` ，且包含的許多重要的方法。</span><span class="sxs-lookup"><span data-stu-id="7530e-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="7530e-132">它將會用來初始化 Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="7530e-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="7530e-133">修改 `App.xaml.cs`：</span><span class="sxs-lookup"><span data-stu-id="7530e-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="7530e-134">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7530e-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="7530e-135">在 `Application_Launching` 方法中插入 `EngagementAgent.Instance.Init`：</span><span class="sxs-lookup"><span data-stu-id="7530e-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="7530e-136">在 `Application_Activated` 方法中插入 `EngagementAgent.Instance.OnActivated`：</span><span class="sxs-lookup"><span data-stu-id="7530e-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="7530e-137">我們強烈地建議您不要在應用程式的其他地方加入 Engagement 初始化。</span><span class="sxs-lookup"><span data-stu-id="7530e-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="7530e-138">不過請注意， `EngagementAgent.Instance.Init` 方法執行於專用的執行緒，而非 UI 執行緒。</span><span class="sxs-lookup"><span data-stu-id="7530e-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="7530e-139">基本報告</span><span class="sxs-lookup"><span data-stu-id="7530e-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="7530e-140">建議使用的方法：多載您的 `PhoneApplicationPage` 類別</span><span class="sxs-lookup"><span data-stu-id="7530e-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="7530e-141">為了啟用 Engagement 計算使用者、工作階段、活動、當機和技術的統計資料所需的所有記錄檔報告，您可讓所有的 `PhoneApplicationPage` 子類別繼承自 `EngagementPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="7530e-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="7530e-142">以下是如何在您應用程式其中一個頁面使用此方法的範例。</span><span class="sxs-lookup"><span data-stu-id="7530e-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="7530e-143">您可以將相同的方法用於您應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="7530e-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="7530e-144">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="7530e-144">C# Source file</span></span>
<span data-ttu-id="7530e-145">修改您的頁面 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="7530e-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="7530e-146">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7530e-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="7530e-147">以 `EngagementPage` 取代 `PhoneApplicationPage`：</span><span class="sxs-lookup"><span data-stu-id="7530e-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="7530e-148">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="7530e-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="7530e-149">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="7530e-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="7530e-150">如果您的頁面繼承自 `OnNavigatedTo` 方法，請注意要讓 `base.OnNavigatedTo(e)` 執行呼叫。</span><span class="sxs-lookup"><span data-stu-id="7530e-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="7530e-151">否則不會報告活動。</span><span class="sxs-lookup"><span data-stu-id="7530e-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="7530e-152">事實上，`EngagementPage` 會呼叫 `OnNavigatedTo` 方法內的 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="7530e-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="7530e-153">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="7530e-153">XAML file</span></span>
<span data-ttu-id="7530e-154">修改您的頁面 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="7530e-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="7530e-155">加入至命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="7530e-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="7530e-156">以 `engagement:EngagementPage` 取代 `phone:PhoneApplicationPage`：</span><span class="sxs-lookup"><span data-stu-id="7530e-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="7530e-157">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="7530e-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="7530e-158">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="7530e-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="7530e-159">覆寫預設行為</span><span class="sxs-lookup"><span data-stu-id="7530e-159">Override the default behavior</span></span>
<span data-ttu-id="7530e-160">根據預設，頁面的類別名稱會在報告時做為活動名稱 (沒有額外的名稱)。</span><span class="sxs-lookup"><span data-stu-id="7530e-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="7530e-161">如果類別使用 "Page" 尾碼，Engagement 也會移除它。</span><span class="sxs-lookup"><span data-stu-id="7530e-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="7530e-162">如果想要覆寫名稱的預設行為，您只需將下列加入您的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7530e-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="7530e-163">如果想要報告活動的一些額外資訊，您可以將以下內容加入至您的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7530e-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="7530e-164">系統會從您頁面的 `OnNavigatedTo` 方法中呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="7530e-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="7530e-165">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="7530e-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="7530e-166">如果您無法或不想要多載您的 `PhoneApplicationPage` 類別，您可以改為透過直接呼叫 `EngagementAgent` 方法來啟動活動。</span><span class="sxs-lookup"><span data-stu-id="7530e-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="7530e-167">我們建議您於 PhoneApplicationPage 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="7530e-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="7530e-168">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="7530e-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="7530e-169">SDK 會在應用程式關閉時自動呼叫 `EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="7530e-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="7530e-170">因此，「強烈」建議每當使用者的活動變更時便叫呼叫 `StartActivity` 方法，並且「絕對不要」呼叫 `EndActivity` 方法。</span><span class="sxs-lookup"><span data-stu-id="7530e-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="7530e-171">這個方法會將訊息傳送給 Engagement 伺服器，目前的使用者已離開應用程式，這會影響所有應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7530e-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="7530e-172">進階報告</span><span class="sxs-lookup"><span data-stu-id="7530e-172">Advanced reporting</span></span>
<span data-ttu-id="7530e-173">(選擇性) 您可以報告應用程式的特定事件、錯誤和工作；若要這樣做，請使用 `EngagementAgent` 類別中找到的其他方法。</span><span class="sxs-lookup"><span data-stu-id="7530e-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="7530e-174">Engagement API 允許使用所有 Engagement 的進階功能。</span><span class="sxs-lookup"><span data-stu-id="7530e-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="7530e-175">如需詳細資訊，請參閱 [如何在 Windows Phone Silverlight 應用程式中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-phone-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7530e-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="7530e-176">進階組態</span><span class="sxs-lookup"><span data-stu-id="7530e-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="7530e-177">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="7530e-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="7530e-178">您可以停用 Engagement 的自動當機報告功能。</span><span class="sxs-lookup"><span data-stu-id="7530e-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="7530e-179">然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="7530e-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="7530e-180">如果您打算停用此功能，請注意當您的應用程式中將發生未處理的當機時，Engagement 將不會傳送該當機，「且」亦不會關閉工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="7530e-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="7530e-181">若要停用自動當機報告，只要依照您宣告的方式自訂您的組態即可：</span><span class="sxs-lookup"><span data-stu-id="7530e-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="7530e-182">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="7530e-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="7530e-183">在 `<reportCrash>` 和 `</reportCrash>` 標記之間，將報告當機設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="7530e-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="7530e-184">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="7530e-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="7530e-185">使用 EngagementConfiguration 物件將報告當機設為 false。</span><span class="sxs-lookup"><span data-stu-id="7530e-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="7530e-186">高載模式</span><span class="sxs-lookup"><span data-stu-id="7530e-186">Burst mode</span></span>
<span data-ttu-id="7530e-187">根據預設，Engagement 服務會即時報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7530e-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="7530e-188">如果應用程式報告記錄檔的頻率很高，最好先緩衝處理記錄檔，再定期一次報告它們 (此稱為「高載模式」)。</span><span class="sxs-lookup"><span data-stu-id="7530e-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="7530e-189">若要這樣做，請呼叫方法：</span><span class="sxs-lookup"><span data-stu-id="7530e-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="7530e-190">該引數是以 「毫秒」為單位的值。</span><span class="sxs-lookup"><span data-stu-id="7530e-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="7530e-191">如果您想要重新啟動及時記錄，您隨時可以呼叫該方法，而不需要使用任何參數 (或使用 0 為值)。</span><span class="sxs-lookup"><span data-stu-id="7530e-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="7530e-192">高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響： 所有工作階段和工作持續時間將調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。</span><span class="sxs-lookup"><span data-stu-id="7530e-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="7530e-193">建議使用低於 30000 (30 秒) 的閾值。</span><span class="sxs-lookup"><span data-stu-id="7530e-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="7530e-194">您必須留意儲存記錄檔僅限於 300 個項目。</span><span class="sxs-lookup"><span data-stu-id="7530e-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="7530e-195">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7530e-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="7530e-196">高載閾值無法設定為小於一秒的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7530e-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="7530e-197">如果您嘗試這樣做，SDK 會顯示含錯誤訊息的追蹤，並且會自動重設為預設值 (0 秒)。</span><span class="sxs-lookup"><span data-stu-id="7530e-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="7530e-198">這樣會觸發 SDK 以即時的方式報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7530e-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

